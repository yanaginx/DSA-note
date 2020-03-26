LIST
=====


Concept

List:

Def: A linear list is a finite, `ordered` sequence of data items known as
elements (the order can be known as the position of the elements).

   | element_1 |----| element_2 |----| element_3 |----...


Linear lists

2 types:
   - General
      -- Unsorted.
      -- Sorted.
   - Restricted (can only append or prepend to the list)
      -- FIFO (queue) <first in first out> 
      -- LIFO (stack) <last in first out>


List ADT:

Def: 

A list of elements of type T is a finite, ordered sequence of elements of
T.

Basic concepts:
   - A list is `empty` when it contains no elements.
   - The number of elements currently stored is the length (size) of the list.
   - The beginning is called the `head`, the end is called the `tail` of the
     list.

Basic operations:
   - Construct a list, leave it empty.
   - Insert an element.
   - Remove an element.
   - Search an element.
   - Retrieve an element. (?) (get the info of the element)
   - Traverese the list, performing given operation on each element.

Extended operations:
   - Determine if the list is empty.
   - Determine if the list is full.
   - Get the size of the list.
   - Clear the list to make it empty.
   - Replace the list's element.
   - Merge two ordered list. (?)
   - Append an unordered list to another.

   - Insertion:
      -- Insert an element to a specified position p in the list.
      -- Insert an element with a given data. (insert to an ordered list)
   - Removal / Retrieval:
      -- Remove / Retrieve at a specified position p 
      -- Remove / Retrieve with a given data.

--------------------

Array Implementation

Dynamically Allocated Array:

3 considered field: 
   - Size
   - Capacity
   - Data

Implementation in C++:
```C++
class DynamicArray 
{
private:
   int size;
   int capacity;
   int *storage;

public:
   //Constructor
   DynamicArray() 
   {
      capacity = 10;
      size = 0;
      storage = new int[capacity];
   }

   //The needed operations 
   //For capacity
   void SetCapacity( int ); //set the capacity;
   void EnsureCapacity( int ); 
   void Pack(); 
   void Trim();
   //For data
   void RangeCheck( int );
   void Set( int, int );
   int Get( int );
   void RemoveAt( int );
   void InsertAt( int, int );
   //
   void Print();
};

void DynamicArray::SetCapacity( int newCapacity )
{
   /*
   Creating a new storage with the capacity of `newCapacity` and replace the
   data of the new one to the old storage and delete the old storage by copying
   and deleting
   */

   int *newStorage = new int[newCapacity];
   memcpy( newStorage, storage, sizeof(int)*size );
   capacity = newCapacity;
   delete[] storage;
   storage = newStorage;
}

void DynamicArray::EnsureCapacity( int minCapacity )
{
   /*
   Ensure the capacity of current array won't smaller than the required
   minCapacity
   */
   
   if ( minCapacity > capacity )
   {
      int newCapacity = (capacity*3)/2 + 1;
      if ( newCapacity < minCapacity )
         newCapacity = minCapacity;
      SetCapacity( newCapacity );
   }
}

void DynamicArray::pack()
{
   /*
      Packing the capacity to the reason able amount according to size 
   */
   if ( size <= capacity/2 )
   {
      int newCapacity = (size*3)/2 + 1;
      SetCapacity( newCapacity );
   }
}

void DynamicArray::trim()
{
   /*
      Trim of the extend capacity, make the capacity = size   
   */
   int newCapacity = size;
   SetCapacity( newCapacity );
}

void DynamicArray::RangeCheck( int index )
{
   if ( index < 0 || index > size )
      throw "Index out of bounds!";   
}

void DynamicArray::Set( int index, int value )
{
   RangeCheck( index );
   storage[index] = value;
}

int DynamicArray::Get( int index )
{
   RangeCheck( index );
   return storage[index]; 
}

void DynamicArray::InsertAt( int index, int value )
{
   RangeCheck( index );
   EnsureCapacity( capacity + 1 );
   int moveCount = size - index;
   if ( moveCount != 0 )
      memmove( storage + index + 1, storage + index, sizeof(int)*moveCount );
   storage[index] = value;
   size++;
}

void DynamicArray::RemoveAt( int index )
{
   RangeCheck( index );
   int moveCount = size - index - 1;
   if ( moveCount != 0 )
      memmove( storage + index, storage + (index + 1), sizeof(int)*moveCount );
   size--;
   Pack();
}
```
Comments:
   - Inserting or Removing operate in O(n).
   - Clear, Empty, Full, Size, Replace and Retrieve in constant time.
