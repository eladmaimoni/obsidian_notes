
### 2 Pointers approach - Does not work
- Create A sorted array of segments, sorted by start time and then end time
- Keep a counter for the platforms, initialize to 1
- Keep 2 pointers - start and end
  - as long as the current end overlaps the start - advance start, increment counter
  - when there is no overlap, advance end, decrement counter - **THIS is the FAILURE POINT**
    
```
here it works
0 ------------
1  -------------
2   --------------
3                   ------------

but here is does not
0 ---------------------
1  -----
2         ------ 
3                         ----------
```
when we are done with the `segment[0]`'s  `end`, we lost the counter for the second `segment[1]`, our `start` is already at segment 3 and there is no real way to know the counter for `segment[1]`.

### Sorting by event type
- keep a unified array of events sorted by time
- each time we encounter an arrival - increment counter
- each time we encounter a departure - decrement counter

```
counter = 0;
max_counter = 0;
for (auto e : events)
{
	if (e.is_arrival)
	{
		++counter;
		max_counter = max(counter, max_counter);
	}
	else
	{
		--counter;
	}
}
```