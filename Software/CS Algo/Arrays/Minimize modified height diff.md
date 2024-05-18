- given array of integers `a[]`, and a modifier $\pm{k}$ , find the smallest possible diff between the maximum and minimum value in the modified array.


What do we learn?
- if we need a certain window of elements to include "all instances" (for example - all indices, or all sets of certain values), we probably need a histogram
- 


$O(n\log(n))$ time with $O(n)$ space

1. combined sorted array of tuples (value, index)
	- create a sorted array (2N) of all possible modifications and their index `{a[i] + k, i}, {a[i] - k, i}`
	- sorted by value
```
   // 1. combined sorted array of tuples (value, index)
   std::vector<HeightIdx> modified_values(2 *n);
   for (int i = 0; i < n; i++) 
   {
       modified_values[2 * i] = { arr[i] - k, i };
       modified_values[2 * i + 1] = { arr[i] + k, i };
   }
   std::sort(modified_values.begin(), modified_values.end(), 
   [](HeightIdx a, HeightIdx b) { return a.height < b.height;}
   );
```
2. we now wish to find the segment that contains 
- at least one instance of each element AND
- has the smallest difference between the first and last element (assuming they are not the same of the same index)

	- keep a histogram for each index to count available elements in the segment
	- go through the sorted array left to right to find 2 boundaries (AKA 2 pointers)
	- right boundary - always set up such that we will have at least one instance of each element in the segment
```
void push_right_until_we_have_all_elements_in_range(
std::vector<int>& segment_indices_histograms,
int& elements_in_range, 
int& right, 
const std::vector<HeightIdx>& modified_values,
int n
)
{
    while (elements_in_range < n && right < modified_values.size())
    {
        auto idx = modified_values[right].idx;

        auto count = segment_indices_histograms[idx]++;

        if (count == 0)
        {
            // we have a new element in the range
            elements_in_range++;
        }

        ++right;
    }
}	  
```
	
	- afterwards - we push left one element and  then push right again until all elements are present
	- our aim is to push right boundary as little as possible since it will increase the gap from left boundary


Variation where the modification must result in a non negative height:
```
struct HeightIdx
{
    int height;
    int idx;
};

void push_right_until_we_have_all_elements_in_range(std::vector<int>& segment_indices_histograms, int& elements_in_range, int& right, const std::vector<HeightIdx>& modified_values, int n)
{
    while (elements_in_range < n && right < modified_values.size())
    {
        auto idx = modified_values[right].idx;

        auto count = segment_indices_histograms[idx]++;

        if (count == 0)
        {
            // we have a new element in the range
            elements_in_range++;
        }

        ++right;
    }
}

int getMinDiff(int arr[], int n, int k) 
{
    if (n == 1)
    {
        return 0;
    }
    // 1. combined sorted array of tuples (value, index)
    std::vector<HeightIdx> modified_values;
    modified_values.reserve(2 * n);
    for (int i = 0; i < n; ++i) 
    {
        auto val = arr[i];
        if (val >= k)
        {
            modified_values.push_back({ val - k, i });
        }
        // else
        // {
        //     std::cout << "val: " << val << " k: " << k << std::endl;
        // }
        modified_values.push_back({ val + k, i });
    }
    std::sort(modified_values.begin(), modified_values.end(), [](HeightIdx a, HeightIdx b) {
        return a.height < b.height;
        });


    std::vector<int> segment_indices_histograms(n);

    int elements_in_range = 0;
    int left = 0;
    int right = 0;

    push_right_until_we_have_all_elements_in_range(
        segment_indices_histograms,
        elements_in_range, 
        right, 
        modified_values, 
        n
    );

    auto min_diff = INT_MAX;
    
    
    while (left < n  && elements_in_range == n)
    {
        // loop invariant: we have all n elements in the range

        auto max_height = modified_values[right - 1].height;
        auto min_height = modified_values[left].height;
        auto max_idx = modified_values[right - 1].idx;
        auto min_idx = modified_values[left].idx;

        if (max_idx != min_idx)
        {
            min_diff = std::min(min_diff, max_height - min_height);
        }
        
        ++left;
        auto count = --segment_indices_histograms[min_idx];

        if (count == 0)
        {
            --elements_in_range;

            push_right_until_we_have_all_elements_in_range(
                segment_indices_histograms,
                elements_in_range,
                right,
                modified_values,
                n
            );
        }
    }

    return min_diff;
}
};
```

