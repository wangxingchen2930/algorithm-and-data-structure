# Data-structure

Topics include:

- stacks
- queues
- linked lists
- trees
    - balanced tree
    - btree
    - red black tree
- graphs
    - minimum spanning trees
    - shortest path

## Linked lists

### Lists vs Array

- Array is more memory efficient (as there is no need to maintain the next field), but requires a contiguous block of memory
- Items in an array can be read and overwritten at any position in O(1) if you know the index, but insertion or removal of an item may take more than O(1) even if you know the index
    - Must also know the size of the array to avoid going out of bound
    - As long as an array is dynamically allocated, it is possible to change the size of the array (subject to availability of contiguous memory for the reallocation of memory)
- Nodes in a list are not stored in contiguous locations
- Not all nodes in a list can be accessed in constant time, but insertion or removal of an item can take O(1) if you know the address of the node before the point of insertion or deletion
    - Can easily shrink or grow a linked list (subject to availability of memory)

### Circular linked lists

- Last node points to the first node
- Instead of storing head address, we maintain only the tail address
- Use sentinel to avoid checking the validity of address

### Doublely-linked lists

- Each node stores data, the address of the next node (in the “next” field), and the address of the previous node (in 
the “prev” field)
- 4 addresses to be updated for insertion and 2 addresses 
for deletion
- Can remove/insert a node easily if address/insertion location is known
- More memory and overhead (management of links)

## Stacks

- LIFO (Last In First Out)

### Implementation

- Linked list
- Array (struct)
    1. Address of the array to store items
    2. Total size of the array (the maximum number of items that can be on the stack)
    3. Index of the stack top
    - Grow the size of the arrsy by a multiplicative factor
    - Shrink the stack by the same factor

## Queues

- FIFO (First In First Out)

### Implementation

- Linked list
- Circular array (struct)
    1. Address of the array to store items
    2. Total size of the array
    3. Index of the queue front
    4. Index of the queue rear

## Priority Queue

- Ascending priority queue: A sequence of dequeue operations remove items in ascending order of levels of priority (lowest or minimum first)
- Descending priority queue: A sequence of dequeue operations remove items in descending order of levels of priority (highest or maximum first)

### Implementation

- tree (heap)
    - A max-heap implements a descending priority queue and a min-heap implements an ascending priority queue
    - O(log n) for enqueue and dequeue, where n is the number of items in the heap

## Trees

- Binary tree height h = O(log n)

### Max heap (descending priority queue)

- In a max heap, the values of the two child nodes are equal to or less than the value of the parent
- The root always contains the maximum value (accessible in O(1))

### Binary tree traversal

- Depth-first
- Breath-first
- Iterative preorder traversal using stack
- Iterative inorder traversal using stack
- Breadth-first traversal using queue

### Threaded binary trees

- A (right in-)threaded binary tree is a binary tree in which every node that does not have a right child has a link to its inorder successor
- The link can be stored in the right pointer, and a binary variable rthread must also be stored in order to tell it is a right child (rthread == 0) or an inorder successor (rthread == 1)
- Useful in order to avoid:
    - Recursion (can search tree only using while loops)
    - Use of stack

### Trie

- Can be used to store a dictionary of words (strings)
- Each node has up to 27 child nodes stored in an array of addresses, each indexed by a character ('\0', 'a', 'b', ..., 'z') 
- Each word (string) is represented by a path from the root node 
- The root node corresponds to an empty string
- Words that share a common prefix will have a common path from the root to the node that corresponds to the prefix

## Height-balanced binary search trees

- Also called AVL trees (Adelson-Velsky and Landis)
- Having a BST that is “balanced” allows the search process to have a worst-case time complexity of O(log n)
- A tree is height-balanced if every node has balance 0, 1, or –1
- Red-black tree is another type of “balanced” tree

### Rotations

- Counter-clockwise rotation (CCR) or left rotation
- Clockwise rotation (CR) or right rotation

### Operations

- Search and insert requires at most 2 rotations to maintain height balanceness
- Deletion may involve rotations at every level from the parent of the deleted node to the root node

## Graph

- Nodes and edges
- Directed graphs
- Adjacency and incidence
- Degrees
- Edge weights
- Path and cycles
    - DAG (directed acyclic graph)
- Connected components
- Strongly connected components
- Adjacency-matrix

### Searching/traversing graph

- Breadth First Search (BFS)
    - Manipulation of queue is necessary
    - Classifying edges by BFS
        - Tree edges: edges in the BF forest
        - Back edges: edges in G connecting a vertex to an ancestor in a BFT
            - Self-loops are back edges
            - No back edges in an undirected graph
        - Cross edges: all other edges
    - O(V + E) operations
    - Applications
        - Determine if an undirected graph is connected and identify 
        - Determine if an undirected graph is cyclic: presence of cross edge within the same tree for undirected graph
        - Find shortest-length path (fewest edges) from one node to another (useful for network flow algorithms)

connected components
- Depth First Search (DFS)
    - Recursion or manipulation of stack is necessary
    - Classifying edges
        - Tree edges: edges in the DF forest
        - Back edges: edges in G connecting a vertex to an ancestor in a DFT
            - Self-loops are back edges
        - Forward edges: nontree edges connecting a vertex to a descendant in a DFT
        - Cross edges: all other edges
            - Forward and cross edges never occur in DFS of undirected graph
    - O(V + E) operations
    - Applications
        - Determine if an undirected graph is connected and identify connected components
        - Identify strongly connected components of a directed graph
        - Determine if a graph is cyclic: presence of back edge
        - Perform topological sort for DAG