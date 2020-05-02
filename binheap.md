BINARY HEAP
====

### Definition:

A Max heap:
- The tree is complete or nearly complete.
- The key value of each node is greater than or equal to the key value in each
  of its descendents.

A Min heap:
- The tree is compelete or nearly complete.
- The key value of each node is less than or equal to the key value in each of
  its descendents.

### Heap Data structure ( using array )
For a node located at index _i_, its children are found at:
   - Left child: _2i+1_
   - Right child: _2i+2_

The parent of a node located at index _i_ is located at: [(_i_-1)/2]

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
Algorithm reheapDown ( ref heap <array>, val position <integer>, val
lastPosition <integer> )
Reestablishes heap by moving data in position down to its correct location.

Pre: 
   All data in the subtree of position satisfy key value order of a heap,
except the data in position.
   lastPosition is an index to the last element in heap.
Post: Data in position has been moved down to its correct location.

leftChild = position*2 + 1
rightChild = position*2 + 2
if leftChild <= lastPosition then
   if ( rightChild <= lastPosition ) AND ( heap[rightChild].key >
heap[leftChild].key ) then
      largeChild = rightChild
   else
      largeChild = leftChild
   end
   if heap[largeChild].key > heap[position].key then
      swap ( largeChild, position )
      reheapDown( heap, largeChild, lastPosition )
   end
end
return 
End reheapDown 
```

### Build a heap
```
Algorithm buildHeap ( ref heap <array>, val size <integer> )
Given an array, rearrange data so that they form a heap.

Pre: heap is array containing data in nonheap order
     size is number of elements in the array.
Post: array is now a heap.

walker = 1
while ( walker < size ) do
   reheapUp ( array, walker )
   walker = walker + 1;
end
End buildHeap 
```

### Insert a node into heap
```
Algorithm insertHeap ( ref heap <array>, ref last <integer>, val data <dataType>
)
Inserts data into heap.

Pre: 
   heap is a valid heap structure.
   last is reference parameter to last node in heap.
   data contains data to be inserted.
Post: 
   data have been inserted into heap.
Return true is successful, false if array is full

if ( heap full ) then
   return false
end
last = last + 1
heap[last] = data
reheapUp( heap, last )
return true

End insertHeap
```

### Delete a node from heap
```
Algorithm deleteHeap ( ref heap <array>, ref last <integer>, ref dataOut
<dataType> )
Deletes root of heap and passes data back to caller

Pre:
   heap is a valid heap structure
   last is reference parameter to last node
   dataOut is reference parameter for output data
Post:
   root deleted and heap rebuilt
   root data placed in dataOut

if ( heap empty ) then
   return false
end
dataOut = heap[0]
heap[0] = heap[last]
last = last - 1
reheapDown ( heap, 0, last )
return true

End deleteHeap
```

Complexity of Binary heap operations:
- reheapUp: O(log2n)
- reheapDown: O(log2n)
- Build a heap: O(nlog2n)
- Insert a node into heap: O(log2n)
- Delete a node from heap: O(log2n)

Common applications:
- selection algorithms
- priority queues
- sorting.
