- [480. Sliding Window Median](https://leetcode.com/problems/sliding-window-median/)
https://thewayofnada.medium.com/a-very-thorough-solution-to-sliding-window-median-and-some-heap-magics-5091a3ed1cdc


Idea
- We have a sliding window of size K (odd number)
- Maintain 2 heaps
  - min heap - containing elements larger than the median (up to K size)
  - max heap - containing elements smaller than the median (up to K size)
  - the median is always the top of the min heap
  - the min heap is always the same size or larger than the max heap
  - heap sizes sum to K
- when a new element is encountered:
  - if it is larger or equal to the median - add it to the min heap
  - if it is smaller - add it to the max heap
  - balance the heaps - pop from one and add to another until they have the same length

- sdf
