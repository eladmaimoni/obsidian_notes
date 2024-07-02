```
// loop invariant - everyting is sorted up to i
for (auto i = 1; i < n - 1; ++i)
{
	// find a place for a[i]
	auto j = i;
	while (j > 0 0 && a[j] < a[j - 1])
	{
		// move a[i] left until it is in the right place
		swap(a[j], a[j - 1]);
		--j;
	}
	
}
```