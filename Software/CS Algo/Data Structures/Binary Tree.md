- Assuming $k$ levels (zero based): 0, 1, 2
- Level $k$ in the tree has $2^k$ elements: 1, 2, 4, 8, 16, 32
- Total elements (according to geometric progression)
  $n = 2^{k + 1} - 1$
## Array Representation
- 
### Children Access using parent index
Intuition:
- each level has $2^k$ elements
- within the level, we have index  $h \in [0, 2^k)$
- next level has $2h$ elements - 2 elements for each element in previous level
- therefore the index is the beginning of the next level plus $2h$
Calculation
- Level $k$ indices start at $2^k - 1$ (deduce $2^k$ from the total number of elements)
- Index `i`  at level $k$ can be written as:
  $i = 2^k -1 + h$ 0
  $h \in [0, 2^k)$ - the 0 based index within the tree level 
- Left child
  $2^{k-1} - 1 + 2h = 2i + 1$
  (start of the next level, plus double the offset since each node has 2 children)
- Right Child
  $2i + 2$

### Parent Access
- Index `i` can be written as:
  $i = 2^k -1 + h$ 
- Parent:
  $2^{k-1} -1 + \frac{h}{2} = \frac{i-1}{2}$
  (start at previous level, go half the length in that level since there are half the elements)
