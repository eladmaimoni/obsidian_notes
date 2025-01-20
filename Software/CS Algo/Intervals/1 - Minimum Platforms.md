https://www.geeksforgeeks.org/problems/minimum-platforms-1587115620/1?page=1&category=Arrays&difficulty=Medium&sortBy=submissions



Repetitions: |||
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


```
    struct Event
    {
        bool is_arrival = false;
        int hour = 0;
    };
    
    int findPlatform(vector<int>& arr, vector<int>& dep) 
    {
        int n = arr.size();
        
        std::vector<Event> events(2 * n);
        
        for (auto i = 0; i < n; ++i)
        {
            events[i] = Event{true, arr[i]};
        }
        for (auto i = 0; i < n; ++i)
        {
            events[i + n] = Event{false, dep[i]};
        }
        
        sort(events.begin(), events.end(), [](const Event& e1, const Event& e2)
            {
                if (e1.hour == e2.hour && e1.is_arrival != e2.is_arrival)
                {
                    return e1.is_arrival; // arrival first
                }
                else
                {
                    return e1.hour < e2.hour;
                }
            }
        );
        
        // now count the maximum amount of concurrent arrivals we have
        
        
      int max_arrivals = 1;
      int current_arrivals = 1;
      int last_arrival = events[0].hour;
      for (auto i = 1; i < 2 *n; ++i)
      {
          auto event = events[i];
          
          if (event.is_arrival)
          {
              last_arrival = event.hour; 
              ++current_arrivals;
              
              if (current_arrivals > max_arrivals)
              {
                  max_arrivals = current_arrivals;
              }
        
          }
          else
          {
              // if departure is later than last arrival, we can simply  reduce the current arrivals
               --current_arrivals;
          }
      }
        
        return max_arrivals;
        // Your code here
    }
```

#intervals