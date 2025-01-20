https://leetcode.com/problems/longest-consecutive-sequence/description/

```
int longestConsecutive(vector<int>& nums) 
{
    // longest consecutive sequence

    unordered_set<int> existing;
    existing.insert(nums.begin(), nums.end());

    auto max_consecutive = 0;
    for (auto num : nums)
    {
        auto prev_num = num - 1;

        // only start from numbers that do not contain previous value
        if (existing.find(prev_num) == existing.end())
        {
            auto next = num + 1;
            while (existing.find(next) != existing.end())
            {
                ++next;
            }

            auto consecutive = next - num;

            if (consecutive > max_consecutive)
            {
                max_consecutive = consecutive;
            }
        }
    }
    return max_consecutive;
}
```

Trick: 
- I had the idea of using unoredered_set.
- however the trick to looking for continuous subsets it too start sequence examination only from elements that do not have a previous element. there can be at most N like those and it avoids more than O(N) total lookups (2N at most if there is no sequence longer than 1)