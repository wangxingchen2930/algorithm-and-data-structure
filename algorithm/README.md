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

<<<<<<< HEAD
## Shortest Path Algorithms

### Dijsktra's algorithm

- Initialize d[] = inf except for d[s] = 0
- Iteratively, add a safe node, say u, i.e., d[u] is the lowest among all d[]
    - Add u to partial shortest path tree
    - Tighten if possible all upper bounds of shortest paths of unexplored nodes adjacent to u
- O(V log V) to perform Extract-Min V times
- O(E log V) to update PQ in the worst case E times
- Total time complexity is O(V log V + E log V) = O(E log V)
- Can be improved to O(E + V log V) if we use a Fibonacci heap
=======
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

## Quick sort

### Idea

- Choose a pivot wisely
- Partition array into two subarrays with items less than or equal to pivot, and items greater than (and possibly equal to) pivot (divide)
- Sort two subarrays recursively (conquer)

### Comments

- Not a stable sorting algorithm because of the partition function
- Recursion requires stack space
- Important that the recursive calls are on subarrays that have fewer elements than the original

### Improvement

- Simple insertion sort is faster for smaller arrays, use it when an array is small enough

## Merge sort

### Idea

- Split array into two subarrays of about the same size
- Sort each subarray recursively (if size > 1)
- Merge the sorted subarrays

### Quick sort vs Merge sort vs Heap sort

- Quicksort: “difficult” division, easy combination, preorder
- Mergesort: easy division, “difficult” combination, postorder
- Quicksort is the fastest sorting algorithm in practice
    - Can perform as badly as O(n2)
    - Requires O(log n) stack space
- Mergesort is guaranteed to run in O(n log n)
    - Slower than quicksort on average
    - Requires O(n) additional temporary storage
- Heapsort is guaranteed to run in O(n log n), in-place, and requires no recursions
    - Many real world tests show that heapsort is slower than quicksort (and mergesort) on average
    - Useful for really large problems

### Comments

- Can be stable if merge() is stable
- Advantage: sequential access of data
    - Excellent for external (out-of-core) sorting (e.g. disk)
    - Good cache usage

### Improvement

- By alternating the role of the output array and the auxiliary buffer (and proper initialization), we can avoid the memcpy operations in merge function
>>>>>>> 90328421b168eac61c98db943377aabe00908f08

### Bellman-Ford algorithm

- Edge weights can be **negative**
- Find shortest paths of length at most k (i.e., at most k edges) in iteration k
    - Subpaths of shortest paths are also shortest paths
    - If shortest paths of length k – 1 is known, shortest paths of length k can be computed
    - If no negative cycles, all shortest paths should not have cycles
- Bellman-Ford algorithm can be made to terminate early
- If the longest path length of all shortest paths is k, we need only k+1 iterations
- Each iteration takes O(E)
- In total, O(kE), where k is the longest path length of all shortest paths
- In the worst case, O(VE) time complexity