# Array Representation
- Level k in the tree has $2^k$ elements
- Level $k$ indices are $[2^k - 1, 2^{k+1} - 1)$
	  [0], [1, 2], [3,4,5,6]

### Children Access
- Index `i` can be written as:
  $i = 2^k -1 + h$ 
  $h$ - the 0 based index within the tree level
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
