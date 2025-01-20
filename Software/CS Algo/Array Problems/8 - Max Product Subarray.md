
https://leetcode.com/problems/maximum-product-subarray

- given an array, find the subarray producing the largest product

Solution
- if we are at element `i`, the best product we can produce is:
- the best product up until `a[i - 1]` multiplied by `a[i]`
- if a[i] is negative, we better take the best negative product up to a[i-1]

Conclusions:
- initializing both 'bests' to 0 makes it hard
```
long long best_negative_product_with_i = 0;
long long best_positive_product_with_i = 0;
long long best = INT_MIN;   
``` 
since this is not a valid product and can interfere with min / max functions along the way. we have no way to differentiate between actual zero element and no product
- better adhere to the principles:
  - try to initialize the first term outside the loop
  - keep loop invariants - if we say negative product then make sure it is negative, or mark it as invalid
- A better way is to relax the invariants - min multiplication and max multiplication instead of negative and positive
```
	long long maxProduct(vector<int> arr, int n) 
	{
	    // what is the best result using the ith element?
	    long long max_ending_at_v = arr[0];
	    long long min_ending_at_v = arr[0];
	    long long max_product = arr[0];
	 
	    //
	    // the idea is to keep the maximal value that can be obtained using the last value
	    // but also the minimal value that might be flipped to become the best one (if it is negative)
	    // note that both elements might be positive, negative or zero at the same time
	    
	    for (auto i = 1; i < n; ++i)
	    {
	        long long v = arr[i];
	        
	        long long ending_at_v_1 = max_ending_at_v * v;
	        long long ending_at_v_2 = min_ending_at_v * v;
	        
	        
	        if (ending_at_v_1 > ending_at_v_2)
	        {
	            max_ending_at_v = ending_at_v_1;
	            min_ending_at_v = ending_at_v_2;
	        }
	        else
	        {
	            max_ending_at_v = ending_at_v_2;
	            min_ending_at_v = ending_at_v_1;
	        }
	        
	        max_ending_at_v = max(max_ending_at_v, v);
	        min_ending_at_v = min(min_ending_at_v, v);
	        
            max_product = max(max_ending_at_v, max_product);
	    }
	 
	    return max_product;
	}
```