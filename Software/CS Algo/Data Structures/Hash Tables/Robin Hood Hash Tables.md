BEST ARTICLE:
https://programming.guide/robin-hood-hashing.html
### Brief
- we use open addressing. an array of key value pairs
- 'home index' - given a key, this is the original "bucket" or slot it maps to
- 'actual index' - the actual slot
- we keep track of 'probe sequence length' (PSL) - each slot contains metadata that holds the distance from the 'home index'
- we update the PSL on each insert and deletion

### Robin Hood Concept
Robin Hood hashing takes buckets from entries that are closer to their initial buckets compared to the entries that need to be inserted. In that way, it takes from the riches and gives to the poor, which is where the name “Robin Hood hashing” originates.

Meaning:
- when inserting a key-value to the table, we always start searching for a slot at the 'home index'
- if we reach the end of the block (of keys that were mapped to the same home index), then we put the element at the end of this block
- if the end of the block is not empty, we shift all the elements of the next block by 1 to the right
- the first element of the next block has a lower PSL than ours (he has PSL = 1) so we can view this as stealing from the rich (rich = closer to the home index)

Intuition:
- when we steal the place from elements that are closer to their home index, we sort of 'balance' the access time of the table

### Probe Sequence
- the list of entries we need to loop over when looking for a key-value or inserting
- Note, that even in cases where we shift entries, the PSL is still counted from the home index
- So, we may have cases where in the home index, we will have a PSL larger than 1, that belongs to the previous block


### Insert Key-Val
1. compute hash
2. find the 'home index' (bucket, slot)
3. linearly search for a bucket whose PSL index is smaller than 

#### Example 1:
block is NOT occupied by pervious block elements, but its end is not empty

- we want to insert the key 25 that maps to slot 3 (home index)
- we start at the home index, (where ideally we should have PSL = 1)
- we iterate on entries until the found PSL is smaller than `i` (our counter)
- in the following case, it is at index 7, where `i = 4` and PSL is 1

| 0   | 1   | 2   | 3     | 4    | 5     | 7     | 8    | 9   | 10  |
| --- | --- | --- | ----- | ---- | ----- | ----- | ---- | --- | --- |
|     |     |     | 76, 1 | 33,2 | 42, 3 | 14, 1 | 22,2 |     |     |

- now we insert our element to slot 7, and look for a place to insert (14, 1)
- this means we set `i = 1` and start looking for a place to put 14 using the same method

| 0   | 1   | 2   | 3     | 4    | 5     | 7     | 8    | 9     | 10  |
| --- | --- | --- | ----- | ---- | ----- | ----- | ---- | ----- | --- |
|     |     |     | 76, 1 | 33,2 | 42, 3 | 25, 4 | 22,2 | 14, 3 |     |
#### Example 2:
Previous block occupies the home index

- it is exactly the same process, but we 'skip' all the elements of the previous block
- our `i` is always smaller than the PSL of the previous block index

### Find Key
- we start at the 'home index' for this key
- we keep a counter `i` and look for the hash
- if the previous block extends to this block, we will find a larger PSL than `i` 
- if the PSL of the entry we are examining is smaller than `i`, it means that it belongs to a later key and the search may stop. this includes empty slots that has PSL 0.

Deleting
- we can't cut off the probe sequence
- so we either have to keep the deleted entries metadata (tombstone) and mark them as deleted
- or we can remove them and backward shift whatever comes after them
- 