https://www.geeksforgeeks.org/heap-data-structure/?ref=lbp

### Single node Heapify
1. Compare parent to both children
2. Swap parent with the largest child
### Insert $O(\log{n})$ 
1. Add to the end of the tree / array
2. Recursively heapify upward until no swap is needed
### Remove $O(\log{n})$ 
1. Swap with the last element and remove
2. Start with the swapped element, recursively heapify downwards until no swap is necessary
### Heapify - transform an array / tree to a heap $O(n)$
Iterate each tree layer from bottom to top, heappifying each node.
- starting with the first index of the lowest layer
# API
```
// max heap
std::priority_queue<int> max_heap;

// min heap
std::priority_queue<int std::vector<int>, std::greater<int>>
        min_heap(data.begin(), data.end());

// access top
max_heap.top();

// add element
max_heap.push(123);

// remove top
max_heap.pop();

// no easy way to remove from the middle
```
