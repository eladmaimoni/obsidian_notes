https://leetcode.com/problems/find-the-duplicate-number/description/

- like detecting cycle in a linked list and finding the junction

```
    int findDuplicate(vector<int>& nums)
    {
        int slow = nums[0];
        int fast = nums[0];

        // Find the intersection point of the two pointers
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);
        
        // Find the entrance of the cycle
        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return slow;
    }
```


- the indices are in range `[0, n]` (there are n + 1 elements with one duplicate)
- the values are `[1, n]`
### Insights
- if we treat the values as indices, we can't reach index 0
- if a certain entry points to itself we will be stuck there. 
- if we are stuck there, it means we reached there, and that must be a duplicate

#pigoen-hole

- Think of indices as nodes
- the node `i = 0` points to a node in range `[1, n]`
- No one points to `i = 0`
- each of the nodes `[1 , n]` must point to `[1, n]`, so one node has 2 edges coming in.
- to view this visually
- 2 indices must point to the same value (next index)
- if `index == value` then this is the cycle
- if not then some other 