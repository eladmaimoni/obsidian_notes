https://leetcode.com/problems/climbing-stairs/

# Naive Thought
- the number of ways to reach $n$ equals the number of ways to reach $(n - 2)$ + 2 ways - adding 11 and 2
- why is this incorrect?
  - we might also jump from $(n - 3)$ straight to $(n-1)$ and add 1
- this does not really describe the rule, we don't "add ways" from a certain point
- if that was the case - we would need to add '1' to n - 2 since we already count one way - that is to reach n - 2

### Correct answer
The approach works because it leverages the fact that to reach the n-th stair, you can come from either the (n−1)-th stair by taking one step or from the (n−2)-th stair by taking two steps. This means:

- **Option 1**: All the ways to reach the (n−1)-th stair, followed by a single step to the n-th stair.
- **Option 2**: All the ways to reach the(n−2)-th stair, followed by a double step to the n-th stair.

These two sets of paths are **mutually exclusive** because they end differently—one with a single step and the other with a double step. Therefore, there's **no overlap or double-counting** when you sum the number of ways from both options.