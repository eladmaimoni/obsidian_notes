
[CppCon 2014: Chandler Carruth "Efficiency with Algorithms, Performance with Data Structures"](https://www.youtube.com/watch?v=fHNmRkzxHWs)

Efficiency - Better Algorithms - Reduce Amount of Work
Performance - Use better data structures for the algorithm (contiguous is the best)

Key Sentences
- Discontinuous Data Structures Are The Root of All Performance Evil

Lessons 1 - unoredered_map:
- a lot of times you need to insert a value to an unordered map if it does not exist.
- you want to avoid computing the hash more than once
- you want to avoid looking up the value (accessing it) more than once

```
auto val = cache[key]; // compute hash & access the map once, default constructing once

if (!val)
{
	val = ...
}

return val;
```

- if we had a way to get to the entry inside the unordered_map without creating a default value (which might be expensive) it would be gread
- note that if we use `find` and or `contains` we are still query the map twice if the element is not found - so this is a trade off - construction complexity vs. accessing twice in case element not found

Lesson 2: vector as queue
- if we wish to push things to the end and pop them from the front - we need a queue (FIFO)
- if we have a bound on the total number of inserts, we can still use a vector. popping means incrementing the start index
- great for bfs! we know how many nodes we have at most
- indices, unlike iterators - can't be invalidated