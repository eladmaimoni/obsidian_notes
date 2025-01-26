`push <register>` :
allocate place on the stack for the specified register, and writes the register content into the new allocated space.

1. **Decrement the stack pointer** (`rsp`) by 8 bytes.
2. Store the content of the 64 bit `<register>` to the newly allocted place.
   
so it is essentially:

```
rsp -= 8; // Reserve space for 8 bytes on the stack
*(uint64_t*)rsp = <register> // Store the 64-bit register value at the new top of stack
``` 


### Examples:

1. `push rbp`
   
2. 
3. dfg
4. dfg
5. fdg