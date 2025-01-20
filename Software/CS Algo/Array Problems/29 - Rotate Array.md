- [189. Rotate Array](https://leetcode.com/problems/rotate-array/)
- WTF

```
    void rotate(vector<int>& nums, int k)
    {
        int n = nums.size();
        if (k > n)
        {
            k = k % n;
        }
        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
```

