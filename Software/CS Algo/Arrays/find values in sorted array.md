find the first and last occurrences of an element **x** in the given array

### approach 1 - binary search and then linear search on limits (l, r)
- this can be quite expensive if the searched value is exactly in the middle and only has 1 instance
```
    vector<int> find(int arr[], int n , int x )
    {
        int l = 0;
        int r = n;
        
        while (l < r)
        {
            auto m = (l + r) / 2;
            auto val = arr[m];
            
            if (val == x)
            {
                while (arr[l] < x) ++l;
                while (arr[r - 1] > x) --r;
                
                return {l, r - 1};
            }
            else if (val < x)
            {
                l = m + 1;
            }
            else 
            {
                r = m;
            }
        }
        
        return {-1, -1};
        
    }
```

this is actually $O(n)$ in the worst case

### approach 2 - 2 times binary search
- when we find the value in the search, we keep updating the limits (l, r)
```
bool found = false;
while (l < r)
{
	auto m = (l + r) / 2;
	auto val = arr[m];
	if (val == x)
    {
	    // we found the value,
	    // if we keep pushing the left boundary
	    // it will become its right limit
	    l = m + 1;
	    found = true;
    }
    else if (val < x)
    {
	    l = m + 1;
    }
    else 
    {
	    r = m;
    }
}

if (found)
{
	result[1] = l - 1; // right limit, last index that equals x
	while (l < r)
	{
		auto m = (l + r) / 2;
		auto val = arr[m];
		if (val == x)
	    {
		    // we found the value,
		    // if we keep pushing the right boundary
		    // it will become its right limit
		    r = m;
	    }
	    else if (val < x)
	    {
		    l = m + 1;
	    }
	    else 
	    {
		    r = m;
	    }
	}
	result[0] = r;
}
```