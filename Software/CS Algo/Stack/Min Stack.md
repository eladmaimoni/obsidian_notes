
[155. Min Stack](https://leetcode.com/problems/min-stack/)

- the trick (which I understood by myself) is to maintain 2 separate stacks.
- one stack for values
- one stack for min values - only add values that are smaller or equal to the last min
- we take advantage of the fact that previous min values are deeper within the min stack
```
    void push(int val) {
        if (min_vals_stack.empty() || val <= min_vals_stack.back())
        {
            min_vals_stack.push_back(val);
        }
        vals.push_back(val);

    }

    void pop() {
        auto back = vals.back();
        if (back == min_vals_stack.back())
        {
            min_vals_stack.pop_back();
        }
        vals.pop_back();

    }
```