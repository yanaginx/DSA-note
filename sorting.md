SORTING
====

### SORTING concept

Sorting is one of the most **important concepts** and **common applications** in
computing.

Requirement:
- Sort stability: data with equal key maintain their relative input order in the
  output.
- Sort efficency: a measure of the relative efficency of a sort = number of
  **comparisions** + number of **moves**.

Sorts -> Internal and External( sort outside of memory )
- Internal:
1. Insertion: Insertion and Shell
2. Selection: Selection and Heap
3. Exchange: Bubble and Quick
4. Divide and conquer: Quick and Merge.

#### Insertion Sort

##### Straight Insertion Sort:
The list is divided into 2 parts: sorted and unsorted.

In each pass, the first element of the unsorted sublist is inserted into the
sorted sublist.

```
23 | 78 45 8 32 56
23 78 | 45 8 32 56
23 45 78 | 8 32 56
8 23 45 78 | 32 56
8 23 32 45 78 | 56
8 23 32 45 56 78 |
```
```
Algorithm InsertionSort()
Sorts the contiguous list using straight insertion sort.

if count > 1 then
   current = 1
   while (current < count) do
      temp = data[current] // the data to be inserted to sorted part.
      walker = current - 1
      while walker >= 0 AND temp.key < data[walker].key do 
         data[walker + 1] = data[walker]
         walker = walker - 1
      end
      data[walker + 1] = temp
      current = current + 1
   end
end

End InsertionSort
```

##### Shell Sort
Given a list of _N_ elements, the list is divided into _K_ segments ( _K_ is called
the increment). 

Each segment contains _N/K_ or more elements.

Segments are dispresed throughout the list.

Also is called diminishing-increment sort.

For the value of _K_ in each iteration, sort the _K_ segments.

After each iteration, _K_ is reduced until is is 1 in the final iteration.

###### Choosing incremental values
From more of the comparisions, it is better when we can receive more new
information.

Incremental values should not be multiples of each other, otherwise, the same
keys compared on one pass would be compared again at the next.

The final incremental value must be 1.

```
Algorithm ShellSort()
Sorts the contiguous list using Shell sort.

k = firstincrementalvalue
while k >= 1 do
   segment = 1
   while segment <= k do
      SortSegment(segment, k)
      segment = segment + 1
   end
   k = nextincrementalvalue
end

End ShellSort


Algorithm SortSegment( val segment <int>, val k <int> )
Sorts the segment begeining and segment using insertion sort, step between in
the segment is k.

current = segment + k
while (current < count) do
   temp = data[current] // the data to be inserted to sorted part.
   walker = current - k
   while walker >= 0 AND temp.key < data[walker].key do 
      data[walker + k] = data[walker]
      walker = walker - k
   end
   data[walker + k] = temp
   current = current + k
end

End SortSegment

```

Insertion Sort Efficency

Straight insertion sort:

f(n) = n(n+1)/2 = O(n^2)

Shell sort:

O(n^1.25)

#### Selection Sort 
In each pass, the smallest/largest itme is selected and placed in a sorted list.

##### Selection Sort
The list is divided into 2 parts: sorted and unsorted.

In each pass, in the unsorted sublist, the smallest element is selected and
exchanged with the first element.

```
| 23 78 45 8 32 56
8 | 78 45 23 32 56
8 23 | 45 78 32 56
8 23 32 | 78 45 56
8 23 32 45 | 78 56
8 23 32 45 56 | 78
```

```
Algoritm SelectionSort
Sorts the contiguous list using straight selection sort.

current = 0
while current < count - 1 do
   smallest = current
   walker = current + 1
   while walker < count do 
      if data[walker].key < data[smallest].key then
         smallest = walker
      end
      walker = walker + 1
   end
   swap( current, smallest )
   current = current + 1
end 
End SelectionSort
```

##### Heap sort
The unsorted sublist is organized into a heap.

