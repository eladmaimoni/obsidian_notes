https://leetcode.com/problems/linked-list-cycle-ii/

- when detecting a cycle on a linked list, we rely on the fact that the margin between the nodes (slow and fast) keeps increasing by 1 each iteration
- when the 2 pointers meet at iteration `i`, we know that:
	- the slow pointer is at distance `i` from `head`
	- the fast pointer is at distance `2i` from head
- the cycle is exactly at length `i` since that is the accumulated distance between the `slow` and `fast` pointers.
- if the distance to the `junction` is `m`, then the distance between the junction and `i` is `i - m`
- that is exactly the distance between where the slow pointer is and the junction


### Linked List when the cycle is detected at iteration `i` 

![[Pasted image 20241104213529.png]]