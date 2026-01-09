# Comprehensive study notes for the Pannon University (MIK) Programming BSc exam
This document follows the thematic list provided in the uploaded exam syllabus (source above). Each section contains definitions, key theorems, algorithm descriptions, complexity estimates, construction outlines, exam-oriented examples, and short answer templates you can memorize or adapt in an oral exam.

---

## Számításelmélet (Computation theory)

### 1. Regular languages
**Definitions**
- Alphabet Σ, strings Σ*, language L ⊆ Σ*.
- Regular expression (RE): syntax and semantics (ε, ∅, single letters, concatenation, union, Kleene star).
- Deterministic Finite Automaton (DFA): 5-tuple (Q, Σ, δ, q0, F). Acceptance by final state.
- Nondeterministic Finite Automaton (NFA): transitions to sets of states; ε-transitions allowed.
- Language class: REG = languages recognized by some (D)FA / described by RE.

**Equivalences / Constructions**
- NFA → DFA: subset (powerset) construction; DFA states correspond to subsets of NFA states; proof of language equivalence by simulation.
- RE → NFA: Thompson construction (build small NFAs for atomic expressions; combine with ε-transitions).
- NFA → Regular expression: state elimination method (optional).
- Closure properties: REG closed under union, concatenation, star, complement, intersection, difference, homomorphism, inverse homomorphism.

**Key lemmas and limits**
- Pumping lemma for regular languages: statement and typical usage to prove non-regularity (choose p, consider a string of length ≥ p, decompose s = xyz with |xy| ≤ p, |y| > 0, and show contradiction).
- Myhill–Nerode theorem (conceptual): minimal DFA states correspond to distinct equivalence classes; provides a necessary-and-sufficient method for regularity and minimization.

**Exam tip / short answer**
- To show L is regular: give RE, or construct DFA/NFA, or closure from known regular languages.
- To show non-regular: use pumping lemma or Myhill–Nerode.

---

### 2. Context-free languages (CFLs)
**Definitions**
- Context-free grammar (CFG): G = (V, Σ, R, S); productions A → α, A ∈ V, α ∈ (V ∪ Σ)*.
- Derivations, parse trees, leftmost/rightmost derivation.
- Pushdown automaton (PDA): nondeterministic PDA recognizes CFLs; stack provides unbounded but structured memory.

**Equivalences / Constructions**
- CFG → PDA: construct PDA that simulates leftmost derivation by pushing RHS of productions (classical construction).
- PDA → CFG: convert by enumerating derivations between stack symbols (less commonly required).

**Properties**
- Chomsky Normal Form (CNF): productions A → BC or A → a (plus S → ε). CNF conversion algorithm (eliminate ε-productions, unit productions, useless symbols).
- Closure properties: CFLs closed under union, concatenation, Kleene star. Not closed under intersection or complement (intersection with regular languages OK).
- Pumping lemma for CFLs (the "second" pumping lemma): used for proving non-CFL (different from regular pumping lemma).

**Parsing**
- CYK algorithm (for grammars in CNF): dynamic programming O(n^3) to determine membership.
- LL(1) vs LR parsing (conceptual difference: predictive vs bottom-up).

**Exam tip**
- To prove a language is CFL: give grammar or PDA. To prove non-CFL: apply pumping lemma for CFLs or show intersection with a regular language yields a known non-CFL.

---

### 3. Turing-recognizable and decidable languages
**Definitions**
- Turing Machine (TM): formal 7-tuple (Q, Σ, Γ, δ, q0, B, F), infinite tape, head, deterministic or nondeterministic.
- Accepting vs halting: a TM accepts input if there exists a computation that halts in an accepting state. Language is Turing-recognizable (recursively enumerable) if some TM accepts exactly L. Decidable (recursive) if a TM halts on all inputs and accepts exactly L.
- Characteristic function vs partial characteristic function.

**Machine-schema examples**
- Copier TM, shift TM, machine that decides a^n b^n c^n (non-context-free) — outline of shape (use multiple passes, counters encoded on tape).
- Machine schema notation: finite control descriptions for common constructs.