In each pass, in the unsorted sublist, the largest element is selected and
exchanged with the last element.

Then the heap is reheaped.

Thực hiện downheap từ phần tử không lá đầu tiên

```
Algorithm HeapSort()
Sorts the contiguous list using heap sort.

position = count/2 - 1
while position >= 0 do
   ReheapDown(position, count - 1)
   position = position - 1
end
>> Downheap lần đầu để tìm max đầu tiên
>> O(nlogn)
last = count - 1
while last > 0 do
   swap(0, last)
   last = last - 1
   ReheapDown(0, last - 1)
end
>> O(nlogn)
End HeapSort 
   
```

Selection Sort Efficency:

Selection Sort: O(n^2)

Heap sort: O(nlogn)

#### Exchange Sort
In each pass, elements that are out of order are exchanged, until the entire
list is sorted.

Exchange is extensively used.

##### Bubble Sort 
The list is divided into 2 parts: sorted and unsorted.

In each pass, the smallest element is bubbled from the unsorted sublist and
moved to the sorted sublist. 

```
Algorithm BubbleSort()
Sorts the contiguous list using bubble sort

current = 0
flag = false
while current < count AND flag = False do 
   walker = count - 1
   flag = True
   while walker > current do
      if data[walker].key < data[walker-1].key then
         flag = false
         swap(walker, walker - 1)
      end
   end 
   current = current + 1
end

End BubbleSort
```

Bubble sort efficency O(n^2)

#### Divide and Conquer 
```
Algorithm DivideAndConquer()
if the list has length > 1 then 
   partiion the list into lowlist and highlist
   lowlist.DivideAndConquer()
   highlist.DivideAndConquer()
   combine(lowlist, highlist)
end
End DivideAndConquer
```

MergeSort:
   Easy Partition and Hard to combine

Quick Sort:
   Hard partition but Easy to combine

##### Quick Sort 
```
Algorithm QuickSort()
Sorts the contiguous list using quick sort.

recursiveQuickSort(0, count - 1)
End QuickSort

Algorithm recursiveQuickSort( val left <int>, val right <int> )
Sorts the contiguous list using quick sort. 
Pre: left and right are valid positions in the list
Post: list sorted

if left < right then
   pivot_position = Partition( left, right)
   recursiveQuickSort( left, pivot_position - 1 )
   recursiveQuickSort( pivot_position + 1, right )
end

End recursiveQuickSort
```

Given a pivot value, the partition rearranges the entries in the list as the
following figure:

left < pivot | pivot | right >= pivot 

>> Tìm cách kiếm pivot trên mạng 

Quick Sort efficency: 
   O(nlogn)

##### Merge Sort 
```
Algorithm recursiveMergeSort ( ref sublist <pointer> ) 
Sorts the linked list using recursive merge sort

if sublist is not NULL AND sublist->link is not NULL then 
   Divide ( sublist, second_list )
   recursivemergeSort( sublist )
   recursiveMergeSort( second_list )
   Merge ( sublist, second_list )
end

End recursiveMergeSort


Algorithm Divide ( val sublist <pointer>, val second_list <pointer> )
Divides the list into 2 halves.

midpoint = sublist
position = sublist->link
while position is not NULL do
   position = position->link
   if position is not NULL then
      midpoint = midpoint->link
      position = position->link
   end
end
second_list = midpoint->link
midpoint->link = NULL
End Divide


Algorithm Merge ( ref first <pointer>, val second <pointer> )
Merges 2 sorted lists into a sorted list.

lastSorted = address of combined
while first is not NULL AND second is not NULL do 
   if first->data.key <= second->data.key then 
      lastSorted->link = first
      lastSorted = first
      first = first->link
   else 
      lastSorted->link = second 
      lastSorted = second
      second = second->link
   end
end 

if first is NULL
   lastSorted->link = second
   second = NULL
else
   lastSorted->link = first
   first = NULL
end 

first = combined.link 
End Merge
```
