https://www.geeksforgeeks.org/extended-knapsack-problem/

Choose up to $K$ items that maximize the value given weight capacity $C$ 

#### Optimal substructure:
Optimal solution using $K$ items and capacity $C$ will use the optimal solution for $K-1$ items and some capacity $c < C$ 

```
int boundedKnapsack(int values[], int weights[], int n, int k, int capacity)
{
	// we need to select up to k items
	
	auto rows = k + 1;
	auto cols = capacity + 1;
	std::vector<int> best_solution(rows * cols, 0);

	
    for (auto ii = 0; ii < n; ++ii)
	{
		auto value = values[ii]; 
		auto weight = weights[ii]; 
		
		for (auto kk = 1; kk < k; ++k)
		{
			for (auto jj = capacity; jj >= weight; --jj)
			{
				auto leftover_capacity = jj - weight;
				auto best_subproplem_solution = best_solution[(kk - 1) * cols + leftover_capacity];

				auto& current_best = best_solution[kk * cols + jj];
				auto candidate = best_subproplem_solution + value;
				if (candidate > current_best)
				{
					current_best = candidate;
				}
			}
		}
	}
	
	return best_solution[k * cols + capacity];

}
```