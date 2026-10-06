# DSA — Question Bank (Unit 1, Unit 2 & Unit 3)

Basic to advanced questions for practice. All coding here is in **C++**, same as class.
(Note: in the DSA MCQ exam, code snippets are given in **C** — practice that separately in the
[MCQ folder](../MCQ/).)

Short answers for the theory questions are at the [end of this file](#answers).
Coding questions have no fixed answer — check your output against what the question asks.

---

## Unit 1

### 1. Basic concepts and notations

**Basic**
1. What is an algorithm? Give one real-life example (not a computer example) of a step-by-step
   process.
2. Name the five qualities of a good algorithm.
3. What is the difference between an algorithm and a program?

**Intermediate**
4. What is "pseudocode"? Why do we write pseudocode before writing the actual program?
5. Write the algorithm (in steps) to find the largest of three numbers.

**Advanced**
6. Write a C++ program to find the largest of three numbers, based on the algorithm you wrote
   above.

### 2. Complexity analysis: time, space and trade-off

**Basic**
1. What is time complexity? What is space complexity?
2. What is meant by "space-time trade-off"?

**Intermediate**
3. Which is generally more important to optimize on a mobile phone with little memory — time or
   space? Why?
4. Write a C++ program to find the sum of first `n` natural numbers in two ways: (a) using a loop,
   (b) using the direct formula `n*(n+1)/2`. Which one has better time complexity?

**Advanced**
5. A program stores results in a table so it never repeats the same calculation twice (this is
   called memoization/caching). Does it save time or space, and what does it cost in return?

### 3. Big-O, Omega and Theta notation

**Basic**
1. What does Big-O (`O`) notation represent?
2. What does Omega (`Ω`) notation represent?
3. What does Theta (`Θ`) notation represent?

**Intermediate**
4. Give the time complexity (Big-O) of:
   (a) a single loop running `n` times
   (b) two nested loops each running `n` times
   (c) accessing one array element by index
   (d) binary search on a sorted array of `n` elements

**Advanced**
5. For linear search, what is the best case (Ω) and what is the worst case (O)? Explain when each
   happens.

### 4. Basic data structures

**Basic**
1. What is a data structure? Give three examples.
2. What is the difference between a linear and a non-linear data structure?
3. What do LIFO and FIFO stand for? Which data structure uses each?

**Intermediate**
4. Give one real-life example each for a stack and a queue.
5. Is an array linear or non-linear? Is a tree linear or non-linear?

**Advanced**
6. A browser's "back button" feature and a printer's "print queue" feature use two different data
   structures. Name each data structure and explain why it fits.

### 5. Linear arrays and memory representation

**Basic**
1. What is a linear array?
2. What does LB (lower bound) and UB (upper bound) mean for an array?
3. Write the formula to find the address of the `i`-th element of a 1-D array, given the base
   address and the size `w` of one element.

**Intermediate**
4. An array `A[10]` has base address `1000` and each element takes `4` bytes. Find the address of
   `A[6]`.
5. Write a C++ program that declares an array of 5 integers, takes input, and prints the address
   of each element using `&`.

**Advanced**
6. An array `A[1..20]` is stored with base address `2000`, and each element is `4` bytes. Find the
   address of `A[15]`, showing every step of the formula.

### 6. Array operations: traversal, insertion, deletion

**Basic**
1. What is traversal in an array?
2. What is insertion in an array? What is deletion?
3. Why does inserting or deleting the first element of an array cost more than doing so for the
   last element?

**Intermediate**
4. Write a C++ program that inserts a new element at a given position in an array (shifting
   later elements to the right).
5. Write a C++ program that deletes an element from a given position in an array (shifting later
   elements to the left).

**Advanced**
6. Write a C++ program that traverses an array and deletes **all** occurrences of a given value
   (not just the first one found).

### 7. Searching: linear search and binary search

**Basic**
1. What is linear search? What is binary search?
2. Does binary search need the array to be sorted first? Why?

**Intermediate**
3. Write a C++ program for linear search that returns the position of a given number in an array
   (or −1 if not found).
4. Write a C++ program for binary search (iterative, using `low`, `high`, `mid`) that returns the
   position of a given number.

**Advanced**
5. For an array of 1,000,000 elements, roughly how many comparisons will binary search need in
   the worst case, compared to linear search? (Use the Big-O idea, not an exact count.)

### 8. Sorting: bubble, insertion and selection sort

**Basic**
1. What is sorting? Name three sorting techniques you have studied.
2. In bubble sort, what is a "swap", and what does one full pass do?

**Intermediate**
3. Write a C++ program for bubble sort on an array of integers.
4. Write a C++ program for selection sort on an array of integers.

**Advanced**
5. Write a C++ program for insertion sort on an array of integers.
6. Which of bubble sort, insertion sort and selection sort would you call the "simplest to
   understand", and which does the least number of swaps in general? Explain in 2 lines.

### 9. Merging two arrays

**Basic**
1. What does "merging" two arrays mean?
2. Do the two arrays need to be sorted before merging into one sorted array?

**Intermediate**
3. Write a C++ program to merge two **sorted** arrays into one sorted array (without sorting the
   result afterwards — merge them directly using two pointers).

**Advanced**
4. Write a C++ program that merges two sorted arrays into one sorted array **without duplicate
   values** (if a number appears in both arrays, it should appear only once in the result).

---

## Unit 2

### 10. Linked lists — introduction and memory representation

**Basic**
1. What is a linked list? How is it different from an array?
2. What is a "node" in a linked list? What two parts does it usually have?
3. What is the "head" of a linked list?

**Intermediate**
4. Give two advantages of a linked list over an array. Give one disadvantage.
5. In an array, memory is contiguous (one block, side by side). Is memory for a linked list also
   contiguous? Explain.

**Advanced**
6. Write a C++ `struct Node` with an `int data` and a `Node* next`. Create three nodes by hand
   (without a loop) and link them together to form a list of 3 nodes.

### 11. Allocation and traversal

**Basic**
1. Which C++ operator is used to create (allocate) a new node dynamically?
2. What does it mean to "traverse" a linked list?
3. How do you know you have reached the end of a singly linked list?

**Intermediate**
4. Write a C++ program that creates a linked list of `n` integers entered by the user (using
   `new` for each node) and then prints all the values.

**Advanced**
5. Write a C++ function `countNodes()` that traverses a linked list and returns how many nodes it
   has.

### 12. Insertion in a linked list

**Basic**
1. Name the three places where a new node can be inserted in a linked list.
2. What must be updated first when inserting a node at the **beginning** of the list — the new
   node's `next`, or the `head`?

**Intermediate**
3. Write a C++ function to insert a new node **at the beginning** of a linked list.
4. Write a C++ function to insert a new node **at the end** of a linked list.

**Advanced**
5. Write a C++ function to insert a new node **after a given position** (e.g. after the 3rd node)
   in a linked list.

### 13. Deletion in a linked list

**Basic**
1. Name the three places from where a node can be deleted in a linked list.
2. Which C++ keyword is used to free the memory of a deleted node?

**Intermediate**
3. Write a C++ function to delete the **first** node of a linked list.
4. Write a C++ function to delete the **last** node of a linked list.

**Advanced**
5. Write a C++ function to delete a node **with a given value** anywhere in the linked list
   (handle the case where the value is not found, and the case where it is the first node).

### 14. Header linked lists: grounded and circular

**Basic**
1. What is a "header linked list"? What extra node does it have compared to a normal linked
   list?
2. What is a "grounded" header linked list?
3. What is a "circular" header linked list?

**Intermediate**
4. In a circular linked list, what does the `next` pointer of the **last** node point to (instead
   of `NULL`)?
5. Give one advantage of a circular linked list over a normal (grounded) singly linked list.

**Advanced**
6. Write a C++ program that creates a small circular linked list (3 nodes) and traverses it
   exactly once, printing each node's data (careful: the loop condition cannot be `while (p != NULL)`
   here — explain why, in a comment).

