LINKED LIST
===

Linked List:

There is a head: |o|
                  |
                   ----
                      |
                      v                     
Connect to a data   | data |o|--->| data |o|--->| data |o| ... --->| data |x|

The elements in a linked list are called nodes.

A node in a linked list is a structure that has at least 2 fields:
   - the data.
   - the address to the next node.

Node
```
node                                // General dataType:
   data <dataType>                  dataType
   link <pointer>                      key <keyType>
end node                               field1<...>
                                       field2<...>
                                       ...
                                       fieldn<...>
                                    end dataType
```

Node Implemetation in C++ 
```C++
struct Node
{
   int data;
   Node* link;
};

// or

struct Node
{
   float data;
   Node* link;
};

// or we can use template like this

template <class ItemType>
struct Node
{
   ItemType data;
   Node<ItemType>* data;
};

// or we can use class to define the Node, by using class we can initiate the
value beforehand

class Node
{
public:
   int data;
   Node* link;
   Node() // Constructor 1
   {
      this->link = NULL;
   }
   Node( int data )
   {
      this->data = data;
      this->link = NULL;
   }
};
```

Linked list Implementation in C++
```C++
class LinkedList
{
   Node* head; //pointer, identify the head address
   int count;   //counting the number of the list
public:
   LinkedList(); //constructor
   ~LinkedList(); //destructor
};
```

Linked list Operations are:
   - Create empty list
   - Insert a node into list
   - Delete a node from a list
   - Traverse a list
   - Destroy a list

Creating an empty linked list:

Pseudo code:
```
   Algorithm CreateList( ref list <metadata> )
   Initializes metadata for a linked list
   Pre: list is a metadata structure passed by reference
   Post: metadata initialized
      list.head = null
      list.count = 0
   return
   End CreateList
```

Insert a node into list, 4 steps:
1. Allocate memory for the new node and setup the data.
2. Locate the pointer p in the list, which will point to the new node:
   > If the new node becomes the first element of the list then p = list.head.
   > Otherwise p is pPre--link where pPre points to the predecessor of the new
   > node.
3. Point the new node to its successor.
4. Point the pointer p to the new node.

```
Insert to the end by 
   pNew->link = pPre->link
   pPre->link = pNew
```

Pseudo code:
```
   Algorithm InsertNode( ref list <metadata>,
                           val pPre <node pointer>, 
                           val dataIn <dataType> ) 
   Pre: list is metadata structure to a valid list
        pPre is pointer to data's logical predecessor
        dataIn contains data to be inserted
   Post: data have been inserted in sequence
   Return true if successful, false if memory overflow
```
