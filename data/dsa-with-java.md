# DSA with Java (Central Topic)

## 1. Foundations & Analysis
* Complexity Analysis
  * Time Complexity (Big O, Omega, Theta)
    * i:

      ### Time Complexity
      * Count **operations vs input size N**, not wall-clock seconds.
      * Notations:
        * **O** = upper bound / worst-case
        * **Ω** = lower bound / best-case
        * **Θ** = tight bound
      * Simplification rules:
        * Drop constants: $O(2N) \rightarrow O(N)$
        * Keep dominant term: $O(N^2 + N) \rightarrow O(N^2)$

      ```java
      for (int i = 0; i < n; i++) { }      // O(N)
      for (int i = 1; i < n; i *= 2) { }   // O(log N)
      ```

      * Common interview order: $O(1) < O(\log N) < O(N) < O(N\log N) < O(N^2) < O(2^N) < O(N!)$

      *Quick rule:* if interviewer does not specify case, state **worst-case Big-O** first.
  * Space Complexity
    * i:

      ### Space Complexity
      * Count **extra (auxiliary) memory** used by the algorithm.
      * Input storage is usually excluded unless asked explicitly.
      * Typical patterns:
        * $O(1)$: few variables, in-place swap
        * $O(N)$: extra array/map/set/queue
        * recursion: space = **max stack depth**

      ```java
      int sum = 0;              // O(1)
      int[] copy = new int[n];  // O(N)
      ```

      *In Java:* deep recursion can throw `StackOverflowError`; iterative + `ArrayDeque` is safer for large depth.
  * Best, Average, and Worst Cases
    * i:

      ### Best, Average, and Worst Cases
      * **Best case:** minimum work for a favorable input.
      * **Average case:** expected work across typical inputs.
      * **Worst case:** maximum work (default interview answer).

      Example (Linear Search):
      * Best: first element match $\rightarrow O(1)$
      * Average: middle-ish match $\rightarrow O(N)$
      * Worst: last/missing $\rightarrow O(N)$

      *Practical interview line:* "Worst-case is $O(N)$; best-case is $O(1)$."
* Recursion
  * Direct & Indirect Recursion
    * i: Implement functions that call themselves directly or cyclically.
  * Head & Tail Recursion
    * i: Understand call stack optimization for recursive calls at the beginning vs the end of functions.
  * Call Stack & Stack Overflow
    * i: Trace how JVM manages execution frames and prevent stack exhaustion.
* Backtracking
  * Decision State Space Tree
    * i: Visualize recursive decision-making paths for combinatorial problems.
  * Pruning & Feasibility State
    * i: Optimize backtracking by discarding invalid solution paths early.
* Bit Manipulation
  * Bitwise Operators (AND, OR, XOR, NOT)
    * i: Manipulate binary representations directly for low-level optimizations.
  * Shift Operators (Left, Right, Unsigned Right)
    * i: Perform ultra-fast multiplication, division, and sign-preservation using bit shifts.
  * Common Bit Masking Patterns (Get, Set, Clear, Update Bit)
    * i: Code core bitwise utility methods in Java to access or modify specific bits.

## 2. Linear Data Structures
* Arrays
  * Static Arrays
    * i: Implement fixed-size contiguous memory allocation in Java.
  * Dynamic Arrays
    * i: Code a custom ArrayList class from scratch that doubles capacity dynamically.
  * Multi-Dimensional Arrays
    * i: Work with matrices and understand row-major vs column-major storage.
* Linked Lists
  * Singly Linked List
    * i: Build a custom class with sequential Node elements and basic CRUD methods.
  * Doubly Linked List
    * i: Implement bidirectionally linked nodes with next and previous pointers.
  * Circular Linked List
    * i: Create a list where the tail node points back to the head node.
* Stacks
  * Array-Based Stack
    * i: Implement a LIFO stack from scratch using a fixed-size Java array.
  * Linked List-Based Stack
    * i: Implement a LIFO stack with dynamic sizing using custom node elements.
