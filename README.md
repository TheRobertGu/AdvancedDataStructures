# AdvancedDataStructures
A collection of exotic &amp; advanced data structures in C++ and Haskell. Also contains small code fragments that don't belong to separate repos, but are worth sharing.

* **d-ary heap**: a generalisation of the binary heap, where every node has *d* children instead of 2. While having basically the same structure and idea as the binary heap, it has better cache behaviour and performs `decreaseKey` quicker, making it a slightly better choice for most purposes. The **4-heap**, specifically, stands out as a good performer. The aforementioned `decreaseKey` is still messy to implement, though, which is why it's missing (for now). All heap modification operations now run in O(log<sub><b>d</b></sub>n) time in the worst case.
* **k-d tree**: a binary space-partitioning tree, containing k-dimensional data (i.e. 3D points ot complex numbers), from where its name arises. Useful for nearest-neighbour (1 or k) and range searches. By using a median-of-medians algorithm for selecting optimal split values, the tree is built balanced in O(nlgn) time, and is done _iteratively_, rather than recursively. Nearest neighbour search is performed in O(lgn) expected time and range search in O(kn<sup>1-1/k</sup>). Heavily optimised for space & cache efficiency, by using **8 bytes per node** in continuous memory, in addition to the data contained.
* **PairingHeap**: a rather simple, fast and efficient multi-way heap, regarded as a simplified Fibonacci heap. Theoretically slower, but in practice much simpler and therefore more efficient than Fibonacci &amp; Binomial heaps, this is most often the best choice for classical algorithms such as Prim's and Dijkstra's. Has user-friendly interface with `decreaseKey` functionality. Time complexities for `insert`, `extractMin` and `decreaseKey` are O(1), O(lgn) and O(lgn) *amortized*, respectively.
* **SkewHeap**: a self-adjusting, leftist heap where every operation is done via skew heap merging. Although there are no structural constraints, it has been shown that all heap modification operations work in O(lgn) *amortized* time.
* **Treap**: **tr**ee + h**eap** = treap. A binary ordered tree where every node has a randomly generated "priority". The values in the nodes form a binary ordered tree, while the priorities in the nodes form a binary heap in the same time. Relies on rotations for moving values (with their respective priorities) up and down the structure, while preserving the BOT invariant. Therefore the tree is roughly well balanced and all modifying operations have O(lgn) *expected* time complexity. Suitable for general-purpose use, such as sets, maps, multisets etc.
* **parallel_sort**: sorts by splitting the input into pieces, sorting the pieces individually (and simultaneously) and and then also merging _in parallel_. Relies on `std::sort` and `std::inplace_merge` and only manages and organizes the multithreaded work. See [`impl::merge_threads()`](https://github.com/Andreshk/AdvancedDataStructures/blob/master/parallel_sort.h#L123) for details.

To-do:
* fix existing structures
* add more structures, such as: Treap and SkewHeap in C++, Persistent Vector, Tiered Vector, (Indexable) SkipList, dense hashset, perfect hashset, Binomial Heap, Splay trees, B-trees, Tries (Radix & Patricia _and_ made persistent), Rope, Suffix Tree, Suffix Array, ~~k-d tree,~~ Fibonacci heap _(dreams are free, right)_ and many more...