### 15. Two-way (doubly) linked lists

**Basic**
1. What is a two-way (doubly) linked list? What extra pointer does each node have, compared to a
   singly linked list?
2. Can you traverse a doubly linked list backwards (from the last node to the first)? Can you do
   this with a singly linked list?

**Intermediate**
3. Write a C++ `struct Node` for a doubly linked list, with `data`, `prev` and `next`.
4. Write a C++ function to insert a new node **at the beginning** of a doubly linked list
   (remember to update both `prev` and `next` links).

**Advanced**
5. Write a C++ function to delete a given node from a doubly linked list, updating the links of
   its previous and next nodes so the list stays connected.
6. Give one advantage of a doubly linked list over a singly linked list, and one disadvantage
   (in terms of memory).

---

## Unit 3

### 16. Stack — introduction and array representation

**Basic**
1. What is a stack? What does LIFO mean?
2. What do `push`, `pop` and `peek` do?
3. What is stack overflow? What is stack underflow?

**Intermediate**
4. In an array stack where `top` starts at `-1`, write the condition for (a) stack full,
   (b) stack empty.
5. Write a C++ program for a stack using an array, with `push()`, `pop()`, `peek()` and
   `display()` functions. Show overflow and underflow messages.

**Advanced**
6. Write a C++ program that uses a stack to reverse a string entered by the user.

