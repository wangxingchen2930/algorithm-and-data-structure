# data-structure

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

## Linked Lists

### Lists vs Array

- Array is more memory efficient (as there is no need to maintain the next field), but requires a contiguous block of memory
- Items in an array can be read and overwritten at any position in O(1) if you know the index, but insertion or removal of an item may take more than O(1) even if you know the index
    - Must also know the size of the array to avoid going out of bound
    - As long as an array is dynamically allocated, it is possible to change the size of the array (subject to availability of contiguous memory for the reallocation of memory)
- Nodes in a list are not stored in contiguous locations
- Not all nodes in a list can be accessed in constant time, but insertion or removal of an item can take O(1) if you know the address of the node before the point of insertion or deletion
    - Can easily shrink or grow a linked list (subject to availability of memory)