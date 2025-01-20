- [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
- Trick: the first array contains extra space to accommodate for the second array elements
- instead of going from small to large with 2 pointers, we start from the ends and go backwards

```
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    
    auto e1 = m - 1; // always point to the smallest in nums1 that haven't been assigned
    auto e2 = n - 1;  // always point to the smallest in nums2 that haven't been assigned

    auto e = m + n - 1;

    while (e1 >= 0 && e2 >= 0)
    {
        if (nums1[e1] >= nums2[e2])
        {
            nums1[e] = nums1[e1];
            --e1;
        }
        else
        {
            nums1[e] = nums2[e2];
            --e2;
        }
        --e;
    }

    while (e2 >= 0)
    {
         nums1[e] = nums2[e2];
        --e2;
        --e;
    }
}
```