### 17. Stack — linked list representation

**Basic**
1. In a linked list stack, which node is the `top`?
2. Can a linked list stack overflow like an array stack? Explain.

**Intermediate**
3. Write a C++ program for a stack using a linked list, with `push()`, `pop()` and `display()`.

**Advanced**
4. Write a C++ program that uses a stack to check whether the brackets in an expression are
   balanced, e.g. `(A+B)*(C-D)` is balanced but `((A+B)` is not.

### 18. Arithmetic expressions and Polish notation

**Basic**
1. What are infix, prefix and postfix notations? Give one example of each.
2. What is Polish notation? What is Reverse Polish notation?
3. Write the precedence of `^`, `*`, `/`, `+`, `-`. Which of them is right-to-left?

**Intermediate**
4. Why do computers prefer postfix (or prefix) expressions over infix expressions?
5. Convert by hand to postfix and prefix: (a) `A * (B + C)` (b) `A + B - C * D`.

**Advanced**
6. Convert by hand to postfix and prefix: `(A + B) * (C - D) / E ^ F`.

### 19. Evaluation of postfix and prefix expressions

**Basic**
1. Which data structure is used to evaluate a postfix expression?
2. In postfix evaluation, when an operator comes, we pop two items. Which popped item is the
   **left** operand?

**Intermediate**
3. Evaluate the postfix expression `4 5 + 7 2 - *` step by step, showing the stack.
4. Evaluate the prefix expression `+ * 2 3 / 8 4` step by step, showing the stack.

**Advanced**
5. Write a C++ program to evaluate a postfix expression of single-digit numbers using a stack.

### 20. Transformation: infix to postfix and prefix

**Basic**
1. In infix-to-postfix conversion, what do we do when we see (a) an operand, (b) `(`, (c) `)`?

**Intermediate**
2. Convert `A * (B + C) - D / E` to postfix using a stack. Show the stack and output after
   each symbol.
3. Write the steps to convert an infix expression to prefix using the "reverse" method.

**Advanced**
4. Write a C++ program to convert an infix expression to postfix using a stack (handle `(`, `)`,
   and the operators `+ - * / ^`).

### 21. Queue — introduction and array representation

**Basic**
1. What is a queue? What does FIFO mean?
2. What are `front` and `rear` in a queue? At which end do we insert, and at which end do we
   delete?

**Intermediate**
3. Give two differences between a stack and a queue.
4. Write a C++ program for a queue using an array, with `enqueue()`, `dequeue()` and `display()`.

**Advanced**
5. Explain, with a small diagram, why a simple (linear) array queue can say "full" even when
   there are free boxes in the array.

### 22. Circular queue

**Basic**
1. What is a circular queue? Why do we need it?
2. Write the formula used to move `rear` forward in a circular queue.

**Intermediate**
3. Write the conditions for a circular queue to be (a) full, (b) empty.
4. A circular queue has `MAX = 6`, `front = 4` and `rear = 1`. How many items does it hold?

**Advanced**
5. Write a C++ program for a circular queue using an array, with `enqueue()`, `dequeue()` and
   `display()`.

### 23. Queue — linked list representation

**Basic**
1. In a linked list queue, which pointer is used for insertion and which for deletion?
2. Why do we keep a separate `rear` pointer in a linked list queue?

**Intermediate**
3. Write a C++ program for a queue using a linked list, with `enqueue()`, `dequeue()` and
   `display()`.

**Advanced**
4. In `dequeue()`, when the last node is deleted, what must happen to `rear`? What bug appears if
   we forget it?

### 24. Priority queues

