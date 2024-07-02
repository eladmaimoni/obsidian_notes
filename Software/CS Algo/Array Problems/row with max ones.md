
- each row is sorted [0 0 0 1 1 1 1]
- we need to find the first row with the maximum ones

Algorithm:
- we need to find the maximum column that has zero
- we go row by row, each starting from the max column that has zero
```
	    auto max_ones = 0;
	    auto row_idx = -1;
	    
	    auto max_col_with_zero = m - 1;
	    
	    for (auto r = 0; r < n && max_col_with_zero >= 0; ++r)
	    {
	        auto& row = arr[r];
	        
	        while (max_col_with_zero >= 0 && row[max_col_with_zero])
	        {
	            // this column has 'one'
	            --max_col_with_zero; 
	        }
	        
	        auto ones = m - max_col_with_zero - 1;
	        if (ones > max_ones)
	        {
	            max_ones = ones;
	            row_idx = r;
	        }
	        
	        
	    }
	    
	    return row_idx;
	    
```