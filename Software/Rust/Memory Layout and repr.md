


### Links
- [type layout](https://doc.rust-lang.org/reference/type-layout.html)
- [SO - memory layout differences](https://stackoverflow.com/questions/79631106/whats-the-difference-between-reprrust-reprc-and-reprpacked)
### `repr(Rust)`
- compiler can reorder fields to minimize padding / space
- compiler can save space when representing enums - it can decide to describe which variant using the variants values (instead of a dedicated "index").
```
#[repr(Rust)]
struct Record{
    a : i32,
    b : f32,
}
```
### `repr(C)`

### `repr(packed)`
- uses the smallest amount of memory possible, even at the cost of having fields misaligned (their addresses are not aligned to their size)
- removes padding
- allows storing more copies per memory space
- can generally necessitate more instructions in order to read / write the struct fields (my assumption)

### `repr(align)`
- allows to increase the alignment of a type ("round up")
- can be combined with `repr(Rust)` OR `repr(C)`
  
The example on SO question mentions a case where an existing struct has a size of a cache line (64 bytes). by default, it may be allocated in addresses that are not aligned to 64 bytes. 
so by forcing an alignment of 64 bytes, we make sure that the entire structure is always contained withing a cache line.
A type being 64 bytes in size does not mean it’s aligned to 64 bytes. By default, a 64-byte struct will typically have alignment equal to the largest alignment of its fields (often 1, 4, 8, or 16)

Why that can help performance:

- Cache-line fit: Many CPUs use 64-byte cache lines. If your 64-byte struct isn’t 64-byte aligned, it may straddle two cache lines, causing extra cache traffic and wasted cache capacity.
- Predictable SIMD/atomic access: Some operations perform best (or are required) on aligned data.
- Reduced false sharing: If each 64-byte object starts on a cache-line boundary and is ≤ 64 bytes, adjacent objects won’t share a cache line.