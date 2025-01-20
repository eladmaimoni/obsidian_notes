Repetitions

#dynamic-programming #2-pointers #memoization 
#sliding_window 
### $O(n^2)$ time with $O(n)$ space
- strings of length 0 or 1 are palindromic
- we use a sliding window of length d
- compare chars on both ends of the sliding window
- maintain in memory the result of the substring that has window length d - 2
- check if the substring of length d - 2 that is contained within the window is also palindromic

```
    string longestPalindrome(string str)

    {
        int n = str.size();
        // for even d
        std::vector<unsigned char> is_palindrome(n, 1); // 0 length is palindrome
        
        int longest_even = 0;
        int longest_s_even = 0;
        for (auto d = 2; d <= n; d += 2)
        {
            for (auto s = 0; s <= (n - d); ++s)
            {
                auto e = s + d - 1;

                if (is_palindrome[s + 1] && str[s] == str[e])
                {
                    is_palindrome[s] = 1;
                    longest_even = d;
                    longest_s_even = s;
                }
                else
                {
                    is_palindrome[s] = 0;
                }
            }
        }
  
        // now odd
        is_palindrome.assign(n, 1);
        int longest_odd = 1;
        int longest_s_odd = 0;
        for (auto d = 3; d <= n; d += 2)
        {
            for (auto s = 0; s <= (n - d); ++s)
            {
                auto e = s + d - 1;

                if (is_palindrome[s + 1] && str[s] == str[e])
                {
                    is_palindrome[s] = 1;
                    longest_odd = d;
                    longest_s_odd = s;
                }
                else
                {
                    is_palindrome[s] = 0;
                }
            }

        }

  

        if (longest_odd > longest_even)
        {
            return str.substr(longest_s_odd, longest_odd);
        }
        else
        {
            return str.substr(longest_s_even, longest_even);
        }

    }
```

### Manacher's Algorithm - O(n) time
#todo
