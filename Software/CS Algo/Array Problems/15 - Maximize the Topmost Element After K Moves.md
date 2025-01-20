
[2202. Maximize the Topmost Element After K Moves](https://leetcode.com/problems/maximize-the-topmost-element-after-k-moves/)

Repetitions: ||

Understanding: 80%
```
    int maximumTop(vector<int>& nums, int k) {

        auto n = nums.size();

  

        if (n == 1 && (k % 2) == 1)

        {

            return -1;

        }

  

        int max_element = INT_MIN;

  

        if (k <= n)

        {

            // maximum between a[0 : k - 2] and a[k]

            for (auto i = 0; i < k - 1; ++i)

            {

                max_element = max(max_element, nums[i]);

            }

  

            if (k < n)

            max_element = max(max_element, nums[k]);

        }

        else if (k > n)

        {

            // just remove all and then either return the max (odd lefteover)

            // or alternately return the 2 highest

            for (auto i = 0; i < n; ++i)

            {

                max_element = max(max_element, nums[i]);

            }

        }

  
  
  

        return max_element;

    }
```