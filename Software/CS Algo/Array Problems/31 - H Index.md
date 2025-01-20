[274. H-Index](https://leetcode.com/problems/h-index/)

```
int hIndex(vector<int>& citations) {
   int max_citations = 0;

   for (auto c : citations)
   {
       if (c > max_citations) max_citations = c;
   } 

   std::vector<int> papers_per_number_of_citations(max_citations + 1, 0);

   for (auto c : citations)
   {
        papers_per_number_of_citations[c] += 1;
   }

   int total_papers_with_at_least_citations = 0;
   for (auto citations_count = max_citations; citations_count >= 0; --citations_count)
   {
        auto number_of_papers = papers_per_number_of_citations[citations_count];
        total_papers_with_at_least_citations += number_of_papers;
        if (total_papers_with_at_least_citations >= citations_count)
        {
            return citations_count;
        }
   }

   return 0;
}
```

#arrays #accumulate