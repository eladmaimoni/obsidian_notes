1. Better write ugly yet simple `if` statements, then simplify them
   - much easier to reason about - "what happens when this happens"
   - much easier to keep certain **invariants** along a loop (such as start < end)
2. Consider initializing the result from the first element 
   - Easier for 2 pointers style
3. Try to keep invariants along a loop such as start < end
4. Corner cases: 0 elements / inputs
5. Corner cases: all elements are the same
6. We reached the end of the array