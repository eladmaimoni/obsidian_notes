https://www.geeksforgeeks.org/problems/knapsack-with-duplicate-items4201/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card

```
    int knapSack(int N, int W, int val[], int wt[])
    {
        auto cols = W + 1;
        //auto rows = N + 1;
        vector<int> best_solution(cols, 0);
        
        for (auto w = 1; w <= W; ++w)
        {
            for (auto jj = 0; jj < N; ++jj) // inner loop since we can choose an element as many time as we want
            {
                auto value = val[jj];
                auto weight = wt[jj];
                
                auto prev_capacity = w - weight;
                
                if (prev_capacity >= 0)
                {
                    auto prev_best = best_solution[prev_capacity];
                    auto candidate = prev_best + value;
                    
                    if (candidate > best_solution[w])
                    {
                        best_solution[w] = candidate;
                    }
                }
            }
        }
        

        return best_solution[W];
        
    }
```