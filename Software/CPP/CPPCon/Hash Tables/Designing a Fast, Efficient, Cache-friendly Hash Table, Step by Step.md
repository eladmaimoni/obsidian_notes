https://www.youtube.com/watch?v=ncHmEUmJZf4

see also:

https://martin.ankerl.com/2016/09/15/very-fast-hashmap-in-c-part-1/

https://programming.guide/robin-hood-hashing.html

https://codecapsule.com/2013/11/11/robin-hood-hashing/

https://www.youtube.com/watch?v=IMnbytvHCjM
### std::unoredered_map
- typical implementation contains a vector of pointers into the bucket chain
- the bucket chain is limited in size, so when we have a key-hash, we modulo it in order to access the correct bucket array 
- the bucket array is a linked list (BAD!) with all the values that have the same key hash modulo
- an entry in a bucket is a value, but usually this entry has the unique hash code (key) along side it
- i think we also need to store the key, since 2 unique keys may have the same hash

Removing the dummy element from the bucket chain
- the buckets chain is a linked list
- it has a dummy element (the previous linked list end) so we can both iterate it in o(n) and so we can insert the new bucket to the beginning of the linked list
- if we change the bucket implementation to not have the dummy element, we save space but lose the advantages above
Removing the computed hash from the bucket chain
- we still store the key-val
- but we now have to recompute the hash of all the buckets in the chain upon find
- also, when rehashing the map, we need to recompute all hashes
- comparing raw keys for find may be expensive (string)
- but we reduce the required space

Tombstone Concept
- we store hash-modulo-key-val in a contiguous array
- when concatenate elements with the same value to be right after the other
- when we delete an element, we put a special value there (tombstone) that basically means - keep looking
Tombstone tradeoffs:
- rehashing heuristics are harder or non deterministic if we keep the tombstone as counted elements

Lessons:
1. iterating std::unoredered_map is SLOW - the key value pairs are arranged in a linked list