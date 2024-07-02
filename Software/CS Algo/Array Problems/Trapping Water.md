```
    long long trappingWater(int arr[], int n)
    {
        
        // water accumulate according to the formula:
        // min(heighest_from_left, heighest_from_right) - height
        
        std::vector<int> heightest_from_left(n, 0);
        
        
        auto max_height_from_left = 0;
        
        for (auto i = 1; i < n; ++i)
        {
            auto height_from_left = arr[i - 1];
            max_height_from_left = max(max_height_from_left, height_from_left);
            heightest_from_left[i] = max_height_from_left;
        }
        
        auto max_height_from_right = 0;
        
        auto total_water = 0ll;
        for (auto i = n - 2; i >= 0; --i)
        {
            auto height_from_right = arr[i + 1];
            max_height_from_right = max(max_height_from_right, height_from_right);
            auto water = min(heightest_from_left[i], max_height_from_right) - arr[i];
            if (water > 0)
            {
                 total_water += water;
            }
        }
        
        return total_water;
        // code here
    }
```