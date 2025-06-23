Uses Heapsort, quicksort and insertion sort algorithms
Switches between sorts depending on the conditions of the array

## Introspective (Intro)
Uses **quicksort** initially, size of the stack monitored to control recursion
If the stack grows larger than log (n) the sort switches to **heap sort**
When the unsorted part of each partition is small enough, the algorithm switches to **insertion sort**
used by the dotnet's sort

## Tim Sort
hybrid sort that combines merge sort and insertion sort
Finds sequences in the data that are already sorted an uses them to sort the rest more efficiently (since insertion sort works well with already sorted data), and then merges runs of already sorted data together
Works well with real-world data
Did this in Y1S2

## Summary
### Insertion Sort
Simple
Good performance for small arrays even though it's $\color{red}O(n^2)$ in the average case
In place so minimal space requirement
Stable

### Quick Sort
Somewhat complex
Regarded as the best sorting algorithm
$\color{red}O(n \log n)$ performance except in the worst case where it's already sorted ($\color{red}O(n^2)$)
If implemented recursively (usually is) stack overflow might be an issue
Worst case is likely to happen at some point, so median of 3 is good for pivot selection
Even with median of 3, data can be contrived to bog it down
In-place so minimal space requirement
Not Stable for common implementations

### Heap Sort
Somewhat complex
Guaranteed O($n \log n$) regardless of data
in-place so minimal space requirement
Often used in embedded systems where an upper bound on running time and constant upper bound on auxiliary storage can be guaranteed

### Hybrid Sorting
Combining two or more sorting algorithms
