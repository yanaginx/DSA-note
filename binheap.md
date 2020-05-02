BINARY HEAP
====

### Definition:

A Max heap:
- The tree is complete or nearly complete.
- The key value of each node is greater than or equal to the key value in each
  of its descendents.

A min heap:
- The tree is compelete or nearly complete.
- The key value of each node is less than or equal to the key value in each of
  its descendents.

### Heap Data structure ( using array )
For a node located at index _i_, its children are found at:
   - Left child: _2i+1_
   - Right child: _2i+2_

The parent of a node located at index _i_ is located at: floor( (_i_-1)/2 )

Given the index for a left child, _j_, its right sibling, if any, is found at
_j_ + 1. Conversely, given the index for a right child, _k_, its left sibling,
if any, is found at _k_-1.

Given the size of the heap, _N_, of a complete heap, the location of the first
leaf is floor ( _N_/2 )

Given the location of the first leaf element, the location of last nonleaf
element is 1 less.

### Reheap Up and Reheap Down

#### Reheap Up
```
Algorithm reheapUp ( ref heap <array>, val position <integer> )
Reestablishes heap by moving data in postion up to its correct location.

Pre: All data in the heap above is position satisfy key value order of a heap,
except for the data in position.
Post: Data in postition has been moved up to its correct location.

if position > 0 then
   parent = position - 1 / 2
   if heap[position].key > heap[parent].key then
      swap( position, parent )
      reheapUp ( heap, parent )
   end
end
return 

End reheapUp
```
#### Reheap down
```
Algorithm reheapDown ( ref heap <array>, 
```
