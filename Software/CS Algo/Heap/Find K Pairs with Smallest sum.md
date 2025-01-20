```
struct Pair
{
    int i1;
    int i2;
};
inline bool operator<(const Pair& p1, const Pair& p2)
{
    if (p1.i1 != p2.i1)
    {
        return p1.i1 < p2.i1;
    }
    else
    {
        return p1.i2 < p2.i2;
    }
}

vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {

    vector<vector<int>> res;

    auto comp = [&](const Pair& p1, const Pair& p2){
        auto sum1 = nums1[p1.i1] + nums2[p1.i2];
        auto sum2 = nums1[p2.i1] + nums2[p2.i2];
        return sum1 > sum2;
    };
    std::priority_queue<Pair, std::vector<Pair>, decltype(comp)> min_heap(comp);

    std::set<Pair> visited;

    int n1 = nums1.size();
    int n2 = nums2.size();

    min_heap.push(Pair{0,0});
    visited.insert(Pair{0,0});
    while (res.size() < k)
    {
        auto top = min_heap.top();
        min_heap.pop();

        res.emplace_back(vector<int>{nums1[top.i1], nums2[top.i2]});
        Pair next1{top.i1 + 1, top.i2}; 
        Pair next2{top.i1, top.i2 + 1}; 

        if (next1.i1 < n1 && visited.find(next1) == visited.end())
        {
            min_heap.push(next1);
            visited.insert(next1);
        }

        if (next2.i2 < n2 && visited.find(next2) == visited.end())
        {
            min_heap.push(next2);
            visited.insert(next2);
        }
    }
    return res;
}
```