Repetitions: ||
Given an array of size **N** containing only 0s, 1s, and 2s; sort the array in ascending order.

https://www.geeksforgeeks.org/problems/sort-an-array-of-0s-1s-and-2s4231/1?page=1&category=Arrays&difficulty=Medium&sortBy=submissions
### Naive $O(n)$ - 2 passes

```
int zeros = 0;
int ones = 0;
int twos = 0;

for (auto i = 0; i < n; ++i)
{
	auto val = a[i];
	if (val == 0)
	{
		a[zeros++] = 0;
	}
	else if (val == 1)
	{
		++ones;
	}
	else
	{
		++twos;
	}
}

while (ones > 0)
{
	a[zeros++] = 1;
	--ones;
}

while (twos > 0)
{
	a[zeros++] = 2;
	--twos;
}

```

### Better $O(n)$ - 1 pass based on the *partition* algortithm
- we keep 2 pointers - start and end
- `start` marks the end of the zeros section
- `end`  marks the start of the twos section
- we move left to right
- we push zeros to the left section
- we push twos to the right section
- when we meet one, we skip it, once we meet a zero, we will fill it

```
// zeros should be on the left
// twos on the right
// ones in between them
int zeros_end = 0;
int twos_start = n - 1;
int i = 0;

while (i < right)
{
	auto val = a[i];
	if (val == 0)
	{
		// value should be on the left
		std::swap(a[zeros_end], a[i]);
		++zeros_end;
		++i;
	}
	else if (val == 2)
	{
		std::swap(a[twos_start], a[i]);
		--twos_start;
	}
	else
	{
		++i;
	}
}
```

### Partition Algorithm
- this can help understanding the principle of the previous
- in this case the 'pivot' is 0
- In words: 
	- swap all `a[i]<= pivot` to the left and move both `left` and `i`
	- for `a[i] > pivot` only advance `i`. this is a placeholder for future possible swap


```
auto left = 0;
auto i = 0;
while (i < n)
{
	auto val = a[i];
	if (val == 0)
	{
		// we push a zero the left, i advances too
		std::swap(a[left], a[i]);
		++left;
		++i;
	}
	else
	{
		// we skip this, but don't push the left wall, if we encounter a 
		// zero, it will be replaced with the left 'wall'.
		++i;
	}
}

```