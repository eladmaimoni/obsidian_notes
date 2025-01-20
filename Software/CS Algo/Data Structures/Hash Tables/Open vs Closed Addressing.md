
Closed addressing - 
Open a
# Closed Addressing - Chaining
- same hash-modulo means same bucket
- there are no entries in the table with the same hash / hash modulo
- typically used in std::unoredered map
- each bucket (table entry) contains a pointer to the a list of buckets
- No limit on load (factor) - the table can grow indefinitely 

# Open Addressing

In **open addressing**, all elements are stored within the hash table itself, and there are no external structures like linked lists. When a collision occurs, the algorithm probes the table (i.e., searches for the next available slot) according to a predefined strategy.

#### Key Characteristics:

1. **Single Storage Array**: All data is stored in the hash table array itself.
2. **Collision Resolution by Probing**:
    - **Linear Probing**: Sequentially check the next slots until an empty one is found.
    - **Quadratic Probing**: Use a quadratic function (e.g., $h(k,i)=h′(k)+i^2$ ) to find the next slot.
    - **Double Hashing**: Use a second hash function to determine the step size for probing.
3. **No Secondary Structures**: The entire table can be represented as a flat array.
4. **Load Factor**: Open addressing requires the load factor (fraction of occupied slots) to remain below a critical threshold (e.g., 70%) to maintain performance.

## Probing

**Probing** is a technique used in **open addressing** to resolve hash collisions by searching for an alternative position in the hash table where the key-value pair can be stored. When a collision occurs (i.e., two keys hash to the same bucket), probing systematically checks other slots in the table until an empty slot is found.

#### **Key Concepts of Probing**

1. **Probing Sequence**:
    
    - The order in which slots are examined during a collision resolution is determined by a probing strategy.
    - A good probing sequence minimizes clustering and ensures that all slots are eventually checked.
2. **Probe Functions**:
    - A probe function defines the next slot to check based on the current step in the sequence.
    - It typically depends on the original hash and the probe step.