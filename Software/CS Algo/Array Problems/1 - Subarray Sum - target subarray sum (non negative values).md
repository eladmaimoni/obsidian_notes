Repetitions: |||
https://www.geeksforgeeks.org/problems/subarray-with-given-sum-1587115621/1?page=1&category=Arrays&sortBy=submissions

given array of non negative numbers, find a contiguous subarray that adds to the target sum $S$


Solution In words:
- use '2 pointers' method to the start and end of the array
- invariant: always make sure start < end
- if the sum is too small - try increasing the sum by incrementing end (if possible)
- if the sum is too large - try decreasing the sum by incrementing start (if possible)

Insights:
- Inclusive accumulative sum can give us a subarray sum with $O(1)$ complexity on the fly
- The subarray sum is always non decreasing, once it passes the target sum we can only decrease the sum by incrementing the start index.
- When we increment `start`, could it be that we 'skipped' a possible solution?
  No, if there is a possible solution with a previous `end`, the subarray sum would have surpass the target earlier, forcing us to increment `i`

```
vector<int> subarraySum(vector<int>arr, int n, long long s)
{
	int start = 0;
	int end = 1;
	long long partial_sum = arr[0];

	while (partial_sum != s)
	{
		// we keep the loop invariant that start < end
		if (partial_sum < s)
		{
			if (end < n)
			{
				// we can increase the sum
				partial_sum += arr[end];
				++end;
			}
			else 
			{
				// we can't increase the sum, return -1
				break;
			}
		}
		else // partial_sum > s
		{
			if (start < (end - 1))
			{
				// we can decrease the sum while maintaining start < end
				partial_sum -= arr[start];
				++start;
			}
			else if (end < n)
			{
				// if we increase start, we will have start == end
				// so we increase both
				partial_sum -= arr[start];
				partial_sum += arr[end];
				++start;
				++end;
			}
			else
			{
				// we can't increase start / shift both
				// this happens when end reaches n and starts is the last element
				break;
			}
		}
	}
	if (partial_sum == s)
	{
		// we increase start, since it requires non zero indices
		return {start + 1, end};
	}
	else
	{
		return {-1};
	}
}
```

### Subtleties
- Note that even though `end` may reach the end of the array, we are still not done. We may need to still reach the end of the array.