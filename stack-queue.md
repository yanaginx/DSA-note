Stack & Queue
===

Stack and Queue are Restricted Linear list type

FIFO: Queue

LIFO: Stack

## Stack
Definition: A stack of elements of type T is a finite, ordered sequence of
elements of T, in which all insertions and deletions are restricted to one end,
called the top.

A stack is Last In - First Out (LIFO) data structure.
LIFO: The last to be inserted is the first one to be taken off 

Basic operations:
   - Create
   - Push
   - Pop
   - Top

Stack: push

   Only success when the stack is not full.

Stack: pop
   
   Only success when the stack is not empty.

Stack: top
   
   Get the info of the top element in the stack. Stack remains unchanged.

## Queue
Definition: A queue of elements of type T is a finite, ordered sequence of
elements of T, in which data can only be inserted at one end called the rear,
and deleted at the other end called the front.

A queue is First In - First Out (FIFO) data structure.
FIFO: The first to be inserted is the first one to be taken off.

Basic operations:
   - Create
   - Enqueue: add element to the rear of the queue
   - Dequeue: remove the front element from the queue
   - Front: get the front element
   - Rear: get the rear element

## Impelemnentation for stack and queue
### Stack
Stack is a linked-list implementation where the head of the linked-list is the
top element of the stack.

Stack structure:
```
   stack
      count <integer> : counting the number of the element in stack
      top <node pointer>: identify the top element address
   end stack
```

Stack node structure:
```
   node
      data <dataType>
      next <node pointer>: identify the next element of the current one
   end node
```

Stack: push:

   Inserting the element to the head of linked-list

Stack: pop:

   Delete the head of linked list and assigned the head to the successor of the
deleted node.

### Queue
Queue is also a linked-list implementation where the head of the linked list is
the front of the queue, it's also contain the info of the last element of the
queue.

Queue structure:
```
   queue
      count <integer>: 
      front <node pointer>: point to the front of the queue
      rear <node pointer>: point to the last element of the queue 
   end queue
```

Queue node structure:
   
The same as stack, linked-list node

Queue: enqueue:

- First encounter: Inserting a new element into an empty queue:
   
   The front and rear pointer should contain the address of that first element.

- Second encounter: Inserting a new element into a not empty queue:

   The rear will be pointing to that new element. 

Queue: dequeue:

- First encounter: Removing the last element of the queue:

   The front and rear pointer will be set to NULL

- Second encounter: Removing front element of the queue:
   
   Only the front pointer is updated
   
   Like removing the head of the linked list.
