AVL OPERATIONS
===

## AVL tree structures:
```
Node
   data <dataType>
   Node* left <pointer>
   Node* right <pointer>
   balance <balance_factor>
end Node

avlTree
   Node* root <pointer>
end avlTree

dataType
   key <keyType>
   field1 <...>
   field2 <...>
   ...
   fieldn <...>
end dataType
```

## AVL Operations:
- Search
- Insert
- Delete

### Insert
```
Algorithm AVLInsert ( ref root <pointer>, val newPtr <pointer>, ref taller
<boolean> )
Using recursion, insert a node into an AVL tree.

Pre: root is a pointer to first node in AVL tree/subtree
     newPtr is a pointer to new node to be inserted.
Post: taller is a boolean: true indicating the subtree's height has increased,
false indicating the subtree's height unchanged.
Return root returned recursively up the tree.

// Insert at root 
if root is null then 
   root = newPtr
   taller = true
   return root
end
if newPtr->data.key < root->data.key then
   root->left = AVLInsert( root->left, newPtr, taller )
   if taller then
      if root is LH then
         root = leftBalance ( root, taller )
      else if root is EH then
         root->balance = LH
      else 
         root->balance = EH
         taller = false
      end
   end
end
else
   root->right = AVLInsert ( root->right, newPtr, taller )
   if taller then 
      if root is LH then
         root->balance = EH
         taller = false
      else if root is EH then 
         root->balance = RH
      else
         root = rightBalance( root, taller )
      end
   end
end
return root
End AVLInsert
   
```
