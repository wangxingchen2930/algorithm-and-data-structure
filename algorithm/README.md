# algorithm

Topics include:

- sorting
    - selection sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - insertion sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - shell sort
    - bubble sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - heap sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(1)
    - quick sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(n)
    - merge sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(n)
    - radix sort
        - Time Complexity: O(nk)
        - Space Complexity: O(n+k)
    - bucket sort
        - Time Complexity: O(n+k)
        - Space Complexity: O(n)
    - topological sort
        - Time Complexity: O(V+E)
        - Space Complexity: O(V)
- searching
- recursion
- hashing

## Asymptotic Notation

Analogy between asymptotic comparison of two functions *f(n)* and *g(n)* and the comparison of two real numbers *a* and *b*;

- <img src="https://render.githubusercontent.com/render/math?math=f(n) = O(g(n)) \approx a \le b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(g(n)) \approx a \ge b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Theta(g(n)) \approx a = b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = o(g(n)) \approx a < b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \omega(g(n)) \approx a > b">

## Insertion Sort

### Idea

- Insert an item into an already sorted array
- Compare item with items in the sorted array from largest to smallest
    - If reverse order, swap items
- Continue until all items are sorted

### Comments

- Only neighbors are swapped and idential items are never exchanged
    - Thus, insertion sort is stable, i.e., the relative positions of identical items do not change
- The algorithm builds up a sorted subarray at the start and successively inserts items into it
- Move up array to find proper position to insert it

### Improvements

- Select and swap the minimum item with the first item (no longer stable)
- Use binary search to find corrrect position
- Use memmove() to move all items (to make room for insertion) "at the same time"

## Shell Sort

### Idea

- Improving insertion sort
- Allow comparisions and swaps between non-adjacent neighbors
- Perform insertion sort on *k* subarrays of original array
- Iterate the process, use a smaller *k* in each pass
- In the last pass, use k = 1

