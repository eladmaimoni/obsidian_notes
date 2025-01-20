- [452. Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/)
- like [[1 - Minimum Platforms]]] 
- but instead of finding the maximum amount of overlapping segments we need to find the total number of overlaps 

### Intuition
- if we sort the segments by their ending point we can


```
int findMinArrowShots(vector<vector<int>>& points) {

    // sort points by endpoint
    sort(points.begin(), points.end(), [] (const vector<int>& a, const vector<int>& b)
        {
            return a[1] < b[1];
        }
    );

    int n = points.size();
    auto last_end_that_shooted_arrow = points[0][1];
    auto total_arrows = 1;
    for (auto i = 1; i < n; ++i)
    {
        auto& point = points[i];
        auto start = point[0];
        auto end = point[1];

        if (start <= last_end_that_shooted_arrow)
        {
            // the last shooted arrow still applies
        }
        else
        {
            last_end_that_shooted_arrow = end;
            ++total_arrows;
        }
    }

    return total_arrows;
}
```