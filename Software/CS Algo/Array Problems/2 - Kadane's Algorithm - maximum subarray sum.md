Repetitions: |||

https://www.geeksforgeeks.org/problems/kadanes-algorithm-1587115620/1?page=1&category=Arrays&difficulty=Medium&sortBy=submissions



```
long long max_sum_that_ends_with_i = arr[0];
long long max_subarray_sum = max_sum_that_ends_with_i;

for (auto i = 1; i < n; ++i)
{
	// the largest sum that ends with i 
	// the largest sum up until i - 1 can either
	// 1. help me (if its positive) get a better overall sum that ends in i
	// 2. make it worse for me - I prefer to start over using the number I am at
	long long arr_i = arr[i];
	if (max_sum_that_ends_with_i < 0)
	{
		max_sum_that_ends_with_i = arr_i;
	}
	else
	{
		max_sum_that_ends_with_i += arr_i;
	}

	max_subarray_sum = max(max_subarray_sum, max_sum_that_ends_with_i);
}

return max_subarray_sum;
```

Insights:
If we are in position i, the best sum that ends at position i - 1 can either:
1. help me get a better sum (if it is positive)
2. make it worse for me (if it is negative), and hence we might prefer starting over

We sum each element, if the sum becomes negative, then it is better to discard it and start over since this continuous part only worsen things