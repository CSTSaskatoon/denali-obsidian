## What is a Heap
complete binary tree
restricted shape such that every level, except possibly the last, is completely full and the bottom left is filled from the left
A max-heap has the property that every node stores a value that is greater than or equal to the value stored by it's children
Thus, the root stores the max of all values in the tree ( a min-heap stores a value that is less than or equal to all of it's children)
no necessary relationship of children

### Representing a tree as an array
Logically a heap is a tree, but it's represented in memory as an array
Root node is index 0
A node at index *`j`* will have it's left child at *`j*2+1`*, and it's right child at *`j*2+2`*
A node's parent's index will be *`(j-1)/2`*
`{ 50, 41, 33, 18, 39, 22, 32, 20, 3 }`
![](Pasted%20image%2020241204101053.png)

### Making a Heap into a Max-Heap
This is a heap, but not a max-heap. How do we reorder it?
start at the bottom of the tree and find the first parent. trickle the current value down the tree
- repeat the process moving backwards through the tree/heap
- Trickling down any given node takes a max of O(log n) time (height of the tree)
- So doing it for every node takes O(n log n) time (every node * height of the tree)

**Logically these are 1D arrays, I'm just styling it like this to separate layers in the tree**
```
{ 4 }
{ 5, 10 }
{ 7, 8, 2, 9 }
{ A, 6, 3 }

{ 4 }
{ 8, 10 }
{ 7, 5, 2, 9 }
{ A, 6, 3 }

{ 10 }
{ 8, 4 }
{ 7, 5, 2, 9 }
{ A, 6, 3 }

{ 10 }
{ 8, 9 }
{ 7, 5, 2, 4 }
{ A, 6, 3 }
```
Final result is `{ 10, 8, 9, 7, 5, 2, 4, A, 6, 3 }`

### Using a max heap to sort
Top of the tree goes last

**Some stuff here I missed**

### Heapifying an array
```
// Original
{ 10 }
{ 8, 9 }
{ 7, 5, 2, 4 }
{ A, 6, 3 }

// Put the 10 at the bottom
{ 3 }
{ 8, 9 }
{ 7, 5, 2, 4 }
{ A, 6, 10 }

{ 9 }
{ 8, 4 }
{ 7, 5, 2, 3 }
{ A, 6 }

{ 10 } // This is the sorted list

{ 6 }
{ 8, 4 }
{ 7, 5, 2, 3 }
{ A }

{ 9, 10 } // sorted

// 6 can't be on top so we swap it with 8. Then, 6 can't be on top of 7 so we swap it with 7.
{ 8 }
{ 7, 4 }
{ 6, 5, 2, 3 }
{ A }

{ 9, 10 } // sorted

// skipping some steps
{ 7 }
{ 6, 4 }
{ A, 5, 2, 3 }

{ 8, 9, 10 }

{ 3 }
{ 6, 4 }
{ A, 5, 2 }

{ 7, 8, 9, 10 }

// he went too fast for this last part
```

