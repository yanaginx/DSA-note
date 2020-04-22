AVL tree
===

### AVL Tree 
- A Binary Search Tree. (BST)
- in which the heights of the left and right subtrees of the root differ by at
  most 1.
- The left and right subtrees are again an AVL Tree.

> AVL Tree is a Binary Search Tree that is balanced tree.

### Balance factor
- Left_higher (LH): Hl = Hr + 1
- Equal height (EH): Hl = Hr
- Right_higher (RH): Hr = Hl + 1

### Balancing Tree:
- When we insert a node into a tree or delete a node from a tree, the resulting
  tree maybe unbalanced. ==> rebalance the tree.
- Four unbalanced tree cases:
   - left of left: a subtree of a tree that is left high has also become left
     high.
   - right of right: a subtree of a tree that is right right has also become
     right high.
   - right of left: a subtree of a tree that is left high become right high.
   - left of right: a subtree of a tree that is right high become left high.

### Rotate right:
```
   20              20                 20            18
  /                /                / /            / \ 
 18         18    /              18   19        12  20
 / \       /      19             /                  /
12 19     12                    12                 19
```

```
Algorithm rotateRight( ref root<pointer> )
Exchanges pointers to rotate the tree to the right.

Pre: root is pointer to tree to be rotated.
Post: node rotated and root updated.

tempPtr = root->left
root->left = tempPtr->right
tempPtr->right = root
return tempPtr

End rotateRight
```

### Rotate left:
```
   20                 22
     \               /  \
     22             20   24
     / \             \
    21  24           21
```
```
Algorithm rotateLeft( ref root<pointer> )
Exchanges pointers to rotate the tree to the left.

Pre: root is pointer to tree to be rotated. 
Post: node rotated and root updated.

tempPtr = root->right
root->right = tempPtr->left
tempPtr->left = root

return tempPtr

End rotateLeft
```

#### Case: left of left
Out of balance condition created by a left high subtree of a left high tree

-> balance the tree by rotating out of balance node to the right.
> left of left -> rotate right on the highest left high unbalance node.

#### Case: right of right
Out of balance condition created by a right high subtree of a right high tree

-> balance the tree by rotating the out of balance node to the left.
> right of right -> rotate left on the highest right high unbalance node.

#### Case: right of left
Out of balance condition created by a right high sbutree of a left high tree

-> balance the tree by 2 steps:
   - rotating the left subtree to the left.
   - rotating the root to the right.
```
   12                               12 -> then rotate right this            8
  /                                /                                       / \
 4 -> rotate left dis 1st         8                                       4   12
  \                              /
   8                            4
```

#### Case: left of right
Out of balance condition created by a left high subtree of a right high tree

-> balance the tree by 2 steps:
   - rotating the right subtree to the right.
   - rotating the root to the left.

```
   12                               12  -> then rotate left dis         13          
     \                                \                                /  \ 
      14 -> rotate right dis           13                             12   14
      /                                 \  
     13                                  14

```

