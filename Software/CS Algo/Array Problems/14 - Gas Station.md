https://leetcode.com/problems/gas-station/

Repetitions: ||
Understanding: 70%

```
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        auto n = gas.size();
        auto start_idx = 0;
        while (start_idx < n)
        {
            auto tank = 0;
            for (auto i = start_idx; i <= (start_idx + n); ++i)
            {
                if (tank < 0)
                {
                    // no more gas, we can't choose this starting point
                    // if we started at a and ran out of gas at point b
                    // then we would have run out of gas if we were to 
                    // start on any point between a and b
                    // (think that we got to a + 1 with a non-negative tank)
                    // and if we start at a + 1 with an empty tank, we will
                    // certainly run out of gas when we reach b.
                    start_idx = i;
                    break;
                }
                auto idx = i % n;
                // accumulate and travel to the next station
                tank = tank + gas[idx] - cost[idx];
            }
            if (tank >= 0)
            {
                return start_idx;
            }
        }

        return -1;

}
```

#greedy

If we start on `a` and run out of gas at point `b`, then we will run out of gas even if we start at `[a,b)`.
- because we got until `b` from `a`, it means we got to `a + 1` with a non negative tank. if we were to start from `a + 1` with an empty tank, we would certainly run out of gas when we reach `b`.


