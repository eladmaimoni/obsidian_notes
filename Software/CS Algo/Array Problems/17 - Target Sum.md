
https://leetcode.com/problems/target-sum/description/

https://walkccc.me/LeetCode/problems/494/
# Naive $O(2^n)$

```
    int expressionCountInner(int* nums, int n, int target)
        if (n == 1)
        {
            if (nums[0] == target && nums[0] == -target)
            {
                return 2;
            }
            else if (nums[0] == target || nums[0] == -target)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }
        auto val = nums[0];
        auto target1 = target - val;
        auto target2 = target + val;
        auto res1 = expressionCountInner(nums + 1, n - 1, target1);
        auto res2 = expressionCountInner(nums + 1, n - 1, target2);
        return res1 + res2;
    }

    int findTargetSumWays(vector<int>& nums, int target)
    {
        return expressionCountInner(nums.data(), nums.size(), target);
    }
```


# Optimization

### Analyses
- We divide the array into to sets:
	- $P$ - all numbers chosen to be positive
	- $N$ - all numbers chosen to be negative
- $P + N = sum(array)$
- $P - N = target$
- $2P = sum(array) + target$
- $2N = sum(array) - target$
### Conclusions
- $sum(array) + target$ and $sum(array) - target$ must be even otherwise the equations don't hold
- We can reduce the problem to finding $P$ that equals $sum(array) + target$ (or $N$ that equals) $sum(array) - target$ 

### Finding $P = (sum(array) + target) / 2$
- First verify $sum(array) + target$ is even
- Zeros can be used by any solution in both signs. so we can remove them during analyses and multiply the final number of combinations by $2^{zeros}$
- Find Subset of numbers that add to $P$

# Counting combinations that add to target number

### Naive
```
int countCombinationsThatAddToTarget(int* nums, int n, int target)
{
    // any number can be either chosen or not
    
    auto val = nums[0];
    auto combinations = 0;
    if (n > 1)
    {
        if (val > target)
        {
            // we can't add this value
            combinations += countCombinationsThatAddToTarget(nums + 1, n - 1, target);
        }
        else
        {
            combinations += countCombinationsThatAddToTarget(nums + 1, n - 1, target);
            combinations += countCombinationsThatAddToTarget(nums + 1, n - 1, target - val);
        }
    }
    else
    {
        if (target == 0)
        {
            combinations += 1;
        }
        if (val == target)
        {
            combinations += 1;
        }
    }
    return combinations;
}
```
### With Memoization
- we can hold an array of with size of target sum
- go through each number
- basic equations:
	- the number of combinations to reach a target with the value
	- equals the number of combinations to reach (target - value) without the value 

```
int findTargetSumWays(vector<int>& nums, int target) 
{        
    int sum = 0;
    auto n = nums.size();
    for (auto i = 0; i < n; ++i)
    {
        auto val = nums[i];
        sum += val;
    }

    auto positive_target = sum + target;
    if (0 != positive_target % 2 || positive_target < 0)
    {
        return 0;
    }
    positive_target /= 2;
    vector<int> combinations_to_target(positive_target + 1, 0);
    combinations_to_target[0] = 1; // a single combinations to 0

    for (auto i = 0; i < n; ++i) // we may use each value only once
    {
        auto num = nums[i];
        for (auto current_target = positive_target; current_target >= num; --current_target)
        {
            auto pre_target = current_target - num;
            combinations_to_target[current_target] += combinations_to_target[pre_target];
        }
    }
    return combinations_to_target[positive_target];
}
```

#dynamic-programming #memoization 