**Important results**
- Church–Turing thesis (informal): any effectively computable function is computed by a TM.
- Halting problem: set of pairs (M, w) such that M halts on w is undecidable; proof by diagonalization/self-reference (reduction).
- Relationship: decidable ⊂ Turing-recognizable; complement relationships (a language and its complement both RE ⇒ decidable).

**Exam tip**
- To show undecidability: reduce known undecidable problem (e.g., HALT) to target. To show decidability: give TM that always halts and recognizes language.

---

## Algoritmusok és adatszerkezetek (Algorithms & Data Structures)

### 4. Algorithm running time (asymptotic notation) and sorting/searching
**Notations**
- Big-O, Θ, Ω; formal definitions using constants; best/worst/average case clarifications.
- Master theorem for divide-and-conquer recurrences (common cases).

**Sorting algorithms**
- Heap sort: build max-heap O(n), then n times extract-max O(log n) ⇒ O(n log n) time, in-place, not stable.
- Quick sort: average O(n log n), worst-case O(n^2) (randomized pivot or median-of-three to avoid worst-case), divide-and-conquer, in-place, unstable unless modified.
- Merge sort: O(n log n) deterministic, stable, needs O(n) extra space (unless in-place variants).
- Quadratic sorts: insertion sort (O(n^2) worst; O(n) best for nearly sorted), bubble sort, selection sort.
- Linear or near-linear special sorts: counting sort (O(n + k)), radix sort (O(n · d)), bucket sort (assumptions on distribution).

**Searching**
- Linear search: O(n)
- Binary search: O(log n) on sorted arrays; careful with index math and termination conditions.

**Exam tip**
- Be ready to write partition step of quicksort, heapify operation, and to analyze recurrence relations.

---

### 5. Elementary and advanced data structures
**Stacks & Queues**
- Operations: push/pop, enqueue/dequeue; O(1) time.
**Linked lists**
- Single, doubly-linked, circular; insertion/deletion complexities; sentinel/head node patterns.
**Binary Search Trees (BST)**
- Search/insert/delete average O(h), where h is height; balanced vs degenerate cases.
**Heaps**
- Binary heap properties, array representation, operations: insert O(log n), extract-max/min O(log n), build-heap O(n).
**Red-Black Trees**
- Properties: every node red/black, root black, red nodes have black children, every path from node to null leaves has same number of black nodes (black-height).
- Rotations (left, right), insertion and deletion algorithms maintain invariants in O(log n).
**B-Trees**
- Balanced multi-way search trees used for external storage (disk). Parameters: minimum degree t, node keys between t−1 and 2t−1, height O(log_t n). Insertion and deletion algorithms preserve invariants.
**Hash tables**
- Hash functions, load factor α = n/m, collision resolution:
  - Chaining (linked lists per bucket).
  - Open addressing: linear probing, quadratic probing, double hashing.
- Amortized expected O(1) operations if resizing and good hash.

**Exam tip**
- Explain rotation in RB-trees; sketch an insertion rebalancing sequence. For hashing, demonstrate clustering pitfalls and how double hashing mitigates primary clustering.

---

### 6. Graph algorithms
**Representations**
- Adjacency list (good for sparse graphs), adjacency matrix (good for dense graphs).

**Traversal**
- BFS: O(V + E), computes shortest path in unweighted graphs (breadth layers).
- DFS: O(V + E), used for topological sort, connected components, and cycle detection.

**Minimum spanning tree (MST)**
- Prim's algorithm: grow tree from a start node using priority queue; O(E + V log V) with Fibonacci heap or O(E log V) typical.
- Kruskal's algorithm: sort edges O(E log E) then union-find to connect components; union-find with path compression nearly O(α(n)) per op.

**Shortest paths**
- Dijkstra: non-negative weights, O((V + E) log V) with priority queue.
- Bellman–Ford: handles negative weights, O(V·E), detects negative cycles.
- Single-source on DAGs: topological order relaxation O(V+E).

