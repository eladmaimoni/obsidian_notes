
- we need to buy low and sell high
- ideally we will sell just before stocks decrease in price and buy just before they increase in size

Algorithm
- go through the price array
- if the price goes up - buy - just before it goes up
- if the price goes down - keep the stock just until it goes up again

```
    vector<vector<int> > stockBuySell(vector<int> A, int n)
    {
        vector<vector<int> > result;
        auto buy_idx = -1;
        auto sell_idx = -1;
        auto price = A[0];
        for (auto i = 1; i < n; ++i)
        {
            auto next_price = A[i];
            
            if (next_price > price && buy_idx == -1)
            {
                // price will go up, we better buy
                buy_idx = i - 1;
            }
            else if (next_price < price && buy_idx != -1)
            {
                // price will go down, we better sell
                sell_idx = i - 1;
                
                result.push_back({buy_idx, sell_idx});
                buy_idx = -1;
                
            }
            price = next_price;    
        }
      
        if (buy_idx != -1)
        {
            // we bought stocks, but prices didn't drop  
            // at the last day, so we sell

            result.push_back({buy_idx, n - 1});
        }
        return result;
    }
```