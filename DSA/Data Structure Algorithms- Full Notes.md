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


---

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

---

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
* **Representations**:
  * **Adjacency Matrix**: `O(V²)`
  * **Adjacency List**: O(V + E)
* **Graph Traversals**:
  * **BFS (Queue)** &mdash; `O(V + E)`
  * **DFA (Stack/ Recursion)** &mdash; `O (V + E)`
* **Algorithms**:
  * **Shortest Path**: `Dijkstra`, `Bellman-Ford`, `Floyd-Warshall`
  * **MST**: `Kruskal`, `Prims`
  * **Topological Sort**
  * **Union-Find** (Disjoint Set)

**Application**: Networks, maps, social media, scheduling.


---

## Algorithms
### Searching
- Linear Search: O(n)
- Binary Search: O(log n) (on sorted arrays)

### Sorting
| Sort                               | Time notation                   |
|:-----------------------------------|:--------------------------------|
| **Bubble/ Insertion/ Selection**:  | `O(n²)`                         |
| **Merge Sort**                     | `O(n log n)`                    |
| **Quick Sort**                     | Avg `O(n log n)`, Worst `O(n²)` |
| **Heap Sort**                      | `O(n log n)`                    |
| **Counting/ Radix/ Bucket Sort**   | `O(n + k)`                      |

### Divide and Conquer
* **Break** &rarr; **Solve** &rarr; **Combine**
* **Example**: 
  * `Merge Sort`
  * `Quick Sort`
  * `Binary Search`
  * `Matrix Multiplication`

### Greedy Algorithms
* Make locally optimal choices
* Examples:
  * Activity Selection
  * Huffman Coding
  * Kruskal & Prim (MST)

### Dynamic Programming (DP)

* Solve subproblems, store results to avoid recomputation
* **Properties**
  * Overlapping subproblems
  * Optimal substructure
* **Example**:
  * Fibonacci
  * Knapsack (0/1, fractional)
  * Longest Common Sequence (LCS)
  * Matrix Chain Multiplication

### Backtracking

* Try all possibilities, backtrack if not feasible
* Example: N-Queens, Sudoku, Rat in a Maze

### Advanced Topics
* Bit Manipulation: Subsets, fast operations
* Union-Find (DSU): Connectivity Problems
* String Algorithms: KMP, Rabin-Karp, Z-Algorithm
* Graph Advanced: Tarjan's Algorithm (SCC), Floyd-Warshall

---

## Complexity Classes
* **P**: Problems solvable in polynomial time.
* **NP**: Solutions verifiable in polynomial time.
* **NP-Complete**: Hardest problems in NP.
* **NP-Hard**: At least as hard as a NP-complete

---

## Application of DSA
* **Real-time systems**: `Scheduling`, `OS Processes`.
* **Databases**: `Indexing` (B-Trees, Hashing)
* **AI/ ML**: `Graphs`, `Search Techniques`
* **Networking**: `Routing Algorithms`
* **Web Search**: `Graphs`, `hashing`, `trees`












