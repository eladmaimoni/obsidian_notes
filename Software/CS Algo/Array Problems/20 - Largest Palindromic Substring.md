

#dynamic-programming #2-pointers #memoization 
#sliding_window 
### $O(n^2)$ time with $O(n)$ space
- strings of length 0 or 1 are palindromic
- we use a sliding window of length d
- compare chars on both ends of the sliding window
- maintain in memory the result of the substring that has window length d - 2
- check if the substring of length d - 2 that is contained within the window is also palindromic

```
string longestPalindrome(string s) 
{
    auto startIdx = 0;
    auto length = 1;

    auto n = s.size();

    std::vector<uint8_t> before_even(n, 1); // d = 0
    std::vector<uint8_t> before_odd(n, 1); // d = 1
    std::vector<uint8_t> current_arr(n, 0);

    std::array<uint8_t*, 2> prev_arr;
    prev_arr[0] = before_even.data();
    prev_arr[1] = before_odd.data();
    uint8_t* current = current_arr.data();
    
    for (auto d = 2; d <= n; ++d)
    {
        uint8_t* prev = prev_arr[d % 2];
        auto start = 0;
        auto end = start + d - 1;

        while (end < n)
        {          
            if (prev[start + 1] && s[start] == s[end])
            {
                current[start] = 1;
                startIdx = start;
                length = d;
            }
            else
            {
                current[start] = 0;
            }
            ++start;
            ++end;
        }

        swap(current, prev_arr[d % 2]);
    }

    return s.substr(startIdx, length);
}
```

### Manacher's Algorithm - O(n) time
#todo
