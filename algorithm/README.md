# Algorithm

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

## Asymptotic notation

Analogy between asymptotic comparison of two functions *f(n)* and *g(n)* and the comparison of two real numbers *a* and *b*;

- <img src="https://render.githubusercontent.com/render/math?math=f(n) = O(g(n)) \approx a \le b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Omega(g(n)) \approx a \ge b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \Theta(g(n)) \approx a = b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = o(g(n)) \approx a < b">
- <img src="https://render.githubusercontent.com/render/math?math=f(n) = \omega(g(n)) \approx a > b">

## Insertion sort

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

## Shell sort

### Idea

- Improving insertion sort
- Allow comparisions and swaps between non-adjacent neighbors
- Perform insertion sort on *k* subarrays of original array
- Iterate the process, use a smaller *k* in each pass
- In the last pass, use k = 1

## Recursion

- A divide-and-conquer technique
- Dynamic programming typically relies on a recursive formulation, but uses an iterative approach to compute (and store) solutions to smaller problems (to avoid repeated computation)

### Order of traversals

- Preorder traversal
    - If the parent node has to pass information to all child nodes
- Inorder traversal
- Postorder traversal
    - If all child nodes have to pass information t a parent node

## Selection sort

### Idea

- Sort by selecting keys (and the associated record) and placing them in their proper (sorted) positions
- On each pass through a unsorted collection, pick the smallest (largest) element in this collection and move it to its proper position

### Comments

- Not faster even for sorted input
- Simple insertion sort is preferred

## Heap Sort

### Idea

- Use a descending heap, a tree implemented using array
- Also called max-heap

### Comments

- It is a priority queue with O(log n) enqueue and dequeue operations
- Array implementation of heap allows in-place sort

### Enqueue element

- Put the new element at the end of the array
- Upward heapify (sifting up)
    - As long as it is larger than its parent, if a parent exists, exchange positions with the parent
    - Similar to to one pass of insertion sort, where we insert the new element into the correct position along the path from the leaf node to the root

### Dequeue operation

- Exchange contents of root node and the last leaf node
- Decrement the heap
- Downward heapify (sifting down)
    - If the new value at the root node is less than its larger child, exchange with the larger child
    - Keep “sifting down” the new value by exchanging with its larger child as long as the larger child is greater
    - Stop when there is no larger child

### Improvement

- Use Downward_heapify to build max-heap
