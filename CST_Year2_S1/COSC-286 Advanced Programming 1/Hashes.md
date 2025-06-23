Associative arrays
- look up values by it's key, not the index
- Also dictionaries, symbol tables and maps

relationship between key and value is *mapping*
Operations of an associative array
- Insert - put a new key/value pair into the array
- Remove - given a key, remove the key/value pair
- Find

## Implementations
Could do a Linked List, but it gives us O(n) search time
Binary search trees could be used as well, but insertions would be slow (self-balancing BST would approach O(log n))
Arrays can be fast if you know the index

### Using arrays for associative arrays
arrays have a lookup time of O(1) if you know the index. What if we could use the key as the index? Almost any value can be converted into an integer somehow

### Transforming keys to indexes
if translating keys to indexes, we would need a very big array
Use modulus to restrict it to a smaller array (Ex. `519 % 12 = 3`, where 12 is the size of the array)
- This is an example of a *Hash function*
- *Hash table/Hash map*

Hash tables have 2 primary parts
- An array, where data (or references to objects) is stored. Each slot is called a *bucket*
- A mapping, or hash function that maps keys to indexes of an array

#### Collisions
When two hash items have the *same index*

Two main ways to reduce them
- Make the table bigger - *Load factor* is how many key/value pairs per bucket
- Use a good hash function that doesn't produce too many collisions

#### Hash Functions
Uniform distribution of values across the whole table
Repeatable
Efficient
worst case is a hash function that tries to put many values in the same location

#### Handling collisions
*Separate Chaining* - Instead of storing the data in the table, we store a reference to a data structure so we can store multiple values in one spot
- Easy to implement
- Can take up a lot of memory

*Probing Algorithms* - AKA Open Addressing - if there's a collision, put it somewhere else in a free space
- Each bucket only stores on element
- Search a well defined sequence (probe sequence) 
	- Ex. "Look 5 buckets ahead"

#### Load Factor and Capacity
Average number of key/value pairs per bucket
*Rehashing* is where we re-hash all of the keys with a bigger array size
*Capacity* is the max number of values given the load limit and the size of the array

### Comparison of methods of implementing an associative arrays
![](Pasted%20image%2020241009114112.png)

### Open Addressing Hash Table
Each entry (bucket) only stores on element
If there is a collision, we find a new location to store the value
Search a well defined sequence of other locations until we find one that's free
- Called a **Probe sequence**

generate an increment and add it to the original hash
Note we will use table sizes for prime numbers - Prevents the situation where an increment divides into the table evenly which could result in an infinite loop

#### Linear Probing Algorithm
uses constant step to find the next position
using an ordinary hash function $h(k)$, a linear probing algorithm would be
$$
h(k, i) = (h(k) + c * i) \text {mod } n
$$
- $h(k)$ is the original hash value
- $n$ is the table size
- $c$ is the step size, or increment value (should be less than the table, typically 1)
- $i$ is the number of attempts (starting at 0)

**Downside is it suffers from clustering - all data values hash to similar location (close proximity)**

