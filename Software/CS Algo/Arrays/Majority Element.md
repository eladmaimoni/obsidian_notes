https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm

Find the array that occurs more than N/2 times in the array, if it exists

Idea
- if an elements occurs more than N/2, counting the rest of the elements combined will sum to less than N/2.
- If we loop and keep a counter for each variable we see, the majority element


```
auto votes = 1;
auto majority_candidate = a[0];
for (auto i = 1; i < n; ++i)
{
	auto val = a[i];
	if (val == majority_candidate)
	{
		++votes;
	}
	else 
	{
		--votes;
		if (votes == 0)
		{
			majority_candidate = val;
			votes = 1;
		}
	}
}
```
Why is this Correct?
- a non majority element will receive **at most** `V < N/2` votes in total
- in the worst case, the majority element will cancel `V` votes but will still get at least one more vote making it the majority candidate.




