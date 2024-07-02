return the $x^{th}$ largest (or smallest) number in a sliding window sized K


### Easier - $x^{th}$ largest among all numbers - $O(n \log x)$
- Maintain a min heap of the the x largest elements 
- When adding a number:
  - if it is smaller them the top, ignore
  - if it is larger then or equal to the top - pop and push to the heap
- when done, the heap top is the $x^{th}$ largest element

### Sliding window $O(n \log {(max(x, n - x))}$
- like the sliding window median, we maintain 2 heaps:
  - min heap of the x largest element - the top is always the answer
  - max heap of the smaller numbers
  - both heaps contain the indices as well
- when a sliding window is shifted
  - remove the oldest value from the 2 heap structure - **expensive if we actually do this**
  - add the new value to the 2 heap structure
  - balance the heaps
- How do you remove the oldest number?
  - we can defer the removal of older elements to the time they are at the top of the heap
  - we will have to track heap sizes **manually**
  - the elements that should have been removed are counted

### What about a data stream?
- here we can't lazily remove data from the heaps - they can grow indefinitely
- we need to use self balancing tree
- the median is effectively the root of the tree in case it is balanced
- TODO - complete this