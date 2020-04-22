AVL tree
===

AVL Tree is:
- A Binary Search Tree. (BST)
- in which the heights of the left and right subtrees of the root differ by at
  most 1.
- The left and right subtrees are again an AVL Tree.

> AVL Tree is a Binary Search Tree that is balanced tree.

Balance factor
- Left_higher (LH): Hl = Hr + 1
- Equal height (EH): Hl = Hr
- Right_higher (RH): Hr = Hl + 1

Balancing Tree:
- When we insert a node into a tree or delete a node from a tree, the resulting
  tree maybe unbalanced. ==> rebalance the tree.
- Four unbalanced tree cases:
   - left of left: a subtree of a tree that is left high has also become left
     high.
   - right of right: a subtree of a tree that is right right has also become
     right high.
   - right of left: a subtree of a tree that is left high become right high.
   - left of right: a subtree of a tree that is right high become left high.
