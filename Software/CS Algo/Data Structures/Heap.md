https://www.geeksforgeeks.org/heap-data-structure/?ref=lbp


- a [[Binary Tree]] structure
- level $i$ has at most $2^i$ elements and exactly that if it is full
- the tree can be represented in a vector:

| 0     | 1     | 2     | 3     | 4     | 5     | 6     | ..  |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | --- |
| $a_0$ | $b_0$ | $b_1$ | $c_0$ | $c_1$ | $c_2$ | $c_3$ | ..  |

### Heap rule:
- Max Heap: Parent $\geq$ Children
- Min Heap: Parent $\leq$ Children
### Single node Heapify
1. Compare parent to both children
2. Swap parent with the largest child
```
voif heapify(int childIdx)
{
	int parent_idx = (i - 1) / 2;

	if (a[parent_idx] < a[child_idx])
	{
		// parent is smaller, we assume that the parent is larger than the other child
		swap(a[parent_idx], a[child_idx]);
	}
	
}
```
### Insert $O(\log{n})$ 
1. Add to the end of the tree / array
2. heapify **upward** until no swap is needed

```
std::vector<int> max_heap;

// insert
auto child_idx = max_heap.size();
max_heap.push_back(val);

while(child_idx > 0)
{
	auto parent_idx = (child_idx - 1) / 2;
	// check if child is larger than parant
		if (max_heap[parent_idx] < max_heap[child_idx])
	{
		// parent is smaller, we assume that the parent is larger than the other child
		swap(max_heap[parent_idx], max_heap[child_idx]);
		child_idx = parent_idx;
	}
	else
	{
		// heap is fine!
		break; 
	}

}

```

Some nice optimization - reducing the number of assignment when we notice that max_heap at child_index always has the same value

```
std::vector<int> max_heap;

// insert
auto child_idx = max_heap.size();
max_heap.push_back(val);

while(child_idx > 0)
{
	auto parent_idx = (child_idx - 1) / 2;
	// check if child is larger than parant
		if (max_heap[parent_idx] < value)
	{
		// parent is smaller, we assume that the parent is larger than the other child
		max_heap[child_idx] = max_heap[parent_idx];
		child_idx = parent_idx;
	}
	else
	{
		// heap is fine!
		break; 
	}

}
max_heap[child_idx] = val;
```
### Remove $O(\log{n})$ 
1. Swap with the last element and remove
2. Start with the swapped element, heapify **downwards** until no swap is necessary
### Heapify - transform an array / tree to a heap $O(n)$
Iterate each tree layer from bottom to top, heappifying each node.
- starting with the first index of the lowest layer
# C++ API

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
