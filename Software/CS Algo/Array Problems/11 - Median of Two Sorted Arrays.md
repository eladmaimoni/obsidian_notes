- [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

### Median
in a sorted array of length n:
- if `n` is *odd*: the median index is `n/2` (for example 2 in case n = 5)
- if `n` is even the median index is undefined and so we take the average between `a[n / 2]` and `a[n/2 - 1]`
### $O(n+m)$ global index using 2 pointers
- this assumes `n` is odd
- if `n` is even, we need to maintain the previous median and average the result
```
p1 = 0
p2 = 0

global_median_index = n / 2

// find the global index of the median
int median;
int prev_median;
while ((p1 + p2) < global_median_index)
{
	prev_median = median
	if (p1 < m && p2 < n)
	{
		if (a[p1] < b[p2])
		{
			++p1
			median = a[p1];
		}
		else
		{
			++p2;
			median = a[p2];
		}
	}
	else if (p1 < m)
	{
		++p1;
		median = a[p1];
	}
	else
	{
		++p2;
		median = a[p2];
	}
}
return (n%2) ? (median + prev_median) / 2 : median;
```

#median #binary-search #arrays #2-pointers