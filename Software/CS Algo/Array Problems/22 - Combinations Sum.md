https://leetcode.com/problems/combination-sum/solutions/

### Works but wrong direction
- this is an attempt to use DP - since we can say that there is a subproblem here
  - using K - 1 items to a target sum $c < C$ can is a sub-solution for $K, C$ 
  - this results in a lot of memory usage $O(NK)$ at least
  - time complexity is also bad (times 3)
```
vector<vector<int>> combinationSum(vector<int>& candidates, int target) 
{
    // sum to reach target array
    // each candidate may be used multiple times
    
    // min number of coins

    // we can count the number of combinations that can sum up to target
    std::vector<int> number_of_combinations_to_target(target + 1, 0);
    number_of_combinations_to_target[0] = 0;

    using CombinationsArray = vector<vector<int>>;
    vector<vector<int>> combinations; // we can keep the all the combinations, but this will be O(n^3)
    vector<CombinationsArray> combinations_for_target(target + 1);

    for (auto candidate : candidates)
    {        
        for (auto current_target = target; current_target >= 1; --current_target)
        {
            auto max_instances = current_target / candidate;
            for (auto kk = 1; kk <= max_instances; ++kk)
            {
                auto c = candidate * kk;

                auto pre_target = current_target - c;

                if (pre_target == 0)
                {
                    // equals the necessary sum explicitly

                    vector<int> comb(kk, candidate);
                    combinations_for_target[current_target].emplace_back(move(comb));
                    // number_of_combinations_to_target[current_target] += number_of_combinations_to_target[pre_target];
                }
                else if (pre_target > 0)
                {
                    // there are combinations for pre target
                    // add them to the current target
                    for (auto comb : combinations_for_target[pre_target])
                    {   
                        for (auto i = 0; i < kk; ++i) 
                        {
                            comb.emplace_back(candidate);
                        }

                        combinations_for_target[current_target].emplace_back(move(comb));
                    }
                }

            }

        }
    }

    return combinations_for_target[target];
}
```

#### DFS
this is basically finding all routes (cyclic or not) that result in the target sum
we can consider each node to be connected to all forward nodes including itself
2 -> 3 -> 5
where each node also has a loop to itself (but not backwards)+
```
void dfs(const std::vector<int>& candidates, int i, int target, std::vector<int>& current_path, vector<vector<int>>& results)
{
    if (i == candidates.size()) return;

    auto val = candidates[i];

    auto leftover = target - val;
    current_path.emplace_back(val);

    if (leftover == 0)
    {
        results.emplace_back(current_path);
    }
    else if (leftover > 0)
    {
        for (auto j = i; j < candidates.size(); ++j)
        {
            dfs(candidates, j, leftover, current_path, results);
        }
    }

    current_path.pop_back();
}
vector<vector<int>> combinationSum(vector<int>& candidates, int target)
{
    vector<vector<int>> results;
    vector<int> path;
    for (auto i = 0; i < candidates.size(); ++i)
    {
        dfs(candidates, i, target,  path, results);
    }

    return results;
}
```