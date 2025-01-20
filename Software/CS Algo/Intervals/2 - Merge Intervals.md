- [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)
- 

```
struct Point
{
    int idx;
    bool is_end;
};
vector<vector<int>> merge(vector<vector<int>>& intervals) 
{
    int n = intervals.size();
    vector<Point> points(2 * n);

    for (auto i = 0; i < n; ++i)
    {
        points[2 * i] = Point{intervals[i][0], false};
        points[2 * i + 1] = Point{intervals[i][1], true};
    }

    sort(points.begin(), points.end(), [] (const Point& p1, const Point& p2)
    {
        if (p1.idx != p2.idx)
        {
            return p1.idx < p2.idx;
        }
        else if (p1.is_end != p2.is_end)
        {
            return !p1.is_end;
        }
        else
        {
            return false;
        }
    });

    vector<vector<int>> result;
    result.reserve(n);
    int count = 0;
    int s = 0;
    int e = 0;
    for (auto p : points)
    {
        if (p.is_end)
        {
            --count;
            if (0 == count)
            {
                result.emplace_back(vector{s, p.idx});
            }
        }
        else
        {
            // p is start
            ++count;
            if (1 == count)
            {
                s = p.idx;
            }
        }
    }

    return result;
}
```
#intervals