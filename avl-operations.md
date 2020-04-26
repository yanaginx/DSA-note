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

#### AVL Left Balance algorithm
```
Algorithm leftBalance ( ref root <pointer>, ref taller <boolean> )
This algorithm is entered when the left subtree is higher than the right
subtree.

Pre: root is a pointer to the root of the [sub]tree
     taller is true.
Post: root has been updated (if necessary) 
      taller has been updated

leftTree = root->left

// Case 1: Left of left: single rotation right
if leftTree->balance is LH then
   root->balance = EH
   leftTree->balance = EH
   taller = false
   root = rotateRight(root)
// Case 2: Right of Left: double rotation left on subtree, right on higher
else
   rightTree = leftTree->right
   if rightTree->balance is LH then 
      root->balance = RH
      leftTree->balance is EH
   else if rightTree->balance is EH then
      root->balance = EH
      leftTree->balance = EH
   else 
      root->balance = EH
      leftTree->balance = LH
   end
   rightTree->balance = EH
   root->left = rotateLeft( leftTree )
   root = rotateRight( root )
   taller = false
end
return root
End leftBalance
   
```
#### AVL Right Balance algorithm
```
Algorithm rightBalance ( ref root <pointer>, ref taller <boolean> )
This algorithm is entered when the right subtree is higher than the right
subtree.

Pre: root is a pointer to the root of the [sub]tree
     taller is true.
Post: root has been updated (if necessary) 
      taller has been updated

rightTree = root->right

// Case 1: Right of right: single rotation left
if rightTree->balance is RH then
   root->balance = EH
   rightTree->balance = EH
   taller = false
   root = rotateLeft(root)
// Case 2: Left of Right: double rotation right on subtree, left on higher
else
   leftTree = rightTree->left
   if leftTree->balance is RH then 
      root->balance = LH
      rightTree->balance is EH
   else if leftTree->balance is EH then
      root->balance = EH
      rightTree->balance = EH
   else 
      root->balance = EH
      rightTree->balance = RH
   end
   leftTree->balance = EH
   root->right = rotateRight( rightTree )
   root = rotateLeft( root )
   taller = false
end
return root
End rightBalance
```

### Delete
```
Algorithm AVLDelete ( ref root <pointer>, val deleteKey <key>, ref shorter
<boolean>, ref success <boolean> )
THis algorithm deletes a node from an AVL tree and rebalances if necessary.

Pre: root is a pointer to the root of the [sub]tree 
     deleteKey is the key of node to be deleted.
Post: node deleted if found, tree unchanged if not found
      shorter is true if subtree is shorter
      success is true if deleted, false if not found.
Return pointer to root of (potential) new subtree.

if tree is null then
   shorter = false
   success = false
   return null
end
if deleteKey < root->data.key then
   root->left = AVLDelete( root->left, deleteKey, shorter, success )
   if shorter then 
      root = deleteRightBalance( root, shorter)
   end
else if deleteKey > root->data.key then
   root->right = AVLDelete( root->right, deleteKey, shorter, success )
   if shorter then
      root = deleteLeftBalance( root, shorter )
   end
else
   // deleteNode is a leaf or has 1 child
   deleteNode = root
   if no right subtree then
      newRoot = root->left
      success = true
      shorter = true
      recycle(deleteNode)
      return newRoot
   else if no left subtree then
      newRoot = root->right
      success = true
      shorter = ture
      recycle(deleteNode)
      return newRoot
   // deleteNode has 2 children
   else
      exchPtr = root->left
      while exchPtr->right is not null do
         exchPtr = exchPtr->right
      end
      root->data = exchPtr->data
      root->left = AVLDelete( root->left, exchPtr->data.key, shorter, success )
      if shorter then 
         root = deleteRightBalance( root, shorter )
      end
   end
end
      
```

#### Delete left balance
```
Algorithm deleteLeftBalance ( ref root <pointer>, ref shorter <boolean> )
The (sub)tree is shorter after a deletion on the right branch. Adjust the
balance factors and if necessary, rotate the tree by rotating right.

Pre: tree is shorter
Post: balance factors updated, balance restored 
      root updated
      shorter updated.

if root is RH then 
   root->balance = EH
else if root is EH then
   root->balance = LH
   shorter = false
else 
   leftTree = root->left
   if leftTree is RH then
      rightTree = leftTree->right
      if rightTree is RH then
         leftTree->balance = LH
         root->balance = EH
      else if rightTree is EH then
         root->balance = EH
         leftTree->balance = EH
      else 
         root->balance = RH
         leftTree->balance = EH
      end
      rightTree->balance = EH
      root->left = rotateLeft( leftTree )
      root = rotateRight( root )
   else
      if leftTree is not EH then
         root->balance = EH
         leftTree->balance = EH
      else
         root->balance = LH
         leftTree->balance = RH
         shorter = false
      end
      root = rotateRight( root )
   end
end
return root
End deleteLeftBalance
```
