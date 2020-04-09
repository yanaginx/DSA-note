TREE
====

## Definition
> A tree consists of a finite set of elements, called *nodes* and a finite set of
> __directed__ lines, called *branches*, that connect the nodes.

## Basic tree concepts
Degree of a nodes: The number of branches associated with the node.

Indegree branch (nhánh vào): Directed branch toward the nodes.
> nhánh hướng tới node đó.

Outdegree branch (nhánh ra): Directed branch away from the nodes. 
> nhánh đi ra từ node đó.
--------------
First node is call the __root__.

Indegree of the __root__ = 0.

Except the __root__, the indegree of a node = 1.

outdegree of a node can be 0, 1 or more.

### Term:
A *root* is the first node with an indegree = 0.

A *leaf* is any node with an outdegree = 0.

An *internal* node is not a root or leaf.

A *parent* has an outdegree > 0.

A *child* has an indegree of 1.

=> An internal node is the parent of a node and the child of an another node.

*Siblings* are two or more nodes that are childs of the same parent node.

For a given node, an ancestor is any node in the path from the root to that
node.

For a given node, a descendent is any node in the path from that node to the leaf.

A *path* is a sequence of nodes in which each node is adjacent to the next one.

The *level* of a node is the distance from the root to that node. 

=> Siblings always have the same level.

The *height* of a tree is the level of the level of the leaf that has the
longest path from the root + 1.

A *subtree* is any connected structure below the root.

