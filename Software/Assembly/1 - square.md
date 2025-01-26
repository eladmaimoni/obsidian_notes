```
int square(int num) {
    return num * num;
}
```

```
square(int):
        push    rbp
        mov     rbp, rsp
        mov     dword ptr [rbp - 4], edi
        mov     eax, dword ptr [rbp - 4]
        imul    eax, dword ptr [rbp - 4]
        pop     rbp
        ret
```


1. `push rbp` - saving the frame pointer (`rbp`) on the stack for later restore.
2. `mov rbp, rsp` - setting the frame pointer the the current top of stack
3. `mov dword ptr [rbp - 4], edi` - write the content of `edi` into the current stack frame
   note that this memory is NOT allocated explicitly by decrementing the stack pointer (`esp`). 
   since the compiler sees that this function returns without allocating additional memory (or calling another function), it can skip the allocation, knowing that `rsp` won't be used again before this function returns.
4. dfgh
5. dfg
6. dfg
7. dfh
8. dfh
9. dfh
10. dfh
11. dfh

![[square_stack_memory|800]]