* Queues
  * Simple Queue
    * i: Implement a FIFO queue using arrays with head and tail tracking pointers.
  * Circular Queue
    * i: Solve array memory wastage by wrapping index pointers back to index zero.
  * Deque (Double-Ended Queue)
    * i: Code a versatile queue allowing insertion and deletion at both ends.

## 3. Hierarchical Data Structures
* Binary Trees
  * Standard Binary Tree
    * i: Design hierarchical structures where each node has at most two children.
  * Full, Complete, and Perfect Binary Trees
    * i: Study structural variants of trees and how they impact storage.
  * Binary Tree Traversals (Pre-order, In-order, Post-order, Level-order)
    * i: Implement DFS and BFS tree traversal strategies in Java.
* Binary Search Trees (BST)
  * Standard BST (Search, Insertion, Deletion)
    * i: Build a sorted tree where left child < parent < right child.
  * BST Properties & Validation
    * i: Write a Java algorithm to verify if a binary tree is a valid BST.
* Self-Balancing Trees
  * AVL Trees (LL, RR, LR, RL Rotations)
    * i: Code tree rotations to maintain O(log N) depth dynamically during insertion.
  * Red-Black Trees
    * i: Learn how self-balancing coloring rules govern Java's TreeSet and TreeMap under the hood.
* Heaps
  * Min-Heap & Max-Heap
    * i: Understand complete binary trees where parents are always smaller/larger than children.
  * Array Representation of Heaps
    * i: Map parent-child relationships mathematically to array indices (2i+1, 2i+2).
  * Heapify Operation
    * i: Code bottom-up or top-down restructuring to restore heap invariants.

## 4. Graph Data Structures
* Graph Representations
  * Adjacency Matrix
    * i: Map graph connections using 2D boolean or integer arrays.
  * Adjacency List
    * i: Represent sparse graphs efficiently using an array of lists in Java.
  * Edge List
    * i: Store graph relations as simple lists of coordinate objects.
* Graph Traversals
  * Breadth-First Search (BFS)
    * i: Explore graphs level-by-level using a queue.
  * Depth-First Search (DFS)
    * i: Explore deep down paths using recursion and the call stack.
* Shortest Path Algorithms
  * Dijkstra's Algorithm
    * i: Find single-source shortest path on positive-weighted graphs using PriorityQueue.
  * Bellman-Ford Algorithm
    * i: Handle graphs with negative edge weights and detect negative cycles.
  * Floyd-Warshall Algorithm
    * i: Implement dynamic programming to find shortest paths between all pairs of nodes.
* Minimum Spanning Trees (MST)
  * Prim's Algorithm
    * i: Grow a minimum tree structure greedily node-by-node.
  * Kruskal's Algorithm
    * i: Construct an MST greedily by sorting edges and using a Disjoint Set Union.
* Topological Sorting
  * Kahn's Algorithm
    * i: Sort directed acyclic graphs (DAGs) linearly using in-degree tracking and queues.
  * DFS-Based Topological Sort
    * i: Utilize recursion post-order storage to construct a valid linear dependencies list.

## 5. Hashing
* Hash Functions
  * Characteristics of Good Hash Functions
    * i: Minimize collisions and distribute keys evenly across buckets.
  * Standard Integer & String Hashing
    * i: Study Java's nativehashCode() design and polynomial hashing strategies.
* Collision Resolution
  * Chaining (Open Hashing)
    * i: Resolve collisions by building linked list nodes at array index buckets.
  * Open Addressing (Closed Hashing)
    * i: Implement collision resolution via Linear Probing, Quadratic Probing, or Double Hashing.
* Custom Hash Map Design
  * Internal Array of Nodes
    * i: Write a custom MyHashMap class with basic get() and put() capabilities.
  * Resizing & Rehashing Logic
    * i: Implement capacity doubling and re-index all old elements to avoid collision spikes.

