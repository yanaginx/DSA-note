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
// value beforehand

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

Algorithm:
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
   > If the new node becomes the first element of the list then `p = list.head`.
   >
   > Otherwise `p is pPre->link` where `pPre` points to the predecessor of the new
   > node.
   >
3. Point the new node to its successor.
4. Point the pointer p to the new node.

```
Insert to the end by 
   pNew->link = pPre->link
   pPre->link = pNew
```

Algorithm:
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

Implementation in C++
```C++
int LinkedList::InsertNode( Node* pPre, int value )
{
   Node* pNew = new Node();
   if ( pNew == NULL )
      return 0;
   pNew->data = value;
   if ( pPre == NULL )
   {
      pNew->link = this->head;
      this->head = pNew;
   }
   else
   {
      pNew->link = pPre->link;
      pPre->link = pNew;
   }
   this->count++;
   return 1;
}
```

Delete a node from a list, 3 steps:
1. Locate the pointer p in the list which points to the node to be deleted (pLoc
   will hold **the node** to be deleted).
   > If that node is the first element in the list: `p is list.head`
   > 
   > Otherwise: `p is pPre->link`, where `pPre` point to the predecessor of the
   > node to be deleted.
2. p points to the successor of the node to be deleted.
3. Recycle the memory of the deleted node.

Algorithm:
```
   Algorithm DeleteNode( ref list <metadata>,
                         val pPre <node pointer>,
                         val pLoc <node pointer>,
                         ref dataOut <dataType>)
   Deletes data from a linked list and returns it to calling module.
   Pre: list is metadata structure to a valid list
        pPre is a pointer to predecessor node
        pLoc is a pointer to the node to be deleted
        dataOut is variable to receive the removed data
   Post: data have been deleted and return to the caller.
```

Implementation in C++
```C++
int LinkedList::DeleteNode( Node* pPre, Node* pLoc )
{
   int result = pLoc->value;
   
   if ( pPre = NULL )
      this-head = pLoc->link;
   else
      pPre->link = pLoc->link;
   
   this->count--;
   delete pLoc;
   return result;
}
```

To be able to find pLoc and pPre, we gotta search through the list to attain
them.

Searching in a linked list:
   - Sequence search
   - Function search of List ADT:

      `<ErrorCode> Search ( val target <dataType>, ref pPre <pointer>, ref pLoc
<pointer> )`

   => Search a node and returns a pointer to it if found.

Successful searches: 3 outcomes:
   - Located first: 
      pPre = NULL; pLoc = target
   - Located middle:
      pPre = pPre; pLoc = target 
   - Located last:
      pPre = pPre; pLoc = target

Unsuccessful searces:

   pPre = pPre; pLoc = NULL

Algorithm
```
```

Implementation in C++
```C++
int LinkedList::Search( int value, Node* &pPre, Node* &pLoc ) 
// gotta use reference because the address value of pPre and pLoc changed
// thoroughly through the search process

{
   pPre = NULL;
   pLoc = this->head;
   while ( pLoc != NULL && pLoc->data != value )
   {
      pPre = pLoc;
      pLoc = pLoc->link;   
   } 
   return (pLoc != NULL); //1 = found, 0 = not found
}
```
