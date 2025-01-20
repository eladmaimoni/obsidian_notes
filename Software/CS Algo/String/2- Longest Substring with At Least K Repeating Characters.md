- [395. Longest Substring with At Least K Repeating Characters](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)

Repetitions: |
return that length of the largest substring that contains at least K repetitions of each char in it.


- $O(nk)$ 

### Subarray with `i` unique values:
- Given a vector of finite set of `m` unique values, find all the possible contiguous subarrays that contain EXACTLY `i <= m` values
- We can use an expanding / shrinking window with a histogram:
  - when there are less than `i` unique value, keep expanding the window
  - when there is more than `i` unique values, shrink the window from the left
  - when there is exactly `i` unique values, keep expanding

#2-pointers
### Unique values
- If we categorize the valid substrings according to the number of unique chars they have
- It is possible to iterate all possible substrings with exactly `k` unique values using the 2-pointers approach
- we can add a loop over all `k`'s to cover all substrings that might match
- this allows us to process all possible substrings more efficiently, since the 2-pointers approach uses induction to skip on redundant substrings (think what happens when we shrink the window, we don't start over at the next index)


```
int longestSubstring(string s, int k) 
{
    // phase 1: count the number of unique chars
    auto total_unique_chars = 0;
    {
        array<int, 26> hist{};
        for (auto c : s)
        {
            int v = c - 'a';

            if (hist[v] == 0)
            {
                hist[v] = 1; 
                ++total_unique_chars;
            }
        }
    }


    auto max_length = 0;

    int n = s.size();
    for (auto unique_count = 1; unique_count <= total_unique_chars; ++unique_count)
    {
        auto start = 0;
        auto end = -1;

        array<int, 26> hist{};
        auto at_least_k_count = 0;
        auto current_unique = 0;

        while (end < n)
        {
            if (current_unique <= unique_count)
            {
                // expand
                ++end;

                if (end < n)
                {
                    int new_val = s[end] - 'a';

                    if(hist[new_val] == 0)
                    {
                        ++current_unique;
                    }
                    
                    if (hist[new_val] == (k - 1))
                    {
                        ++at_least_k_count;
                    }

                    hist[new_val] += 1;
                }
                else
                {
                    break;
                }

            }
            else
            {
                // shrink
                int removed_val = s[start] - 'a';
                ++start;

                if(hist[removed_val] == 1)
                {
                   --current_unique;
                }
                
                if (hist[removed_val] == k)
                {
                    --at_least_k_count;
                }

                hist[removed_val] -= 1;
            }


            auto length = (end - start + 1);


            // all unique chars have at least 
            if (current_unique == unique_count && at_least_k_count == unique_count && length > max_length)
            {
                max_length = length;
            }
        }
    }

    return max_length;
}
```

