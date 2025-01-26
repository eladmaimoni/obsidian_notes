- `rsp` - stack **pointer**. 
  The 64 bit address of the top of the stack.
  When a thread starts, it is allocated a fixed amount of memory for its stack variables. The `rsp` register will be initialized to the highest memory address in the stack and decrement as we go.
  When the program needs extra space on the stack, it will typically decrement this pointer by a certain amount.
- `rbp` - base pointer (AKA frame pointer)
  this register typically points to the start of the stack within the current function.
  This allows the program to allocate new stack variables by decrementing `rsp` by a fixed amount, while referencing the allocated memory relative to the non-changing `rbp`. 
  
  Typically, a function sets `rbp = rsp` at the start (the prologue), and then uses fixed offsets from `RBP` (like `rbp - 4`) to access local data. When the function ends, `RBP` is restored (the epilogue).
- 
- dfgdf
- dfg
- dfg
- dfg
- dfg
- dfg
- gfd
- fgd
- gdf
- gfd