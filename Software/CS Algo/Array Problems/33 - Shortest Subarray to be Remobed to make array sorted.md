 
- [1574. Shortest Subarray to be Removed to Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)


### 2 pointers insight
- a lot of times our intuition says 'two pointers' but it seems like putting then 2 pointers where we feel like they should be isn't working.
- try putting the pointers on different ends or at a 'valid but no ideal' solution
- the goal is to start at a valid solution and to force movement for a single pointer

### 2 Pointers Problem
Given 2 sorted arrays `a[n]` and `b[m]`, find indices `i` and `j` such that the concatenation of `a[0:i]` and `b[j:]` is sorted.

Option 1:
- init a pointer at the end of `a`  and the start of `b`

```
                *
a = 1 2 2 2 2 2 3
    *            
b = 1 2 2 2 2 2 3
```
- the goal is to move b pointer rightward and `a`'s pointer leftward as little as possible until we satisfy `a[i] <= b[j]`
- the problem is that we may have 2 ways to move the pointers - both moving left and right might work by either reducing `a[i]` or increasing `b[j]`
- so the induction is not well formed

Option 2:
- init a pointer 
```
    *            
a = 1 2 2 2 2 2 3
    *            
b = 1 2 2 2 2 2 3
```
- if the condition `a[i] <= b[j]` does not hold, we MUST increase `j`
- if the condition does hold, we can try to increase `i`
- Note there is no

```
int findLengthOfShortestSubarray(vector<int>& arr) 
{
    int n = arr.size();
    int right = n - 1;

    // when done, right will point to the first element that 
    // does not satisfy the condition (decreasing)
    // if all is increasing, right will be 0
    // if all is decreasing, right will be n - 1
    while (right > 0 && arr[right - 1] <= arr[right])
    {
        --right;
    }

    auto left = 0;
    auto shortest_subsequence = right;
    while (left < right && left < n && (left == 0 || arr[left - 1] <= arr[left]))
    {
        if (right < n)
        {
            if (arr[left] <= arr[right])
            {
                // condition holds
                // we may increase left

                shortest_subsequence = min(shortest_subsequence, right - left - 1);
                ++left;
            }
            else
            {
                ++right;
            }
        }
        else
        {
            shortest_subsequence = min(shortest_subsequence, right - left - 1);
            ++left;
        }

    }


    return shortest_subsequence;
}
```