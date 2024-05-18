A simple implementation of the partition algorithm:
- go through all elements and throw to the left all the elements smaller than or equal to the pivot
```
int partition(int arr[], int l, int r, int pivot)
{
    // when done, position l will point to the first element that is greater than pivot
    for (auto i = l; i < r; ++i)
    {
        auto val = arr[i];

        if (val <= pivot)
        {
            std::swap(arr[l], arr[i]);
            ++l;
        }
    }

    return l - 1; // return the position of the pivot
}
```

This implementation has its problems:
- Although it partitions the array into 2 parts, the pivot itself can end up **anywhere** in the left part of the array.
- when we partition the subarray again, we might choose the same element again
- we don't know where the pivot might end up

An alternative is
1. select the pivot
2. swap the pivot to be the last element
3. once done with the partition, the pivot position will be the last on the left

```
int partition(int arr[], int l, int r, int pivot_idx)
{
	
	
	std::swap(arr[pivot_idx], arr[r - 1]);
	auto pivot = arr[r - 1];


    // when done, position l will point to the first element that is greater than pivot
    for (auto i = l; i < r - 1; ++i)
    {
        auto val = arr[i];

        if (val <= pivot)
        {
            std::swap(arr[l], arr[i]);
            ++l;
        }
    }
	std::swap(arr[l], arr[r - 1]); // last swap is the pivot
    return l; // return the position of the pivot
}
```