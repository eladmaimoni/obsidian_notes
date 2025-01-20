
- [Job Sequencing Problem](https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1?page=3&difficulty=Medium&sortBy=submissions) 
### My Thinking

1. Sort the array so that late deadlines appear first, if the deadline is the same have the better profit first.
2. start with `t = latest_deadline` this is the first element in the sorted array and the latest deadline we have
3. keep a variable `i` to point to the job
4. whenever we have `t` time left, it is best to choose the most profitable element that first the deadline
5. 

### $O(n^2)$ time with $O(n)$ space
- sort by profit
- find the latest time slot available to perform the job 
```
    vector<int> JobScheduling(Job jobs[], int n) 
    {
        std::sort(jobs, jobs + n, 
            [](const Job& j1, const Job& j2)
            {
                if (j1.profit != j2.profit)
                {
                    return j1.profit > j2.profit;
                }
                else
                {
                    return j1.deadline > j2.deadline;
                }
            }
        );
        
        int max_t = 0;
        
        for (auto i = 0; i < n; ++i)
        {
            auto deadline = jobs[i].deadline;
            if (deadline > max_t)
            {
                max_t = deadline;
            }
        }
        
        std::vector<unsigned char> time_taken(max_t + 1, 0);

        int total_profit = 0;
        int total_jobs = 0;
        for (auto i = 0; i < n; ++i)
        {
            auto deadline = jobs[i].deadline;
            auto profit = jobs[i].profit;
            
            // find the latest deadline possible
            // suitable t is [1, deadline]
            for (auto t = deadline; t >= 1; --t)
            {
                if (time_taken[t] == 0)
                {
                    time_taken[t] = 1;
                    total_profit += profit;
                    total_jobs += 1;
                    break;
                    
                }
            }
            
        }

        return {total_jobs, total_profit};
        
    }
```

### Using Disjoint Set

```
  int find(vector<int>& parent, int x) {
    if (parent[x] == x) {
        return x;
    }
    return parent[x] = find(parent, parent[x]);
    }
    // Function to find the maximum profit and the number of jobs done.
    vector<int> JobScheduling(Job jobs[], int n) 
    {
        std::sort(jobs, jobs + n, 
            [](const Job& j1, const Job& j2)
            {
                if (j1.profit != j2.profit)
                {
                    return j1.profit > j2.profit;
                }
                else
                {
                    return j1.deadline > j2.deadline;
                }
            }
        );
        
        int max_t = 0;
        
        for (auto i = 0; i < n; ++i)
        {
            auto deadline = jobs[i].deadline;
            if (deadline > max_t)
            {
                max_t = deadline;
            }
        }
        

        int total_profit = 0;
        int total_jobs = 0;
        
        // for each profit, we would like to find the latest possible time slot available
        // to schedule it.
        // for that, we maintain a tree structure
        // each deadline will point to the latest available time slot (initially it is the
        // deadline itself)
        
        std::vector<int> latest_slot_available(max_t + 1, 0);
        
        for (auto i = 1; i <= max_t; ++i)
        {
            latest_slot_available[i] = i;
        }
        
        for (auto i = 0; i < n; ++i)
        {
            auto deadline = jobs[i].deadline;
            auto profit = jobs[i].profit;   
            auto available_slot = find(latest_slot_available, deadline);
            
            if (available_slot > 0)
            {
	            // union this slot with the result of the previous one
                latest_slot_available[available_slot] = find(latest_slot_available, available_slot - 1);
                total_profit += profit;
                total_jobs += 1;
            }
        }

        return {total_jobs, total_profit};
        
    }
```


#greedy #union-find

