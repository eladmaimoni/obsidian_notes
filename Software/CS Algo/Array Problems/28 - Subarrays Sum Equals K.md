- [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

```
    int subarraySum(vector<int>& nums, int k) 
    {
        std::unordered_map<int, int> prefixes_count;

        int n = nums.size();
        
        int acc = 0;
        int total = 0;
        for (int i = 0; i < n; ++i)
        { 
            int val = nums[i];
            acc += val;
            
            int prefix = acc - k;

			// prefix_count[prefix] means the number of ways
			// to obtain a contig sub array (from with different end points)
			// that amounts to prefix
			// we can create k with those end points
            total += prefixes_count[prefix];
            total += (acc == k); // prefix needed is zero, so we can just use the path to acc - the whole array as well
            prefixes_count[acc] += 1;
        }
        
        return total;
    }
```

#hash-map #arrays #prefix-sum
