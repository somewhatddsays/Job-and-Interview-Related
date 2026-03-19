# Data Structure Algorithms (DSA) &mdash; Full Notes

## Introduction
* **Data Structure (DS)**: A way of organizing and storing data so that it can be accessed and modified efficiently.
* **Algorithm (A)**: A step-by-step finite procedure to solve a program.

### Key Goals
* **Efficiency**:
* **Reusability**: Common structure & algorithms reused across problems.
* **Scalability**: Works on large inputs

### Complexity Analysis
* **Time Complexity**: How execution time grows with input size n.
* **Space Complexity**: Amount of memory required.

**Asymptotic Notations**:
* **Big-O (O)**: Upper bound (worst case).
* **Big-O (&Omega;)**: Lower bound (best case).
* **Big-O (Θ)**: Tight bound (average case)

> **Example growth** <br>
O(1) < O(log n) < O(n) < O(n log n)< O(n2) < O(2<sup>5</sup>) < O(2<sup>n</sup>) < O(n!)


## Basic Data Structure

### Arrays
- Continuous block of memory storing elements of the same type.
- **Operations**:
  - **Access**: O(1)
  - **Insertion/ Deletion**: O(n)
- **Application**: `Lookup tables`, `static data storage`.


### Strings
* Array of characters
* **Operations**:
  * Searching patterns (Naive O(nm), KMP O(n + m))
  * Substring, concatenation, palindrome check.
* **Applications**: `Text processing`, `compilers`, `search engines`.


### Linked List

* Collection of nodes, each with data + pointer to next (and/ or previous)
* **Types**:
  * Singly Linked List
  * Doubly Linked List
  * Circular Linked List


### Stack

* LIFO (Last In, First Out)
* **Operations**:
  * Push
  * Pop
  * Peek (O(1)each)
* **Application**:`Expression evaluation`, `Function call Stack`, `Undo feature`


### Queue

* FIFO (First In, First Out).
* **Operations**:
  * Circular Queue
  * Dequeue
  * Priority Queue
* **Applications**: Scheduling`, `Buffering`, `BFS`


### Hashing
* **Hash Function &rarr; Hast Table**
* Collision handled via:
  * Chaining (Linked List)
  * Open Addressing (Linear/ Quadratic Probing, Double Hashing)
* **Complexity**: 
  * Average O(1)
  * Worst O(n)
* **Application**: `Database`, `Caches`, `Symbol Tables`

## Non-Linear Data Structure

### Trees
* **Hierarchy-based structure** with root & subtrees.

#### Terminology:
* `Root`, `Parent`, `Child`, `Sibling`, `Leaf`, `Height`, `Depth`.

#### Types of Trees:
* **Binary Tree**: Each node &le; 2 children.
* **Binary Search Tree (BST)**: `Left < Root < Right`
* **Balanced Trees**:
  * **AVL Tree** (`balance factor -1/0/1`).
  * **Red-Black Tree** (`self-balancing`).
* **Heap**:
  * **Min-Heap/ Max-Heap** (complete binary tree).
  * Used in Priority Queue.
* **Trie**: Prefix tree for strings.
* **Segment Tree/ Fenwick Tree**: Range queries.

**Applications**:`Expression Trees`, `Indexing`, `Memory Management`, `Compilers`

### Graphs
* Set of Vertices (V) and edges (E).
* **Types**:
  * Directed/ Undirected
  * Weighted/ Unweighted
  * Cyclic/ Acyclic
* Representations:
  * Adjacency Matrix: O(V)
####



### Trees

## Algorithms

