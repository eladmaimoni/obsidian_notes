- https://www.enjoyalgorithms.com/blog/find-the-maximum-j-i-in-array
- Find the largest index difference (positive) that yields a positive value difference
- `i < j && a[j] <= a[i]`

### Smart Brute Force
- we take advantage of the fact that we want to find the maximal index difference
- so we can start iterating from the right and stop on the first element that satisfies this
```
for (auto i = 0; i < n; ++i) // left to right
{
	for (auto j = n - 1; j >= 0; --j) // right to left
	{
		if (a[j] >= a[i])
		{
			// if we found this pair, this is the best we can do with
			// this 'i'
			max_diff = max(max_diff, j - i);
			break;
		}
		
	}
}
```

Observation:
- for each i, we are searching from the right to see if the condition holds
- if for each index, we were to know what is the **maximal value up to that index is**, we could solve this immediately:

```
struct ValueIdx 
{
 int value;
 int idx;
} 

std::vector<ValueIdx> max_value_up_to_idx(n);

auto max_val_idx = 0;
auto max_val = INT_MIN;
for (auto i = 0; i < n; ++i)
{
	if (a[i] > max_val)
	{
		max_val = a[i];
		max_val_idx = i;
	}
	max_value_up_to_idx[i] = {max_val, max_val_idx};
}
```

And now the second loop can be skipped:

```
for (auto i = 0; i < n; ++i) // left to right
{
	if (max_val >= a[i])
	{
		
	}
	for (auto j = n - 1; j >= 0; --j) // right to left
	{
		if (a[j] >= a[i])
		{
			// if we found this pair, this is the best we can do with
			// this 'i'
			max_diff = max(max_diff, j - i);
			break;
		}
		
	}
}
```