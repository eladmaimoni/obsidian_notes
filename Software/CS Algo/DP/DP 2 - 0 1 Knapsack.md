Problem:
maximize total value, each value may be chosen once limited to total capacity.

https://www.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1

```
    int knapsack(int max_capacity, vector<int>& weights, vector<int>& values) 
    {
        std::vector<int> max_value_for_capacity(max_capacity + 1, 0);
        auto n = weights.size();
        
        for (auto i = 0; i < n; ++i) // each value may be chosen once
        {
            auto i_value = values[i];
            auto i_weight = weights[i];
            
            for (auto w = max_capacity; w >= i_weight; --w)
            {
                auto max_value_for_prev_weight = max_value_for_capacity[w - i_weight];
                
                auto candidate = max_value_for_prev_weight + i_value;
                
                if (candidate > max_value_for_capacity[w])
                {
                    max_value_for_capacity[w] = candidate;
                }
            }
        }
        
        return max_value_for_capacity[max_capacity];
    }
```

- Note that weights can be `1` and then the problem appears as "choose the maximum of K items" that yield the highest value

### DP characteristics 
- Optimal substructure: 
	- The best solution for a capacity $C$ will combines the best solution for some smaller capacity $c < C$ together with an additional element chosen that makes the capacity exceed $c$
	- Hence it make sense to calculate the best solution per capacity
- Overlapping subproblems
	- given some capacities $C_1$ and $C_2$, we will need the best solutions for all cases $c < C_1, C_2$
- Tabulation:
	- We solve the the solution bottom-up: first for the smaller capacity and gradually for the larger capacities, remembering the solution for the smaller capacities. 
- sdf