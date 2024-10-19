https://leetcode.com/problems/coin-change/

- Minimum number of coins to reach a certain amount
- Given an array of coins with different values, what is the minimum number of coins to reach a certain amount

Repetitions: ||
Understanding: 90%

```
int coinChange(vector<int>& coins, int amount) 
{
    // this array will keep the minimum number of coins we can use
    // to reach the amount of money
    // so the result will be in index 0
 
    std::vector<int> min_coins_to_reach_target(amount + 1, -1);
    min_coins_to_reach_target[0] = 0;
    auto n = coins.size();
    auto data = coins.data();

    for (auto target = 1; target <= amount; ++target)
    {
        auto min_coins = INT_MAX;
        for (auto c : coins)
        {
            auto pre_target = target - c;

            if (pre_target >= 0)
            {
                auto min_coins_to_reach_pre_target = min_coins_to_reach_target[pre_target];

                if (min_coins_to_reach_pre_target != -1)
                {
                    // pre target can be reached
                    min_coins = min(min_coins, min_coins_to_reach_pre_target + 1);
                }
            }
        }

        if (min_coins != INT_MAX)
        {
            min_coins_to_reach_target[target] = min_coins;
        }

    }
 
    return min_coins_to_reach_target[amount];
}
```

#dynamic-programming #memoization #greedy 