## 6. Core Algorithms
* Searching Algorithms
  * Linear Search
    * i: Scan elements sequentially on unsorted collections.
  * Binary Search
    * i: Implement O(log N) search on sorted arrays using dividing mid-pointers.
  * Ternary Search
    * i: Divide search space into three parts to locate maximums/minimums of unimodal functions.
* Sorting Algorithms
  * Bubble, Selection, and Insertion Sort
    * i: Implement baseline O(N^2) sorting algorithms in Java.
  * Merge Sort
    * i: Code a recursive Divide & Conquer sorting algorithm that guarantees O(N log N) stability.
  * Quick Sort
    * i: Implement an in-place sorting algorithm utilizing partitioning and random pivots.
  * Heap Sort
    * i: Sort collections efficiently by passing elements through a binary heap structure.

## 7. Advanced Algorithm Paradigms
* Divide and Conquer
  * Subproblem Division & Merge Logic
    * i: Break complex problems into independent identical subproblems and combine outputs.
* Greedy Algorithms
  * Local Optimal Choices
    * i: Solve optimization problems by choosing the best immediate, local option at each step.
* Dynamic Programming (DP)
  * Memoization (Top-Down Approach)
    * i: Store recursive computation results in arrays or hash maps to prevent redundant operations.
  * Tabulation (Bottom-Up Approach)
    * i: Solve core base cases first and sequentially build up the DP table.
  * DP State & Transition Equations
    * i: Master writing mathematical formulations that define problem steps.
* Pattern Tracking
  * Two Pointers Pattern
    * i: Utilize two moving indexes on a collection to solve target sum or reversal problems in O(N).
  * Sliding Window Pattern
    * i: Track a sub-segment window of fixed or variable size to optimize array scans.

## 8. Advanced Data Structures
* Trie (Prefix Tree)
  * Node Structure
    * i: Design nodes containing array/Map children pointers and an isEndOfWord flag.
  * Insertion, Search, and StartsWith Prefix Matching
    * i: Implement fast prefix searching for autocomplete engines.
* Disjoint Set Union (DSU / Union-Find)
  * Find and Union Operations
    * i: Group disconnected components and check for cyclic dependencies in O(1) amortized time.
  * Path Compression & Union by Rank
    * i: Optimize DSU trees to remain flat for near-constant time operations.
* Segment Trees
  * Tree Construction (Divide & Conquer)
    * i: Build segment nodes representing ranges of an underlying array.
  * Range Query & Point Update Operations
    * i: Answer range query questions and execute updates in O(log N) time.
* Fenwick Trees (Binary Indexed Tree)
  * Prefix Sum Queries & Point Updates
    * i: Implement a highly memory-efficient array tree using binary index arithmetic.

## 9. Java-Specific Concepts
* Java Collection Framework
  * List, Set, Queue & Deque
    * i: Master how ArrayList, LinkedList, HashSet, PriorityQueue, and ArrayDeque differ structurally.
  * Map Interface
    * i: Understand implementation trade-offs between HashMap, LinkedHashMap, and TreeMap.
* Java Generics in DSA
  * Generic Classes and Methods (<T>)
    * i: Implement custom DSA container classes that handle any reference type.
  * Bounded Type Parameters (<T extends Comparable<T>>)
    * i: Enforce type-safety rules so elements in custom structures are naturally sortable.
* Memory Management & References
  * Java Heap vs Stack Memory
    * i: Understand how Java manages primitives on the stack and references objects on the heap.
  * Object References & Pass-by-Value Mechanics
    * i: Master how pointers are copied during Java function calls to avoid unintended object mutation.
* Custom Sorting Protocols
  * Comparable Interface
    * i: Implement compareTo(T o) directly inside custom data objects for default sorting.
  * Comparator Interface
    * i: Create flexible external sorting rules using custom classes or lambda expressions.