**Max flow**
- Ford–Fulkerson: augmenting path method; complexity depends on path-finding and capacities (can be exponential if capacities arbitrary).
- Edmonds–Karp: particular implementation with BFS gives O(V·E^2).
- Concepts: residual graph, augmenting path, cut, max-flow min-cut theorem.

**Exam tip**
- Be prepared to run one iteration of Dijkstra or Bellman-Ford on small graph by hand; explain union-find operations during Kruskal.

---

## Adatbázisok (Databases)

### 7. Redundancy, anomalies and normalization. NoSQL overview
**Problems**
- Redundancy causes update, insertion, deletion anomalies.

**Functional dependencies (FD)**
- FD X → Y: for relation R, identical X-values imply identical Y-values.
- Types: full, partial, transitive dependencies.

**Normal forms**
- 0NF, 1NF (atomic values), 2NF (no partial dependency of non-key on part of a composite key), 3NF (no transitive dependencies), BCNF (every FD X → Y: X is superkey).
- Decomposition algorithm: lossless-join and dependency preserving considerations.

**ACID and CAP**
- ACID (Atomicity, Consistency, Isolation, Durability) for transactions.
- CAP theorem: in distributed systems, only two of Consistency, Availability, Partition tolerance guaranteed simultaneously.

**NoSQL systems**
- Types: key-value stores, document stores, column-family stores, graph databases.
- CAP trade-offs, eventual consistency vs strong consistency.
- MapReduce paradigm: map, shuffle, reduce; use for batch processing large datasets.

**Exam tip**
- Given a relation and FDs, perform normalization to 3NF/BCNF and show decomposition preserves losslessness and dependencies where possible.

---

### 8. Conceptual DB design, EER, relational algebra and SQL
**E/R and EER**
- Entities (strong/weak), relationships (1:1, 1:N, M:N), attributes (simple, composite, multivalued), participation constraints (min/max cardinalities), specialization/generalization.
- Mapping EER to relations: mapping rules for 1:1, 1:N, M:N (with associative entity), specialization (single table, class table, concrete table strategies).

**Relational algebra operators**
- Selection σ, Projection π, Cartesian product ×, Join (θ-join, natural join), Union ∪, Intersection ∩, Difference −, Renaming ρ, Division ÷.
- SQL correspondences: SELECT-FROM-WHERE, GROUP BY, HAVING, ORDER BY. Use subqueries, joins, aggregate functions.

**Exam tip**
- Translate EER fragment to relations; write sample SQL queries that correspond to relational algebra expressions.

---

## Mesterséges intelligencia (AI)

### 9. Agents and propositional logic
**Agents**
- Agent architecture: environment, sensors, actuators, performance measure. Types of environments: deterministic/stochastic, fully/partially observable, episodic/sequential, static/dynamic, discrete/continuous.
- Agent types: reflex agents, model-based, goal-based, utility-based, learning agents. Multi-agent systems: coordination, communication.

**Propositional logic**
- Syntax and semantics: atomic propositions, connectives ¬, ∧, ∨, →, ↔.
- Entailment (⊨), satisfiability (SAT), validity.
- Proof methods: truth tables (complete but exponential), formal derivation systems (natural deduction), resolution (convert to CNF and apply resolution rules).

**Quine's method**
- A constructive method for propositional theorem proving based on recursive substitution/partition of formulas (used as an efficient alternative to naive truth-table enumeration). See standard AI logic texts for algorithmic description. :contentReference[oaicite:1]{index=1}

**Resolution**
- Convert formula to CNF, apply resolution rule (resolvent of clauses with complementary literals) until empty clause derived (unsatisfiable) or no new clauses (satisfiable).

**Exam tip**
- Be able to convert a propositional formula to CNF and perform a short resolution derivation.

---

### 10. Problem representation and search
**State-space representation**
- States, actions, transition model, goal test, path cost.

**Uninformed search**
- Breadth-first search (BFS), depth-first search (DFS), depth-limited, iterative deepening, uniform-cost search (Dijkstra-like for costs).