**Basic**
1. What is a priority queue? Give one real-life example.
2. In a priority queue, if two items have the same priority, which one is deleted first?

**Intermediate**
3. Name two ways to represent a priority queue in memory.
4. Items `X(3), Y(1), Z(2), W(1)` are inserted (smaller number = higher priority). Write the order
   in which they are deleted.

**Advanced**
5. Write a C++ program for a priority queue using a linked list that is kept sorted by priority.

### 25. Deques

**Basic**
1. What is a deque? Name its four operations.
2. What is an input-restricted deque? What is an output-restricted deque?

**Intermediate**
3. In a circular array deque, write the formula to move `front` one step back in `insertFront()`.
   Why do we add `MAX` before taking `%`?

**Advanced**
4. Write a C++ program for a deque using a circular array, with `insertFront()`, `insertRear()`,
   `deleteFront()`, `deleteRear()` and `display()`.
5. Explain how a deque can be used as a stack and also as a queue.

---

# Answers

## Unit 1

1. Algorithm = a finite set of clear steps to solve a problem (e.g. a cooking recipe). Five
   qualities: Input, Output, Definiteness, Finiteness, Effectiveness. Algorithm is the idea/plan
   (language independent); a program is that idea written in a specific programming language.
2. Pseudocode = a plain-English, step-by-step description of an algorithm that is not tied to any
   programming language's exact syntax. It helps plan the logic first without worrying about
   compiler errors.
3. Time complexity = how the running time grows as input size grows. Space complexity = how the
   memory used grows as input size grows. Trade-off = you can often use more memory to make a
   program faster, or less memory but make it slower — you balance the two based on what the
   situation needs.
4. On a mobile phone with little memory, **space** usually matters more, because running out of
   memory can crash the app, while being a little slower is usually tolerable. The formula
   `n*(n+1)/2` is `O(1)` — better time complexity than the loop, which is `O(n)`.
5. Memoization saves **time** (avoids repeating the same work) at the cost of extra **space**
   (the table that stores past results).
6. Big-O = worst-case (maximum) time/space an algorithm needs. Omega = best-case (minimum).
   Theta = the case when best and worst are the same (a tight, exact bound).
7. (a) `O(n)`  (b) `O(n²)`  (c) `O(1)`  (d) `O(log n)`.
8. Linear search: best case `Ω(1)` (the item is the very first element checked); worst case
   `O(n)` (the item is last, or not present, so every element is checked).
9. Data structure = a way of organizing and storing data so it can be used efficiently, e.g.
   array, stack, queue. Linear: elements are arranged one after another (array, stack, queue,
   linked list). Non-linear: elements branch out (tree, graph). LIFO = Last In First Out (stack).
   FIFO = First In First Out (queue).
10. Stack real-life example: a stack of plates (last plate placed is the first one removed).
    Queue real-life example: a ticket counter line (first person in line is served first). Array
    is linear; a tree is non-linear.
11. Browser back button → **stack** (the most recently visited page is undone first — LIFO).
    Printer queue → **queue** (the first document sent is the first one printed — FIFO).
12. Linear array = a set of elements of the same type stored in consecutive memory locations, all
    accessed using one variable name and an index. LB/UB = the smallest and largest valid index of
    the array. Address formula: `Address(A[i]) = Base + w × (i − LB)`.
13. `Address(A[6]) = 1000 + 4 × (6 − 0) = 1000 + 24 = 1024` (assuming lower bound 0; if the array
    is 1-indexed, use `(6 − 1)` instead).
14. Traversal = visiting every element of the array once, usually to print or process it.
    Insertion = adding a new element into the array (existing elements after that position shift
    right to make room). Deletion = removing an element from the array (elements after it shift
    left to fill the gap). Inserting/deleting near the **beginning** costs more because more
    elements must shift, compared to the end where nothing (or very little) needs to shift.
15. Binary search needs a **sorted** array because it works by comparing the middle element and
    deciding to search the left half or the right half — this logic is only correct if the array
    is in order.
16. Binary search on 1,000,000 elements needs about `log₂(1,000,000) ≈ 20` comparisons in the
    worst case; linear search could need up to 1,000,000 comparisons. Binary search is dramatically
    faster on large sorted arrays.
