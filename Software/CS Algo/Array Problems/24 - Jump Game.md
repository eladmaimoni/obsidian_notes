https://leetcode.com/problems/jump-game/?envType=problem-list-v2&envId=array&difficulty=MEDIUM

Idea: 
- whenever you encounter a zero, you should keep counting the 'gap' you must jump over until you encounter a cell that allows you to jump over it
- the end of the array is a special case
```
bool canJump(vector<int>& nums) 
{
    auto n = (int)nums.size();

    if (n == 1) return true;
    int gap = 0;
    for (auto i = n - 1; i >= 0; --i)
    {
        auto val = nums[i];
        auto d = n - i - 1;

        if (val == 0)
        {
            ++gap;
        }
        else
        {
            if (val > gap || val >= d)
            {
                gap = 0;
            }
            else
            {
                ++gap;
            }
        }
    }

    return gap <= 0;
}
```