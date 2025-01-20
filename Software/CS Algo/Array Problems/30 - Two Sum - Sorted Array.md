- [167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)


Given an array, find 2 elements that amounts to target sum
- non sorted variation uses a hash table too lookup `target - a[i]`
- assuming a sorted array, we can find this at $O(n)$ with $O(1)$ space

### $O(n)$ solution
- keep 2 indices (pointers) - `left` and `right` and calculate `v = a[left] + a[right]`
- if `v < target` increment left
- if `v > target` decrement right
### Why is this correct?
Could it be that we 'miss' a possible combination like that?
- I think it is best to think in an 'induction style' proof
- assume we have elements [0.... n-1]
- Iteration 0:
  if we are at `a[left = 0]` and our sum is too small. then the only thing we can do is increment `left`. 
  every other combination of right will only make the sum smaller. so there is no possible pair with the current `left` in the array. so we must check left = 1 and process the subarray [1... n-1]
- every other iteration will follow the same logic only on a sub array.
- 