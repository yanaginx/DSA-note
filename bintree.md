BINARY TREE
===

## Definition:
> A binary tree node cannot have more than two subtrees.
```

                  a
                 / \
(left subtree)  b   d (right subtree)
               / \   \
              e   f   g   
```

## Binary tree properties
To store *N* nodes in a binary tree:
   - The minimum height: `Hmin = [log2(N)] + 1` or `Hmin = [log2(N + 1)]`
   - The maximum height: `Hmax = N`
The binary tree has the height of *H*:
   - The minimum nodes: `Nmin = H`
   - The maximum nodes: `Nmax = 2^H - 1`
Balance:
   > The balance factor of a binary tree is the difference in height between its
   > left and its right subtree.
   >
   >                 B = Hl - Hr

Balanced tree:
   - Balance factor is 0, 1 or -1.
   - subtrees are balanced.

Complete tree:
`N = Nmax = 2^H - 1`
```
            a
           / \
          b   c
         / \ / \
        d  ef   g

> The last level is full
```

Nearly complete tree:
`H = Hmin = [log2(N)] + 1`
```
            a
           / \
          b   c
         / \ 
        d   e

> Nodes in the last level are on the left  
```

## Binary tree implementation
Linked list implementation (Doubly linked list)
```
node 
   data <itemType>
   left <pointer>
   right <pointer>
end node

binaryTree
   root <pointer>
end binaryTree
```
Array-based implementation (only used for complete tree of nearly complete tree)

## Binary tree traversals
Depth-first traversal: The processing proceeds along a path from the root
through one child to the most distant descendent of that first child before
processing another child, i.e. processes all of the descendents of a child
before moving on to the next child.

Breadth-first traversal: The processing proceeds horizontally from the root to
all of its children, then to its children's children. i.e. each level is
completed before moving on to the next level.

### Depth-first traversal:
Preorder traversal (NLR)
```
      1
     / \
    2   3
```
Inorder traversal (LNR)
```
      2
     / \
    1   3
```
Postorder traversal (LRN)
```
      3
     / \
    1   2
```

__Preorder traversal (NLR)__
```
Algorithm PreOrder (val root <pointer>)
Traverse a binary tree in node-left-right sequence.
Pre: root is the entry node of the tree or subtree
Post: each node has been processed in order

if ( root is not NULL ) then
|   process(root)
|   PreOrder(root->left)
|   PreOrder(root->right)
end
Return
```
__Inorder traversal (LNR)__
```
Algorithm InOrder (val root <pointer>)
Traverse a binary tree in left-node-right sequence.
Pre: root is the entry node of the tree or subtree
Post: each node has been processed in order

if ( root is not NULL ) then
|   InOrder(root->left)
|   process(root)
|   InOrder(root->right)
end
Return
```
__Postorder traversal (LRN)__
```
Algorithm PostOrder (val root <pointer>)
Traverse a binary tree in left-right-node sequence.
Pre: root is the entry node of the tree or subtree
Post: each node has been processed in order

if ( root is not NULL ) then
|   PostOrder(root->left)
|   PostOrder(root->right)
|   process(root)
end
Return
```

### Breadth-first traversal
```
      1
     / \
    2   3
   / \   \
  4   5   6
```
```
Algorithm BreadthFirst(val root <pointer>)
Process tree using breadth-first traversal

Pre: root is the node to be processed.
Post: tree has been processed.

currentNode = root
bfQueue = createQueue()

while (currentNode is not NULL)
| process(currentNode)
|  if (currentNode->left is not NULL)
|  |  enqueue(bfQueue, currentNode->left)
|  end
|  if (currentNode->right is not NULL)
|  |  enqueue(bfQueue, currentNode->right)
|  end
|  if (bfQueue is not empty)
|  |   currentNode = dequeue(bfQueue)
|  end
|  else
|  |   currentNode = NULL
|  end 
end 
destroy(bfQueue)
end breadthFirst
