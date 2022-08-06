# Algorithm

Topics include:

- Sorting
    - Selection sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - Insertion sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - Shell sort
        - Time Complextity: O(n(logn)^2)
    - Bubble sort
        - Time Complexity: O(n^2)
        - Space Complexity: O(1)
    - Heap sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(1)
    - Quick sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(n)
    - Merge sort
        - Time Complexity: O(nlogn)
        - Space Complexity: O(n)
    - Radix sort
        - Time Complexity: O(nk)
        - Space Complexity: O(n+k)
    - Bucket sort
        - Time Complexity: O(n+k)
        - Space Complexity: O(n)
- Searching
    - Topological sort
        - Time Complexity: O(V+E)
        - Space Complexity: O(V)
    - Depth first search (DFS)
    - Breadth first search (BFS)
- Recursion
- Hashing
- Dynamic Programming
- Greedy Algorithms
- Linear Programming
- Approximation Algorithms
- Randomization
- NP-completeness


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

### Optimization

- Every element is at most one position off to the right place after two-sorting and three-sorting. Saparate k-sorting function could be implemented for one-sorting (last sorting) which only need one time traversing.
- Implementing the shell sort based on bubble sort could be early stopped by finding no swapping in any single traversing.

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


## Topological sort

Given a directed acyclic graphs(DAG) G = (V, E), topological sort is a linear ordering of all vertices of the DAG such that if G contains an edge <u, v>, u appears before v in the ordering

- Initialize an empty queue and an empty list
- Initialize the in-degree of each node to 0
- Go through adjacency lists of all nodes to count the in-degree of every node
- Go through all the nodes and enqueue every node with in-degree 0
- While queue is not empty
    - Dequeue node v from queue and output it to end of list
    - Reduce the in-degree of all nodes in the adjacency list of v
        - If the in-degree becomes zero, enqueue the node
- The list contains the topological sort order of DAG
- **DFS-based**: 
    - Whenever a node is colored BLACK, insert it in front of linked list
    - Return linked list of vertices (in reverse order of timestamp f[ ])
- Topological sort O(V + E)

## Non-comparison-based sorting

### Counting sort

- An array of n non-negative integers r[0..n-1], with the maximum possible integer being k
    - If integers can be negative, subtract minimum to turn them non-negative
- Space complexity: O(k)
- Time complexity
    - First for-loop, O(k)
    - Second for-loop, O(n)
    - Last double for-loop, O(k + n)
- If k >> n, should not use counting sort

### Bucket sort (hash sort)

- Set up a set of m “buckets” (often an array of linked lists)
- For each item x, compute index of its bucket f(x) {0, ..., m – 1} and place the item in it
- Sort each non-empty bucket (or place the item in 
order in Step 2)
- Put items from non-empty buckets back into array
- All items in one bucket must be greater than those in the preceding buckets and less than those in the following buckets
- Space complexity: O(n + m) to account for linked lists of altogether n items and m buckets
- Time complexity
    - If keys are distributed uniformly over all m buckets and there is only one record per bucket, complexity is O(n+m)
    - In the worst case, O(n2) if there are O(n) records in at least one of the buckets and insertion sort is used to sort each buckets

### Radix sort

- Based on the values of the actual digits (or symbols) in the positional representations of the numbers being sorted
- Determining which of two integers of equal length is 
larger
    - Start at the most significant position and advance through the least significant position as long as the corresponding symbols in the two numbers match
    - The number with the symbol that has a larger magnitude in the first position in which the symbols of the two numbers do not match is the larger of the two numbers
    - If all symbols of both numbers match, the numbers are equal
- Space complexity: O(n)
- Time complexity: O(n * d)

### Which sorting algorithm to use?
- For small or almost sorted input: simple insertion sort
- If input is distributed uniformly, bucket sort is a good choice
- If in-place sorting is not important, quicksort is in general quite efficient


## Hashing

- A search method for finding items in O(1)
- Let the key of an item tell you where to find it, a hash function, h(key), that maps a key to a valid index of an array called hash table
    - Given a key, can retrieve the item from hash table using htable[h(key)] directly
    - O(1) means the time complexity is constant regardless the size of the hash table and the number of items in the table

### Collision resolution

- Separate chaining: collisions are placed outside the hash table with links
    - Load factor: a = n/m
    - Average length of list is a
    - Insertion (of distinct keys) or search: O(1+a)
    - Deletion: O(1+a)
- Coalesced chaining: collisions are placed inside the hash table with links
    - For an unsuccessful search, average number of probes = e^(2a/4) – a/2 + 0.75
    - For a successful search, average number of probes = (e^(2a) – 1)/8a – a/4 + 0.75
- Open adddressing: collisions are placed inside the hash table without links
    - Average number of probes for a successful search: (1/2)*(1 + (1-a)^(-1))
    - Average number of probes for an unsuccessful search:  (1/2)*(1 + (1-a)^(-2))

### Double hashing

- Similar to linear probing as in using a probe sequence based on h(k, i), i starts at 0, and potentially ends at m – 1 if the entire table is filled
- Instead of probe increment of 1 as in linear probing, use h2(k) to provide the increment for probing
- h(k, i) = (h1(k) + i * h2(k)) % m
- Expected cost of unsuccessful search = O(1 + a + a2 + a3 + ...) = O(1/(1 – a))
- Expected cost of successful search is (1/a) * ln(1/(1-a))

### Universal hashing

- A collection H of hash functions is universal if
    - For any two distinct keys x and y, the number of hash functions h belongs to H for which h(x) = h(y) is |H|/m
    - The chance of a collison between x and y when h is chosen randomly from H is 1/m (= |H|/m * 1/|H|)
- Expected number of collisions when hashing n items into m slots (n £ m) is (n – 1)/m < 1
- Chance of collision is 1/m, as desired


## Dynamic Programming

### Greedy vs Divide-and-conquer vs Dynamic programming:
- Greedy: Build up a solution incrementally, myopically optimizing some local criterion.
- Divide-and-conquer: Break up a problem int sub-problems, solve each sub-problem independently, and combine solution to sub-problems to form solution to original problems.
- Dynamic programming: Break up a problem into a series of overlapping sub-problems, and build up solutions to larger and larger sub-problems.



## NP-completeness

### NP Problem

The NP problems set of problems whose solutions are hard to find but easy to verify and are solved by Non-Deterministic Machine in polynomial time.

### P vs NP

It asks whether every problem whose solution can be quickly verified can also be quickly solved.
- The class of questions for which some algorithm can provide an answer in polynomial time is **P**.
- The class of questions for which an answer can be verified in polynomial time id **NP**, which stands for "nondeterministic polynomial time". 

### NP-Hard Problem

A Problem **X** is NP-Hard if there is an NP-complete problem **Y**, such that **Y** is reducible to **X** in polynomial time. NP-Hard problems are as hard as NP-Complete problems. NP-Hard problem need not be in NP class.

***Example:*** Halting problem, Vertex cover problem, etc.

### NP-Complete Problem

A problem **X** is NP-Complete if there is an NP problem **Y**, such that **Y** is reducible to **X** in polynomial time. NP-Complete problems are as hard as NP problems. A problem is NP-Complete if it is a part of both NP and NP-hard problem. A non-deterministic Turing machine can solve NP-Complete problem in polynomial time.

***Example:*** Determine whether a graph has a Hamiltonian cycle, Determine whether a Boolean formula is satisfiable or not, Circuit-satisfiability problem, etc.