17. Sorting = arranging elements in increasing or decreasing order. Three techniques: bubble sort,
    insertion sort, selection sort. In bubble sort, a "swap" exchanges two adjacent elements that
    are in the wrong order; one full pass compares and swaps adjacent elements across the whole
    array, pushing the largest remaining element to its correct position at the end.
18. Selection sort generally does the **fewest swaps** (at most `n−1` swaps, since it swaps only
    once per pass after finding the minimum). Bubble sort is usually considered the **simplest to
    understand** since it is just "compare neighbours and swap".
19. Merging = combining two arrays into one single array. If the goal is a sorted result without
    re-sorting afterwards, then yes — both input arrays must already be sorted so the two-pointer
    merge technique works correctly.

## Unit 2

20. Linked list = a linear data structure where elements (nodes) are linked using pointers,
    instead of being stored in contiguous memory like an array. A node usually has two parts:
    `data` (the value) and `next` (a pointer to the next node). The `head` is a pointer that
    stores the address of the first node of the list.
21. Advantages of a linked list over an array: its size can grow or shrink at runtime (no fixed
    size), and inserting/deleting at the beginning is fast (no shifting needed). Disadvantage: no
    direct/random access — to reach the 5th node you must traverse from the head, one node at a
    time. Linked list memory is **not** contiguous — each node can be anywhere in memory; only the
    `next` pointers connect them logically.
22. `new` is used to dynamically allocate a new node in C++. Traversal = starting at `head` and
    following `next` pointers one by one until the end. You know you've reached the end of a
    singly linked list when the current pointer becomes `NULL`.
23. Three places to insert: at the beginning, at the end, or at a given position (after a specific
    node). When inserting at the beginning, you must first set the **new node's `next`** to point
    to the current `head`, and only then update `head` to point to the new node (doing it in the
    other order would lose the rest of the list).
24. Three places to delete from: the beginning, the end, or a node with a given value/position.
    `delete` is used in C++ to free the memory of a removed node.
25. Header linked list = a linked list that has one extra special "header" node at the front
    (which does not store real data, just acts as a starting anchor). Grounded header linked
    list = the last node's `next` still points to `NULL` as usual. Circular header linked list =
    the last node's `next` points back to the header node instead of `NULL`, forming a circle.
26. In a circular linked list, the **last node's `next`** points back to the **first node** (or the
    header, in a circular header list) instead of `NULL`. Advantage: from any node you can reach
    every other node, and you can keep going around the list endlessly (useful, e.g., for a
    round-robin turn order).
27. Doubly linked list = a linked list where each node has **two** pointers: `prev` (to the
    previous node) and `next` (to the next node), in addition to `data`. This lets you traverse
    both forward and backward, which a singly linked list cannot do (it only has `next`).
    Advantage of doubly linked list: easy backward traversal and easier deletion of a node when you
    already have a pointer to it. Disadvantage: extra memory is used for the additional `prev`
    pointer in every node.

## Unit 3

28. Stack = a linear data structure where items are added and removed from **one end only**,
    called the **top**. LIFO = Last In, First Out (the last item pushed is the first one popped,
    like a pile of plates). `push` adds an item on the top, `pop` removes the top item, and `peek`
    only reads the top item without removing it. Overflow = trying to push into a **full** stack.
    Underflow = trying to pop from an **empty** stack.
29. With `top` starting at `-1`: (a) stack full → `top == MAX - 1`; (b) stack empty →
    `top == -1`. To reverse a string, push every character, then pop them all — the last
    character comes out first, so the string is reversed.
30. In a linked list stack, the **first node** is the `top` (push = insert at beginning, pop =
    delete first node, both fast). It does **not** overflow like an array stack, because there is
    no fixed size — a new node is created with `new` for every push. It can fail only if the
    computer's whole memory runs out. Bracket checking: push every `(`, and for every `)` pop one
    `(`; the brackets are balanced only if we never pop from an empty stack and the stack is empty
    at the end.
31. Infix = operator **between** operands (`A+B`). Prefix = operator **before** operands (`+AB`).
    Postfix = operator **after** operands (`AB+`). Prefix is called **Polish notation**, and
    postfix is called **Reverse Polish notation**. Precedence: `^` (highest), then `*` `/`, then
    `+` `-` (lowest). `^` is **right to left**; the others are left to right.
