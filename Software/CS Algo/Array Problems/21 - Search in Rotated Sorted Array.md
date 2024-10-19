### Find the pivot
- the pivot is either the min or max element
- the pivot is an element where **both** the right or the left are larger than it
  4 5 6 **0** 1 2 3
- 
- if an subarray is rotated, we have no idea which value range is there
	- we know that both the maximum and the minimum is there
	- hence we should look at the whole array
- when subdividing a rotated sorted array, only one side remains rotated
	- 