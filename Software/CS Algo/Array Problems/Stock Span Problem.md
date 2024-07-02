For each array element, find the number of elements to its left that are smaller than the element.

Idea:
- Go through elements start to end
- Keep a vector of elements (index, value) which are larger than the current element
- When done processing `a[i]` the vector contains only elements that are larger than `a[i]` and `a[i]` itself
- The vector (stack) implements the recursive rule:
  `(a[0] < v)` $\bigcap$ `. . .` (`a[i-2] < v`) $\bigcap$ (`a[i-1] < v` ) $\bigcap$ (`a[i] < v`)
  where v is the group of elements to the left of a[i]
- On the next step we **pop** all elements that are smaller or equal to `a[i + 1]` (there are at most i like these) and keep only those larger than `a[i + 1]`

Invariant:
- at each iteration `i`, all the elements in the array are larger then `a[i]`
- maintaining that invariant takes at most `n` operations throughout the loop

When we process element i:
- the first element to the left that is larget than a[i] is either a[i -1] or (if a[i - 1] is smaller than it) one of the elements that are larger than a[i -1] - we pop them until we get to one.

```
    struct IdxVal
    {
        int idx;
        int val;
    };
    //Function to calculate the span of stockâ€™s price for all n days.
    vector <int> calculateSpan(int price[], int n)
    {

        vector<IdxVal> s;
        s.reserve(n / 2);

        vector<int> spans(n);

        for (auto i = 0; i < n; ++i)
        {
            auto val = price[i];
            
            // pop all elements <= a[i] until we reach an element that is larger than a[i]
            while (!s.empty() && s.back().val <= val)
            {
                s.pop_back();
            }
            
            // now the stack contains only elements that are larger than a[i] or non at all
            
            int counter;
            if (!s.empty())
            {
                counter = i - s.back().idx;
            }
            else
            {
                counter = i + 1;
            }
            
            spans[i] = counter;
            s.push_back(IdxVal{i, val});
        }
        
        return spans;
 
    }
```