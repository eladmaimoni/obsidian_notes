https://leetcode.com/problems/next-permutation/solutions/5979363/2-method-c-beginner-friendly-beat-100/?envType=problem-list-v2&envId=array

```
void nextPermutation(vector<int>& nums) 
{
    int n = nums.size();

    auto prev_val = nums[n - 1];
    auto min_from_right = prev_val;

    auto i = n - 2;

    while(i >= 0 && nums[i] >= nums[i + 1])
    {
        --i;
    }
    // i is now pointing one idx pass the increasing suffix

    if (i >= 0)
    {
        // in the increasing suffix, we need to find the smallest element that is larger the i
        // the suffix is increasing
        auto j = n - 1;
        while (nums[j] <= nums[i])
        {
            --j;
        }
        swap(nums[j], nums[i]);
    }

    reverse(nums.begin() + i + 1, nums.end());
}
```