**Heuristic search**
- Heuristic function h(n). Greedy best-first, A* (f(n) = g(n) + h(n)), admissible and consistent heuristics and their role in optimality/efficiency.
- Iterative deepening A*, RBFS (recursive best-first search).

**Local search**
- Hill-climbing, simulated annealing, tabu search.

**Adversarial search**
- Minimax algorithm, evaluation functions, alpha-beta pruning (effectively reduces branches explored; same result as minimax but faster).

**Exam tip**
- Know proofs for A* admissibility and effects of heuristic consistency; run minimax on small game trees and show alpha-beta pruning.

---

### 11. Machine learning basics and neural networks
**Learning types**
- Supervised (classification, regression), unsupervised (clustering—k-means), reinforcement learning (policy, value functions, exploration vs exploitation), semi-supervised learning.

**Common algorithms**
- Decision trees (ID3/C4.5), k-NN, Naive Bayes, logistic regression, SVM (conceptual), k-means clustering.
- Overfitting vs underfitting; cross-validation; regularization (L1, L2).

**Neural networks**
- Perceptron, feed-forward networks, activation functions (sigmoid, tanh, ReLU), backpropagation (gradient descent on loss function), loss functions (MSE, cross-entropy).
- Deep learning basics: stacked layers, vanishing gradients, regularization (dropout, weight decay).

**Exam tip**
- Explain training loop for supervised NN and how gradients are computed via backpropagation; describe regularization strategies to mitigate overfitting.

---

## Computer architecture & networks & operating systems (selected items)

### Info representation and ALU
- Number systems: binary, two's complement for signed integers, floating point (IEEE-754 basics), endianness.
- ALU: adder circuits (ripple-carry, carry-lookahead), subtractors, basic multiplier (shift-add), divider algorithms (restoring/non-restoring).

### Control units
- Hardwired vs microprogrammed control, Mealy vs Moore finite-state controllers, horizontal vs vertical microcode.

### Processes and synchronization (OS)
- Process lifecycle, context switch, CPU scheduling algorithms (FCFS, SJF, Round Robin, Priority, Fair scheduling); metrics: turnaround, waiting, response times.
- Synchronization primitives: locks, semaphores (P/V), monitors; critical section problem and solutions (Peterson’s algorithm for two processes).
- Deadlock: Coffman conditions (mutual exclusion, hold and wait, no preemption, circular wait), prevention/avoidance (Banker's algorithm), detection and recovery.

### Memory management
- Memory hierarchy, virtual memory, paging and segmentation basics; page replacement algorithms (FIFO, LRU, Optimal), TLB and associative mapping.

### Filesystems & storage
- Disk scheduling algorithms (FCFS, SSTF, SCAN), RAID levels, file allocation methods (contiguous, linked, indexed), distributed file access concepts.

### Networking (layers)
- Physical & data link: media types, topologies, MAC addresses, frames and switching basics.
- Network layer: IPv4/IPv6 structure, subnetting, VLSM, routing protocols (distance-vector vs link-state), default gateway, NAT.
- Transport layer: UDP vs TCP, ports, three-way handshake (SYN, SYN-ACK, ACK), sliding window, flow control vs congestion control.

---

## Software engineering

### 10. Software as product and development models
- Software lifecycle phases: requirements, design, implementation, testing, maintenance.
- Models: Waterfall, Incremental, Spiral, Agile (Scrum, XP), prototyping, component-based development. Trade-offs, applicability.

### 11. Object-oriented design and UML
- OOP principles: encapsulation, inheritance, polymorphism, abstraction.
- UML diagrams: use-case, class, state, activity, sequence diagrams — purpose and primary elements.
- Rational Unified Process (RUP): phases (inception, elaboration, construction, transition), workflows/disciplines.

### 12. Software testing
- Verification vs validation, static vs dynamic testing, white-box vs black-box.
- Coverage metrics: statement, branch (decision) coverage; path testing and infeasibility.
- Test levels: unit, integration, system, acceptance. Test design techniques: equivalence partitioning, boundary value analysis, pairwise testing.
- Test process: test plan → cases → data → execution → reporting.
