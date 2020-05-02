HASHING
===

Traversing: O(n)

Binary search: O(log2n)

Hashing: O(1) complexity in searching 

Home address: address produced by a hash function.

Prime area: memory that contains all the home addresses.

Synonyms: a set of keys that hash to the same location.

Collision: the location of the data to be inserted is already occupied by the
synonym data.

Ideal hashing:
- No location collision
- Compact address space

Collision solution and probing

### Hash functions
- Direct hashing
- Modulo division
- Digit extraction
- Mid-square
- Folding
- Rotation

#### Direct hashing
```
   hash(Key) = Key
```
Pros:
- Key are different -> hash(key) aren't colliding
Cons:
- Memory are huge.

#### Modulo division
```
   hash(Key) = Key mod listSize
```
Fewer collisions if listSize is a prime number.

Example:

   1 000 000 employees to be handled.

   Data space stored up to 300 employees.

   hash(121267) = 121267 mod 307 = 2.
> finding the nearest prime number to reduce the collisions.

#### Digit extraction
```
   hash(Key) = selected digits from Key
```
Example:
```
379452 -> 394
121267 -> 112
378845 -> 388
160252 -> 102
045128 -> 051
```

#### Mid-square
```
   hash(Key) = middle digits of Key^2
```
Example:

9452 * 9452 = 89340304 -> 3403

- Disadvantage: the size of the Key^2 is too large.
- Variations: use only a portion of the key.
Example:
379452 = 394 * 394 = 143641 -> 364.

#### Folding
They key is divided into parts whose size matches the address size.

Example:

Key = 123|456|789

_fold shift_
123 + 456 + 789 = 1368
-> 368

_fold boundary_
321 + 456 + 987 = 1764
-> 764

### Collision resolution 
- Except for the direct hashing, none of the others are one-to-one mapping.
-> Requiring collision resolution methods
- Each collision resolution method can be used independently with each hash
  function.

Collision resolution algorithms
- Opening Addressing
- Linked list resolution

#### Open Addressing
When a collision occurs, an unoccupied element is searched to place the new
element in.

Hash function:
```
h: U -> {0, 1, 2,..., m-1}

U: set of keys
{}: addresses
```
Hash and probe function:
```
hp: U x {0, 1, 2,..., m-1} -> {0, 1, 2,...,m-1}

U x {}: set of keys and probe numbers
{}: addresses
```

Inserting:
```
Algorithm hashInsert( ref T <array>, val k <key> )
Insert key k to table T.

i = 0
while i < m do 
   j = hp(k, i)
   if T[j] = nil (not in list) then
      T[j] = k
      return j
   else
      i = i + 1
   end
end
return error: "hash table overflow"

End hashInsert 
```

Searching: 
```
Algorithm hashSearch( ref T <array>, val k <key> )
Search key k in table T.

i = 0
while i < m do
   j = hp(k, i)
   if T[j] = k then
      return j
   else if T[j] = nil then
      return nil
   else
      i = i + 1
   end
end
return nil
End hashSearch
```

There are different methods to impelement hp:
- Linear probing
- Quadratic probing
- Double hashing
- Key offset

##### Linear probing
When a home address is occupied, go to next address ( the current address + 1 ):
```
   hp(k,i) = ( h(k) + i ) mod m 
```
##### Quadratic probing
When a home address is occupied, increase the address by the collision probe
number squared: 
```
   hp(k,i) = ( h(k) + i^2 ) mod m 
```

##### Double hashing
```
hp(k,i) = ( h1(k) + ih2(k) ) mod m
```

##### Linked list resolution
If collision, add the key into a linked list.
