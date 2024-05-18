- given an array of non negative integers, find the index where the exclusive accumulative sum up to to it, equals to the sum after it.
- sum before element - equals sum after it
- corner cases [1], [1 0]
- an easier solution will be 2 times accumulative sum but will require 2 passes.
- here we use to pointers style solution

```
    int equilibriumPoint(long long a[], int n) 
    {
        

        auto left = -1;
        auto right = n;
        long long sum_left = 0;
        long long sum_right = 0;
        

        while ((right - left) > 2 || sum_left != sum_right)
        {
            if (sum_left < sum_right)
            {
                 ++left;
                 sum_left += a[left];

            }
            else if (sum_left > sum_right)
            {
                
                 --right;
                 sum_right += a[right];
            }
            else
            {
                // sum are the same
                // by first priority:
                // - move to an element with zero value
                // else just move left
                // this ugliness is to account for 
                // corner cases such as [1 0] whose 
                // equlibrium point is 1
                if (left < (n-1) && a[left + 1] == 0)
                {
                    ++left;
                }
                else if (right > 0 && a[right - 1] == 0)
                {
                   --right;
                }
                else
                {
                    ++left;
                    sum_left += a[left];
                }
                

            }
        }

        if (sum_left == sum_right && (right - left) == 2)
        {
             return right;
        }
        else
        {
            return -1;
        }
       
    }
```