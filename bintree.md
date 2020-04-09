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
   - The minimum height: `Hmin = log2(N) + 1` or `Hmin = log2(N + 1)`
   - The maximum height: `Hmax = N`
The binary tree has the height of *N*:
   - The minimum nodes: `Nmin = N`
   - The maximum nodes: `Nmax = 2^N - 1`
Balance:
   > The balance factor of a binary tree is the difference in height between its
   > left and its right subtree.
   >
   >                 B = Hl - Hr

Balanced tree:
   - Balance factor is 0, 1 or -1.
   - subtrees are balanced.
