Given an array arr[] of size N and an integer K. Find the maximum for each and every contiguous subarray of size K.

### Why can't we do $O(1)$ memory?
- think of array 9 8 7 0  0 1 and K = 4
- if we do a sliding window, remembering only the maximal element of the window, then once we remove 9, and add 0, we 'forget' the second max element in the window (8).
- the same principle also fails us if we also remember the second largest element.

### Why can't we use a max heap?
- Keep a max heap of size k - O(k) space
- use a sliding window of size K
- Each iteration we remove the element that left the window from and insert the one that entered the window - O(log k)
- This WON'T WORK since removing an item is no O(log k) if we don't know exactly which index is it. 
- We only know the **value** - hence we need to search the heap which is O(k)


### $O(n \log{k})$ time using self balancing tree
- same principle of our idea with the max heap
- using a self balancing tree means we can retrieve the value at O(log k)
```
using pair_t = std::pair<int, int>;
std::vector<int> result;

// std::set does not accept duplicates, so we must use pair
std::set<pair_t, std::greater<pair_t>> last_k;

for (auto i = 0; i < k; ++i)
{
    last_k.insert({ arr[i], i });
}


result.push_back(last_k.begin()->first);


for (auto i = k; i < n; ++i)
{
    assert(last_k.size() == k);
    auto prev = arr[i - k];

    auto val = arr[i];

    auto itr = last_k.find({ prev,i - k });
    last_k.erase(itr);
    last_k.insert({ val, i });
    assert(last_k.size() == k);
    result.push_back(last_k.begin()->first);
}

return result;
```

### $O(n)$ using a deque
- examine the k-sized sliding window 
