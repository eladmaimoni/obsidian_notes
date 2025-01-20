https://leetcode.com/problems/combination-sum-ii/?envType=problem-list-v2&envId=array&difficulty=MEDIUM

- we are not allowed to start a combination from the same number or else we might have duplicates
- this applies to sub combinations as well
```
void dfs(vector<int>& candidates, int i, int target, vector<int>& current_path, vector<vector<int>>& res)
{
    auto val = candidates[i];

    current_path.emplace_back(val);
    auto leftover = target - val;

    if (leftover == 0)
    {
        res.emplace_back(current_path);
    }
    else if (leftover > 0)
    {
        auto j = i + 1;

        if (j < candidates.size())
        {
            dfs(candidates, j, leftover, current_path, res);
            ++j;

            for (; j < candidates.size(); ++j)
            {
                if (candidates[j] > candidates[j - 1])
                {
                    dfs(candidates, j, leftover, current_path, res);
                }
            }
        }
        
 
    }

    current_path.pop_back();
}

vector<vector<int>> combinationSum2(vector<int>& candidates, int target) 
{
    std::sort(candidates.begin(), candidates.end());
    vector<vector<int>> res;
    vector<int> current_path;
    current_path.reserve(candidates.size());
    res.reserve(candidates.size());

    dfs(candidates, 0, target, current_path, res);

    for (auto i = 1; i < candidates.size(); ++i)
    {
        if (candidates[i] > candidates[i - 1])
        {
            // if we start with the same value, we might get a duplicate combination
            // we start with each value once and only once
            // this applies also to sub combinations within the start point
            // if we continue with the sequenc, it is only within the recursion.
            dfs(candidates, i, target, current_path, res);
        }
    }
    return res;
}
```

#dfs
