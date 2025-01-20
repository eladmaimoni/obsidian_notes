Repetitions: ||||
https://www.geeksforgeeks.org/problems/minimum-number-of-jumps-1587115620/1?page=1&category=Arrays&difficulty=Medium&sortBy=submissions

 https://www.interviewbit.com/blog/minimum-number-of-jumps/
https://leetcode.com/problems/jump-game-ii/
 
 ### $O(n^2)$ Solution
  - for each target index, we go back and calculate the minimum possible jumps to reach it
  - with each target, we go back and check all possible starting points

```
int min_jumps_to_reach_target[n];
min_jumps_to_reach_target[0] = 0;

for (auto target_index = 1; target_index < n; ++target_index)
{
	// outer loop calculates the min possible jumps to each target index
	auto min_jumps_to_reach_target = INT_MAX;
	for (auto start_index = 0; start_index < end_index; ++start_index)
	{
		auto distance = target_index - start_index;
		auto reach = arr[start_index];
		if (reach > distance)
		{
			// we can reach target from start
			// check if it results in a better number of jumps
			auto min_jumps_to_reach_start = min_jumps_to_reach_i[start_index];
			auto  = min_jumps_to_reach_start + 1;
			
			if (jumps_to_reach_target < min_jumps_to_reach_target)
			{
				min_jumps_to_reach_target = jumps_to_reach_target;
			}
		}
		
	}
	min_jumps_to_reach_target[target_index] = min_jumps_to_reach_target;
}
```

### $O(n)$ Solution
  - Once you finalized your **decision** to jump to/from cell i, you need to decide where to jump next. 
  - Where do you choose to jump to in the range `i + [1, arr[i]]? 
	  - The cell which will take you the farthest
	  - This is the best decision from what you **can** do
  - When you must **finalize** your decision?
	  - When you depleted the leftover range from last jump location (decision)
  -  Your first decision is the first cell i = 0. 

```

int jumps = 1;
int max_reach = arr[0];
int leftover_range_from_last_jump = max_reach;

if (n == 1)
{
    return 0;
}

if (max_reach >= (n - 1))
{
	return jumps;
}



for (auto i = 1; i < n; ++i)
{
	--leftover_range_from_last_jump;
	if (leftover_range_from_last_jump < 0)
	{
		return -1; // we can't reach further
	}
	//assert(leftover_range_from_last_jump > 0); // loop invariant
	
	auto possible_reach_if_we_jump_to_i = i + arr[i];

	if (possible_reach_if_we_jump_to_i > max_reach)
	{
		// this may be a better jump location
		max_reach = possible_reach_if_we_jump_to_i;
	}

	if (max_reach >= (n - 1))
	{
		// we can reach the end with one more jump
		++jumps;
		break;
	}
	
	if (leftover_range_from_last_jump == 0)
	{
		// we must now finalize our decision of which cell to jump 
		// from/to
		// it is where we got our max reach
		++jumps; 
		leftover_range_from_last_jump = max_reach - i;
	}
}

return jumps;
```

### Why do we always want to jump to the cell which will give us the max reach?

#greedy 