32. Computers prefer postfix/prefix because they need **no brackets** and **no precedence rules**
    — the order of symbols already shows what to do first, so they can be evaluated in one scan
    using a stack. Conversions: (a) `A*(B+C)` → postfix `ABC+*`, prefix `*A+BC`.
    (b) `A+B-C*D` → postfix `AB+CD*-`, prefix `-+AB*CD`.
33. `(A+B)*(C-D)/E^F` → postfix `AB+CD-*EF^/`, prefix `/*+AB-CD^EF`. (`^` is done first, then `*`
    and `/` from left to right.)
34. A **stack** is used to evaluate postfix. When an operator comes, the **first** popped item is
    the **right** operand and the **second** popped item is the **left** operand.
    `4 5 + 7 2 - *`: push 4, push 5, `+` → 9; push 7, push 2, `-` → 5 (stack: 9 5); `*` → 9 × 5 =
    **45**.
35. Prefix `+ * 2 3 / 8 4` (scan right to left): push 4, push 8, `/` → 8 / 4 = 2; push 3, push 2,
    `*` → 2 × 3 = 6 (stack: 2 6); `+` → 6 + 2 = **8**.
36. Infix to postfix: (a) operand → write it to the output; (b) `(` → push it; (c) `)` → pop
    operators to the output until `(`, then remove the `(`. `A*(B+C)-D/E`:
    `A` → out `A`; `*` → stack `*`; `(` → stack `*(`; `B` → out `AB`; `+` → stack `*(+`;
    `C` → out `ABC`; `)` → out `ABC+`, stack `*`; `-` → pop `*` (higher), out `ABC+*`, stack `-`;
    `D` → out `ABC+*D`; `/` → stack `-/`; `E` → out `ABC+*DE`; end → pop all.
    Postfix = **`ABC+*DE/-`**.
    Infix to prefix (reverse method): (1) reverse the infix and swap `(` with `)`, (2) find the
    postfix of that, (3) reverse the result.
37. Queue = a linear data structure where items are inserted at the **rear** and deleted from the
    **front**. FIFO = First In, First Out (like a ticket line). Differences from a stack: a stack
    is LIFO, a queue is FIFO; a stack uses one end (`top`), a queue uses two ends (`front` and
    `rear`).
38. In a simple (linear) array queue, `rear` only moves forward. After some deletions, `front`
    moves forward and the boxes before it become free, but once `rear == MAX - 1` the queue says
    "full" and those free boxes can never be used again. A **circular queue** fixes this.
39. Circular queue = the last box of the array is joined back to the first box, so `rear` can
    wrap around and reuse free boxes. Move rear: `rear = (rear + 1) % MAX`. Full:
    `(rear + 1) % MAX == front`. Empty: `front == -1`. For `MAX = 6`, `front = 4`, `rear = 1`:
    count = `(1 - 4 + 6) % 6 + 1` = **4** items (indexes 4, 5, 0, 1).
40. In a linked list queue, insertion uses `rear` (add after the last node) and deletion uses
    `front` (remove the first node). We keep `rear` so that insertion does not need to walk
    through the whole list. When the last node is deleted, `rear` must also be set to `NULL`;
    otherwise it points to a deleted node and the next `enqueue()` writes into freed memory, and
    `front` stays `NULL`, so the new item is lost.
41. Priority queue = a queue where each item has a priority, and the item with the **highest
    priority** is deleted first (e.g. a hospital emergency room, CPU job scheduling). Items with
    the **same** priority are deleted in the order they came (FIFO). Two representations: a
    one-way linked list kept sorted by priority, and an array of queues (one queue per priority
    level). (A heap is also used.) For `X(3), Y(1), Z(2), W(1)` the deletion order is
    **Y W Z X**.
42. Deque = double-ended queue: insertion and deletion are allowed at **both** ends. Four
    operations: `insertFront`, `insertRear`, `deleteFront`, `deleteRear`. Input-restricted deque =
    insertion at only one end, deletion at both ends. Output-restricted deque = deletion at only
    one end, insertion at both ends.
43. In `insertFront()`: `front = (front - 1 + MAX) % MAX`. We add `MAX` so that when `front` is
    `0`, it goes back to `MAX - 1` instead of becoming `-1` (an invalid index). A deque works as a
    **stack** if we insert and delete at the **same** end (e.g. `insertRear` + `deleteRear`), and
    as a **queue** if we insert at one end and delete at the other (e.g. `insertRear` +
    `deleteFront`).
