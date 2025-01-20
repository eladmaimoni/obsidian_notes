https://leetcode.com/problems/container-with-most-water/description/

https://jessijokes.medium.com/solving-the-leetcode-container-with-most-water-problem-f720c4f0dacd

- Repetitions: ||
- Understanding Rate: 40%
### **Why Does This Work?**

#### **1. Starting with the Maximum Width**

- By initializing `start` and `end` at the extreme ends of the array, you start with the widest possible container.
- The initial area is calculated using the full width of the array.

#### **2. Moving the Shorter Line**

- **Reasoning**:
    
    - The area is determined by the min height.
    - Moving the taller line inward **cannot** increase the area because:
        - The width decreases.
        - The min height cannot increase.
        - No matter how much we move the index, the area will be limited by the shorter line.
    - Moving the shorter line inward **may** increase the area.
    - If we move the shorter line, we don't miss any potential larger area with the taller line (because we keep examine candidates to it until we find a taller line) 
    - If we were to move the taller line, we could potentially miss on candidates that create a larger area with it.

```
    int maxArea(vector<int>& height) {
        auto n = height.size();
        int start = 0;
        int end = n - 1;
        int max_container = -1;
        while (start < end)
        {

            auto h_left = height[start];
            auto h_right = height[end];
            auto container_size = (end - start) * min(h_left, h_right);
            max_container = max(max_container, container_size);

            if (h_left < h_right)
            {
                ++start;
            }
            else
            {
                --end;
            }
        }
        return max_container;
    }
```

#2-pointers #arrays 