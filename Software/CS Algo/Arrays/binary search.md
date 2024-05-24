```
    int binary_search(int* arr, int n, int x)
    {
        int l = 0;
        int r = n;
        
        while (l < r)
        {
            auto m = (l + r) / 2;
            auto val = arr[m];
            
            if (val == x)
            {
                return m;
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
	    return -1;
    }
```

