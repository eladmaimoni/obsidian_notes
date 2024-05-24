Given an array arr[] of size N and an integer K. Find the maximum for each and every contiguous subarray of size K.
https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/?ref=lbp
### Why can't we do $O(1)$ memory?
- think of array 9 8 7 0  0 1 and K = 4
- if we do a sliding window, remembering only the maximal element of the window, then once we remove 9, and add 0, we 'forget' the second max element in the window (8).
- the same principle also fails us if we also remember the second largest element.

### $O(n \log{n})$ time using max heap
- Keep a max heap 
- use a sliding window of size K
- Each iteration - ensure the top element is always within the sliding window
	- remove the top element as long as its index is outside the window (logarithmic)
	- add the new element to the heap
- Note that the heap may **grow to size n** if the elements are always increasing \[1 2 3 4] 5 6 7 8 9 10 11 12 - the top of the heap is never outside the window
- We can't limit the heap to size k since then we will have to remove the element that leaves the window - searching it in the queue is linear which will lead to $O(nk)$ time.



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
- each time we slide the window, 2 of the K elements change
- one is added from the right and one is removed from the left
- which of the k elements may affect the maximum?
	- once you have a larger number to your right, it will last longer and make you redundant (because you will always be smaller)
	- so only numbers that have no larger elements to their right
- \[5 1 **9** 4\] 1 0 6
- \[**13 12 11 10** \] 9 8 7 6 5 4 3 2 1 
- \[**13 12 11 10** \] 14 15 16 17 18
- \[**19 12 11 10** \] 14 15 16 17 18
So the loop invariant is:
- the queue holds elements whose elements to the left are larger
Each time we add an element to the queue:
- we remove the first element - O(1)
- we remove all elements on the right that are smaller than the new element O(k)?
- we add the new element - O(1)
- the second step might be O(k) in the worst case but it adds up to n steps at most. once an element is removed, it is no longer added. and there are only n elements.


Algorithm:
1. keep a queue sized K that hold up to k elements that may affect the maximum - $O(k)$ space
4. Move with a sliding window - $O(n)$ time
5. each time we move the sliding window:
   - add a new element to the queue
   - if the added element is larger than the right of the queue
   - if the new element is 
   - go over the queue right to left - $O(k)$
   - remove elements that are smaller than the current maximum in the queue

```
    vector <int> max_of_subarrays(int *arr, int n, int k)
    {
        deque<pair<int,int>> k_candidates;
        std::vector<int> result;
       
  
        for (auto i = 0; i < k; ++i)
        {
            auto val = arr[i];
            
            while (!k_candidates.empty() && val >= k_candidates.back().first)
            {
                k_candidates.pop_back();
            }
            
            k_candidates.push_back({val, i});
        }
        
        result.push_back(k_candidates.front().first);
   
        for (auto i = k; i < n; ++i)
        {
            auto val = arr[i];
            
            
            // invariant 1: make sure the queue only holds elements from the current window
            if (!k_candidates.empty() && k_candidates.front().second <= (i - k))
            {
                k_candidates.pop_front();
            }

            // invariant 2: make sure all elements int the queue are always larger then their right
            while (!k_candidates.empty() && val >= k_candidates.back().first)
            {
                k_candidates.pop_back();
            }
           
            // insert the new element, it is larger then all elements to the right of it
            k_candidates.push_back({val, i}); 
            
            result.push_back(k_candidates.front().first);
        }
    
        return result;       

    }
```

#cs #priority_queue #sliding_window #red_black_tree
