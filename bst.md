Binary Search Tree (BST)
=====

A binary search tree is a binary tree with the following properties:
- All items in the left subtree has their value less than the value of the root.
- All items in the right subtree has their value greater than or equal to the value of the root.
- Each subtree is itself a binary search tree. 

Valid BST:
```
   17                17
   (a)              /  \
                   8   19
                    (b)
    17         17          17
   /          /  \           \
  6          6   19          19
 /          / \                \
3          3  14               22
(c)           (d)            (e) 

```

## BJT Traversal
```
            23
           /   \
          18    44
         /  \   / \
        12  20 35  52
```
Preorder Traversal: 23 18 12 20 44 35 52

Inorder Traversal: 12 18 20 23 35 44 52 

Postorder Traversal: 12 20 18 35 52 44 23

If using Inorder Traversal, we can have a list with its value increase from
smallest to the largest.

### Find the smallest and largest Node in the BST
Find smallest:
```
Algorithm findSmallestBST( val root <pointer> )
This algorithm finds the smallest node in a BST.
Pre: root is a pointer to a nonempty BST or subtree.
Return address of the smallest node.

if root->left = NULL then 
|  return root
end
return findSmallestBST( root->left )
End findSmallestBST
```

Find largest:
```
Algorithm findLargestBST( val root <pointer> )
This algorithm finds the largest node in a BST.
Pre: root is a pointer to a nonempty BST or subtree.
Return address of the largest node.

if root->right = NULL then 
|  return root
end
return findLargestBST( root->right )
End findLargestBST
```
### Binary search
```
Recursive search

if root is NULL
|  then return null
end

if ( target < root->data.key ) then
|  return searchBST( root->left )
else if ( target > root->data.key ) then
|  return searchBST( root->right )
else 
|  return root
end

End searchBST

or Iterative search

while ( root is not NULL ) AND ( root->data.key != target ) do
|  if ( target < root->data.key ) 
|  |  root = root->left
|  else 
|  |  root = root->right
|  end
end while
return root 

End searchBST
```

### Insert Node into BST
Iterative insert
```
Algorithm iterativeInsertBST ( ref root <pointer>, val new <pointer> )
Insert node containing new data into BST using iteration.

Pre: 
   root is address of first node in a BST
   new is address of node containing data to be inserted.

Post: new node inserted into the tree.

if ( root is NULL ) then
|  root = new
else
|  pWalk = root
|  while pWalk not NULL do
|  |  parent = pWalk
|  |  if new->data.key < pWalk->data.key then 
|  |  |  pWalk = pWalk->left
|  |  else
|  |  |  pWalk = pWalk->right
|  |  end
|  end
|  if new->data.key > parent->data.key then
|  |  parent.right = new
|  else 
|  |  parent.left = new
end

End interativeInsertBST

```

Recursive insert

>> Truyền bằng root bằng tham khảo rồi chạy tay thử 

```
Algorithm recursiveInsertBST ( ref root <pointer>, val new <pointer> )
Insert node containing new data into BST using recursion

Pre:
   root is address of current node in a BST.
   new is address of node containing data to be inserted.
Post:
   new node inserted into the tree

if root is null then
|  root = new
else
|  if root->data.key > new->data.key then
|  |  recursiveInsertBST ( root->left, new )
|  else
|  |  recursiveInsertBST ( root->right, new )
|  end
end
return

End recursiveInsertBST
```

## Delete node
Deletion of a leaf: Set the deleted node's parent link to NULL.

Deletion of a node having only right subtrees or left subtrees: Attach the
subtree to the deleted node's parent.

Deletion of a node having both subtrees: Replace the deleted node by its
predecessor or by its successor, recycle this node instead.


>> Using the largest node on the left or using the smallest node on the right
>> subtree of the node u want to delete.

```
Algorithm deleteBST( ref root <pointer>, val dltKey <keyType> )
Deletes a node from a BST

Pre: 
   root is pointer to tree containing data to be deleted.
   dltKey is key of node to be deleted.

Post:
   node deleted and memory recycled if dltKey not found, root unchanged.

Return 
   true if node deleted, false if not found.

if root is NULL then 
|  return false
end
if dltKey < root->data.key then
|  return deleteBST ( root->left, dltKey )
else if dltKey > root->data.key then
|  return deleteBST ( root->right, dltKey )
else
|  // Deleted node found - Test for leaf node
|  if root->left is null then
|  |  dltPtr = root
|  |  root = root->right
|  |  recycle(dltPtr)
|  |  return true
|  else if root->right is null then
|  |  dltPtr = root
|  |  root = root->left
|  |  recycle(dltPtr)
|  |  return true
|  else
|  |  //Deleted node is not a leaf.
|  |  //Find the large node on the left subtree
|  |  dltPtr = root->left
|  |  while dltPtr->right is not NULL do
|  |  |  dltPtr = dltPtr->right
|  |  end
|  |  // Node found. Move data and delete leaf node
|  |  root->data = Ptr->data
|  |  return deleteBST( root->left, dltPtr->data.key )
|  end
end

End deleteBST
```
