1. Better write ugly yet simple `if` statements, then simplify them
   - much easier to reason about - "what happens when this happens"
   - much easier to keep certain **invariants** along a loop (such as start < end)
2. Consider initializing the result from the first element 
   - Easier for 2 pointers style
3. Try to keep invariants along a loop such as start < end
4. When looking at a recursion rule, look forward as well as backward
   - How to deduce i based on `i-1`: `[0, .... i-1], i`
   - How to deduce i based on i + 1
1. Corner cases: 0 elements / inputs
2. Corner cases: all elements are the same
3. We reached the end of the array

Thought Process Keywords
- 2 pointers - one from `end` one from `start`
- 2 pointers from start
- fixed sliding window
- sorting


Thought Process Tips
- memorize solutions multiple times - this reinforce patterns and understanding
- once you know the solution - visualize it in multiple ways
- memorize both visually and literally 
- memorize correctness

