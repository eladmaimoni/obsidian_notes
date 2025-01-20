- [28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/)

Repetitions: ||
- string matching really matters if the input string has a lot of repetitions of a substring from the pattern
- for example:
  - string = "rarararararbingo"
  - pattern = "rarbingo"
  - we will do a lot of false matching each time we encounter the letter 'r' in the string


The KMP (Knuth-Morris-Pratt) algorithm optimizes the search for a substring (`needle`) within a main string (`haystack`) by pre-processing the `needle`. This pre-processing involves creating the LPS (Longest Prefix Suffix) array, which allows the algorithm to skip unnecessary comparisons, achieving a time complexity of `O(n+m)`, where `n` is the length of the `haystack` and `m` is the length of the `needle`.

### Longest Prefix Suffix Table
For a given `pattern` the `lps[i]` looks at the substring `pattern[0:i]` and tells us the length of the of the substring that ends at `i` and:
- is a prefix of `pattern[0:i]`
- is a suffix of `pattern[0:i]`
- both prefix and suffix may not contain the whole pattern(hence they are called 'proper')

table represent for each index the length of the substring that ends in that index and is both a prefix of `pattern` and a suffix of the same 

```
std::vector<int> lps(const string& pattern)
{
    auto n = pattern.size();
    std::vector<int> lps_table(n);
    lps_table[0] = 0;

    auto i = 1;
    auto w = 0;

    while (i < n)
    {
        if (pattern[i] == pattern[w])
        {
            ++w;
            lps_table[i] = w;
            ++i;
        }
        else
        {
            if (w > 0)
            {
                // so far, we have matched the pattern with w chars.
                // but there is a mismatch.
                // the pattern we have so far (until i - 1) matches the beginning of the pattern
                // we would like to take the pattern that begins one char to the front and see if that
                // partially prefix the string
                // we need to match again
                w = lps_table[w - 1];
            }
            else
            {
                w = 0;
                lps_table[i] = w;
                ++i;
            }
        }
        
    }

    return lps_table;
}

int strStr(string haystack, string needle) 
{
    auto lps_table = lps(needle);

    auto n = haystack.size();
    auto m = needle.size();

    auto i = 0;
    auto j = 0;

    while (i < n && j < m)
    {
        if(haystack[i] == needle[j])
        {
            ++j;
            ++i;
        }
        else
        {
            if (j > 0)
            {
                j = lps_table[j - 1];
            }
            else
            {
                j = 0;
                ++i;
            }
        }

    }


    if (j == m)
    {
        return i - m;
    }
    else
    {
        return -1;
    }
}
```