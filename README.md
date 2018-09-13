# AdvancedDataStructures
A collection of exotic &amp; advanced data structures in C++ and Haskell. Also contains small code fragments that don't belong to separate repos, but are worth sharing.

* **Binary heap (static)**: A modification to the classic data structure, supporting `decreaseKey` and optimized specifically for Prim's and Dijkstra's algorithms: the total number of values is predetermined and no values are added/removed after initialization. Uses two "pointers" per node. Time complexities are O(lgn) for `extractMin` and `decreaseKey` and O(n) for construction/initialization (a trivial operation).
* **Cartesian tree**: a _static_ binary tree with min-heap properties, constructed from a given array of values. Here static means that after construction no insertion/deletion operations may be performed, only lookups & queries. What's special here is the **O(n)** on-line construction algorithm, which maintains the "right spine" of the tree at every iteration, using it to achieve amortized O(1) insertion time per element. Other uses will be added later.
* **d-ary heap**: a generalisation of the binary heap, where every node has *d* children instead of 2. While having basically the same structure and idea as the binary heap, it has better cache behaviour and performs `decreaseKey` quicker, making it a slightly better choice for most purposes. The **4-heap**, specifically, stands out as a good performer. The aforementioned `decreaseKey` is still messy to implement, though, which is why it's missing (for now). All heap modification operations now run in O(log<sub><b>d</b></sub>n) time in the worst case.
* **k-d tree**: a binary space-partitioning tree, containing k-dimensional data (3D points or complex numbers, for example), from where its name arises. Useful for nearest-neighbour (1 or k) and range searches. By using a median-of-medians algorithm for selecting optimal split values, the tree is built balanced in O(nlgn) time, and is done _iteratively_, rather than recursively. Nearest neighbour search is performed in O(lgn) expected time and range search in O(kn<sup>1-1/k</sup>). Heavily optimised for space & cache efficiency, it keeps the nodes in continuous memory and uses as little as **8 bytes per node** (in addition to the data contained, of course).
* **PairingHeap**: a rather simple, fast and efficient multi-way heap, regarded as a simplified Fibonacci heap. Theoretically slower, but in practice much simpler and therefore more efficient than Fibonacci &amp; Binomial heaps, this is most often the best choice for classical algorithms such as Prim's and Dijkstra's. Has a user-friendly interface with `decreaseKey` functionality. Time complexities for `insert`, `extractMin` and `decreaseKey` are O(1), O(lgn) and O(lgn) *amortized*, respectively. The [`pairing_heap_static`](https://github.com/Andreshk/AdvancedDataStructures/blob/master/pairing_heap_static.h) is a variant of this structure, optimized precisely for use in the aforementioned algorithms (similarly to [`binary_heap_static`](https://github.com/Andreshk/AdvancedDataStructures/blob/master/binary_heap_static.h)): the total number of values is predetermined, memory is allocated once for all nodes and also deallocated once (instead of per-node), all nodes are contained inside this continuous space and no values are added/removed after initialization.
* **SkewHeap**: a self-adjusting, leftist heap where every operation is done via skew heap merging. Although there are no structural constraints, it has been shown that all heap modification operations work in O(lgn) *amortized* time.
* **Static hashset**: hashing a static set of values in O(n) storage with *no collisions*. The values hashed are required to be in \[0;p) for a prime number p (can be chosen according to the use case). The total space used is for approx. 5n elements. The only meaningful operation supported is querying whether or not a value is in the set and is performed in, of course, O(1) time.
* **Treap**: **tr**ee + h**eap** = treap. A binary ordered tree where every node has a randomly generated "priority". The values in the nodes form a binary ordered tree, while the priorities in the nodes form a binary heap in the same time. Relies on rotations for moving values (with their respective priorities) up and down the structure, while preserving the BOT invariant. Therefore the tree is roughly well balanced and all modifying operations have O(lgn) *expected* time complexity. Suitable for general-purpose use, such as sets, maps, multisets etc.
* **X-fast trie**: a static data structure, supporting searching for a value's predecessor/successor in a given, fixed set of values in just O(**lglgm**) time (where `m` is the maximum value in the set). Constructed in O(nlgm) time and takes O(n) space. The name comes from the trie, constructed during initialization. Due to being static (i.e. no addition/removal of values after construction) the "pointers" from each node in the trie are replaced by indices, used during the search operations, and as a result the finished structure does not actually contain a trie. In order to hit O(lglgm) as a hard, non-amortized bound, it relies on being able to hash perfectly a given, fixed set of integers (currently not supported).

To-do:
* fix existing structures
* add more structures, such as: Treap and SkewHeap in C++, Persistent Vector, Tiered Vector, (Indexable) SkipList, dense hashset, ~~perfect hashset~~, perfect dynamic hashset, Binomial Heap, Splay trees, B-trees, Tries (Radix & Patricia _and_ made persistent), Rope, Suffix Tree, Suffix Array, ~~k-d tree,~~ Fibonacci heap _(dreams are free, right)_ and many more...
