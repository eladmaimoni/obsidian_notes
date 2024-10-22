https://www.geeksforgeeks.org/introduction-to-knapsack-problem-its-types-and-how-to-solve-them/

https://www.geeksforgeeks.org/problems/fractional-knapsack-1587115620/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card


```
    double fractionalKnapsack(vector<int>& values, vector<int>& weights, int w) 
    {
        
        // greedy - take the item with the most value per weight, at most one item
        
        // 1. sort the value / weights according to their value / weight (descending order)
        // 2. iterate over them, insert as much weight as possible for the first one
        // 3. return the total value accumulated
        
       struct ValueWeight
       {
           int value;
           int weight;
       };
       
       vector<ValueWeight> vals(values.size());
       
       for (auto i = 0u; i < values.size(); ++i)
       {
           vals[i] = ValueWeight{values[i], weights[i]};
       }
       
       std::sort(vals.begin(), vals.end(), [](const ValueWeight& a, const ValueWeight& b) {
           
           double a_ratio = (double)a.value / a.weight;
           double b_ratio = (double)b.value / b.weight;
           return a_ratio > b_ratio;
       });

       double total = 0.0;
       for (auto i = 0u; i < vals.size(); ++i)
       {
           auto value = vals[i].value;
           auto weight = vals[i].weight;
           
           if (weight <= w)
           {
               total += value;
               w -= weight;
           }
           else if (w > 0)
           {
               auto partial = (double)w / weight;
               total += value * partial;
               break;
           }
           else
           {
               break;
           }
       }
       
       return total;
       
    }
```