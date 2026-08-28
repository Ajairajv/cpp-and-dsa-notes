# DSA — Unit 1

Simple notes for all Unit 1 topics. All programs are in **C++**.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**
```bash
g++ program.cpp -o program
./program
```

### Topics
1. [Basic concepts and notations](#1-basic-concepts-and-notations)
2. [Complexity analysis: time, space and trade-off](#2-complexity-analysis-time-space-and-trade-off)
3. [Big-O, Omega and Theta notation](#3-big-o-omega-and-theta-notation)
4. [Basic data structures](#4-basic-data-structures)
5. [Linear arrays and memory representation](#5-linear-arrays-and-memory-representation)
6. [Array operations: traversal, insertion, deletion](#6-array-operations-traversal-insertion-deletion)
7. [Searching: linear search and binary search](#7-searching-linear-search-and-binary-search)
8. [Sorting: bubble, insertion and selection](#8-sorting-bubble-insertion-and-selection)
9. [Merging two arrays](#9-merging-two-arrays)

---

## 1. Basic concepts and notations

**What it is**

| Word | Meaning |
|---|---|
| **Data** | Raw facts. Example: `21`, `"Aarav"`, `87.5` |
| **Data structure** | A way of storing data in memory so that we can use it easily. Example: array |
| **Algorithm** | A step-by-step method to solve a problem |

**Five qualities of a good algorithm**

1. **Input** — it takes zero or more inputs.
2. **Output** — it gives at least one output.
3. **Definiteness** — every step is clear, not confusing.
4. **Finiteness** — it must stop after some steps. It cannot run forever.
5. **Effectiveness** — every step is simple enough to be done.

**Notation (how we write an algorithm)**

Before writing a program, we write the steps in simple English. This is called **pseudocode**.

```text
Algorithm FIND_LARGEST(A, N)
    Step 1: Set MAX := A[0]
    Step 2: Repeat for I = 1 to N-1
                If A[I] > MAX then
                    Set MAX := A[I]
                [End of If]
            [End of Loop]
    Step 3: Write MAX
    Step 4: Exit
```

**Program**

```cpp
#include <iostream>
using namespace std;

// The same algorithm written as a C++ program
int findLargest(int a[], int n) {
    int max = a[0];                 // Step 1
    for (int i = 1; i < n; i++) {   // Step 2
        if (a[i] > max)
            max = a[i];
    }
    return max;                     // Step 3
}

int main() {
    int a[7] = {23, 9, 71, 4, 68, 15, 42};

    cout << "Array: ";
    for (int i = 0; i < 7; i++)
        cout << a[i] << " ";
    cout << endl;

    cout << "Largest element = " << findLargest(a, 7) << endl;
    return 0;
}
```

**Output**
```
Array: 23 9 71 4 68 15 42
Largest element = 71
```

**Practice question**

**Q1.** Write the five qualities of a good algorithm.

---

## 2. Complexity analysis: time, space and trade-off

**What it is**

**Time complexity** — how much **time** an algorithm takes. We do not count it in seconds, because
seconds change from computer to computer. Instead we **count the number of steps**.

**Space complexity** — how much **memory** an algorithm needs.

**How to count steps**

| Code | Steps | Complexity |
|---|---|---|
| `x = a[5];` | 1 step | `O(1)` |
| one loop running `n` times | `n` steps | `O(n)` |
| a loop inside a loop | `n × n` steps | `O(n²)` |
| value becomes half every time | `log n` steps | `O(log n)` |

**Three cases**

| Case | Meaning |
|---|---|
| **Best case** | Least work. Example: the item is the first one |
| **Average case** | Normal work |
| **Worst case** | Most work. Example: the item is the last one, or not there |

**Time–space trade-off**

Sometimes we can make a program **faster by using more memory**, or **save memory by doing more
work**. This is called the time–space trade-off.

Example: to find a student's marks quickly, we can store all marks in a big table (more memory, but
fast). Or we can search the list every time (less memory, but slow).

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    int n = 5;
    int count;

    // O(1) - one step only, does not depend on n
    count = 1;
    cout << "O(1)    steps = " << count << endl;

    // O(n) - one loop
    count = 0;
    for (int i = 1; i <= n; i++)
        count++;
    cout << "O(n)    steps = " << count << endl;

    // O(n*n) - loop inside a loop
    count = 0;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            count++;
    cout << "O(n^2)  steps = " << count << endl;

    // O(log n) - value becomes half each time
    count = 0;
    int x = n;
    while (x > 1) {
        x = x / 2;
        count++;
    }
    cout << "O(logn) steps = " << count << endl;
    return 0;
}
```

**Output**
```
O(1)    steps = 1
O(n)    steps = 5
O(n^2)  steps = 25
O(logn) steps = 2
```

**Practice question**

**Q2.** Write the time complexity of each:
(a) a single loop running `n` times
(b) a loop inside another loop
(c) reading `a[3]` from an array
(d) a loop where the value becomes half every time

---

## 3. Big-O, Omega and Theta notation

**What it is**

These three symbols are used to show how much time an algorithm takes.

| Symbol | Name | Meaning | Used for |
|---|---|---|---|
| `O` | **Big-O** | The **maximum** time. "It will not take more than this." | **Worst** case |
| `Ω` | **Omega** | The **minimum** time. "It will take at least this much." | **Best** case |
| `Θ` | **Theta** | The **exact** time. Maximum and minimum are the same. | **Average** case |

**Easy way to remember**

- `O` is like "**at most**" (upper limit) — like a speed limit.
- `Ω` is like "**at least**" (lower limit).
- `Θ` is like "**exactly**" (both limits together).

**Rules to make it simple**

1. Remove the constant numbers. `O(5n)` becomes `O(n)`.
2. Keep only the **biggest** term. `O(n² + n + 10)` becomes `O(n²)`.

**Order from fastest to slowest**

```
O(1)  <  O(log n)  <  O(n)  <  O(n log n)  <  O(n²)  <  O(2ⁿ)
```

**Why it matters — for n = 1000**

| Complexity | Number of steps |
|---|---|
| `O(1)` | 1 |
| `O(log n)` | 10 |
| `O(n)` | 1,000 |
| `O(n²)` | 1,000,000 |

**Program**

```cpp
#include <iostream>
using namespace std;

// Linear search, so we can see all three cases
int search(int a[], int n, int key, int &steps) {
    steps = 0;
    for (int i = 0; i < n; i++) {
        steps++;
        if (a[i] == key)
            return i;
    }
    return -1;
}

int main() {
    int a[5] = {10, 20, 30, 40, 50};
    int steps;

    search(a, 5, 10, steps);        // first element
    cout << "Best case (first item)  : " << steps << " steps  -> Omega(1)" << endl;

    search(a, 5, 30, steps);        // middle element
    cout << "Average case (middle)   : " << steps << " steps  -> Theta(n)" << endl;

    search(a, 5, 99, steps);        // not present
    cout << "Worst case (not found)  : " << steps << " steps  -> O(n)" << endl;
    return 0;
}
```

**Output**
```
Best case (first item)  : 1 steps  -> Omega(1)
Average case (middle)   : 3 steps  -> Theta(n)
Worst case (not found)  : 5 steps  -> O(n)
```

**Practice question**

**Q3.** What is the meaning of `O`, `Ω` and `Θ`? Which one is used for the worst case?

---

## 4. Basic data structures

**What it is**

A data structure is a way of storing data. They are divided into two types.

```
                    DATA STRUCTURES
                          |
          -----------------------------------
          |                                 |
      PRIMITIVE                      NON-PRIMITIVE
  (int, float, char)                       |
                            ---------------------------
                            |                         |
                        LINEAR                   NON-LINEAR
                (data in a line, one            (one item can have
                 after another)                  many connections)
                            |                         |
                Array, Stack, Queue,             Tree, Graph
                  Linked list
```

**Short meaning of each**

| Structure | Meaning | Example in real life |
|---|---|---|
| **Array** | Items stored one after another in memory | Roll numbers in a list |
| **Stack** | Last In First Out (LIFO). Add and remove from one end only | Pile of plates |
| **Queue** | First In First Out (FIFO). Add at back, remove from front | Line at a ticket counter |
| **Linked list** | Items joined by addresses (pointers), not side by side | Treasure hunt clues |
| **Tree** | One item has many items below it | Family tree |
| **Graph** | Any item can join to any other item | Roads between cities |

**Array vs Linked list**

| Array | Linked list |
|---|---|
| Memory is fixed | Memory grows when needed |
| Items are side by side in memory | Items are anywhere, joined by pointers |
| Getting `a[5]` is very fast | Must count from the start, so slow |
| Inserting in the middle is slow | Inserting is fast |

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    // ARRAY
    int a[5] = {10, 20, 30, 40, 50};
    cout << "Array   : ";
    for (int i = 0; i < 5; i++) cout << a[i] << " ";
    cout << endl;

    // STACK - Last In First Out
    int stack[10], top = 0;
    stack[top++] = 1;
    stack[top++] = 2;
    stack[top++] = 3;
    cout << "Stack   : put 1 2 3, take out -> ";
    while (top > 0) cout << stack[--top] << " ";     // comes out reversed
    cout << endl;

    // QUEUE - First In First Out
    int queue[10], front = 0, rear = 0;
    queue[rear++] = 1;
    queue[rear++] = 2;
    queue[rear++] = 3;
    cout << "Queue   : put 1 2 3, take out -> ";
    while (front < rear) cout << queue[front++] << " ";   // same order
    cout << endl;
    return 0;
}
```

**Output**
```
Array   : 10 20 30 40 50
Stack   : put 1 2 3, take out -> 3 2 1
Queue   : put 1 2 3, take out -> 1 2 3
```

**Practice question**

**Q4.** Which data structures are linear and which are non-linear? Also write the full form of LIFO
and FIFO.

---

## 5. Linear arrays and memory representation

**What it is**

A **linear array** is a list of items:
- of the **same type** (all `int`, or all `float`),
- stored in memory **one after another** (side by side),
- used with a common name and an **index** number.

**How it looks in memory**

```
index :     0        1        2        3        4
        +--------+--------+--------+--------+--------+
   A =  |   10   |   20   |   30   |   40   |   50   |
        +--------+--------+--------+--------+--------+
address  1000     1004     1008     1012     1016
             (each int takes 4 bytes, so +4 each time)
```

**The address formula — very important for exams**

> **LOC(A[i]) = Base + w × (i − LB)**

| Symbol | Meaning |
|---|---|
| `LOC(A[i])` | address of the item we want |
| `Base` | address of the **first** item |
| `w` | size of one item in bytes (int = 4, float = 4, char = 1, double = 8) |
| `i` | index we want |
| `LB` | lower bound (the first index number) |

**Example.** Array `A[1..20]`, Base = 1000, w = 4. Find the address of `A[7]`.

```
LOC(A[7]) = 1000 + 4 × (7 − 1)
          = 1000 + 4 × 6
          = 1000 + 24
          = 1024
```

**Remember:** if the array starts from `A[1]`, then `LB = 1`. In C++, arrays start from 0, so
`LB = 0`.

**Number of items** = `UB − LB + 1`

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    int a[5] = {10, 20, 30, 40, 50};

    cout << "Size of one int = " << sizeof(int) << " bytes" << endl << endl;

    cout << "Index   Value   Address" << endl;
    for (int i = 0; i < 5; i++) {
        cout << "  " << i << "      " << a[i] << "     " << &a[i] << endl;
    }

    cout << endl;
    cout << "See that each address is 4 more than the last one." << endl << endl;

    // The formula, done by hand
    int base = 1000, w = 4, lb = 1, i = 7;
    cout << "Question: A[1..20], Base = 1000, w = 4. Find LOC(A[7])" << endl;
    cout << "LOC(A[7]) = " << base << " + " << w << " * (" << i << " - " << lb << ") = "
         << base + w * (i - lb) << endl;
    return 0;
}
```

**Output** (the real addresses will be different on your computer, that is normal)
```
Size of one int = 4 bytes

Index   Value   Address
  0      10     0x61fe00
  1      20     0x61fe04
  2      30     0x61fe08
  3      40     0x61fe0c
  4      50     0x61fe10

See that each address is 4 more than the last one.

Question: A[1..20], Base = 1000, w = 4. Find LOC(A[7])
LOC(A[7]) = 1000 + 4 * (7 - 1) = 1024
```

**Practice question**

**Q5.** An array `A[1..50]` has Base address 2000 and each item takes 4 bytes.
Find the address of `A[15]`.

---

## 6. Array operations: traversal, insertion, deletion

**What it is**

| Operation | Meaning | Time |
|---|---|---|
| **Traversal** | Going through every item once (to print or add) | `O(n)` |
| **Insertion** | Putting a new item at some position | `O(n)` |
| **Deletion** | Removing an item from some position | `O(n)` |

**Why insertion and deletion are slow**

- To **insert**, all the items after that place must move **one step right** to make space.
- To **delete**, all the items after that place must move **one step left** to fill the gap.

```
Insert 25 at position 2:
Before :  10  20  30  40  50
                  <-- 30, 40, 50 move right -->
After  :  10  20  25  30  40  50

Delete position 1:
Before :  10  20  30  40  50
              <-- 30, 40, 50 move left -->
After  :  10  30  40  50
```

**Important**
- Inserting/deleting at the **end** is fast (nothing moves).
- Inserting/deleting at the **beginning** is slowest (everything moves).
- **Overflow** = trying to insert when the array is full.
- **Underflow** = trying to delete when the array is empty.

**Program**

```cpp
#include <iostream>
using namespace std;

void display(int a[], int n) {
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

int main() {
    int a[20] = {10, 20, 30, 40, 50};
    int n = 5;

    cout << "Original       : ";
    display(a, n);

    // INSERTION - insert 25 at position 2
    int pos = 2, item = 25;
    for (int i = n - 1; i >= pos; i--)      // move backwards, right side
        a[i + 1] = a[i];
    a[pos] = item;
    n++;
    cout << "Insert 25 at 2 : ";
    display(a, n);

    // DELETION - delete position 0
    pos = 0;
    cout << "Deleted item   : " << a[pos] << endl;
    for (int i = pos; i < n - 1; i++)       // move forwards, left side
        a[i] = a[i + 1];
    n--;
    cout << "After deleting : ";
    display(a, n);

    // TRAVERSAL - add all items
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + a[i];
    cout << "Sum of all     : " << sum << endl;
    return 0;
}
```

**Output**
```
Original       : 10 20 30 40 50
Insert 25 at 2 : 10 20 25 30 40 50
Deleted item   : 10
After deleting : 20 25 30 40 50
Sum of all     : 165
```

**Practice question**

**Q6.** Why is inserting an item at the beginning of an array slower than inserting at the end?
Also write the meaning of overflow and underflow.

---

## 7. Searching: linear search and binary search

**What it is**

**Linear search** — check every item one by one from the start until you find it.
- Works on **any** array (sorted or not sorted).
- Time: `O(n)`

**Binary search** — check the **middle** item. If the item you want is smaller, look only in the
left half. If bigger, look only in the right half. Repeat.
- The array **must be sorted**. This is compulsory.
- Time: `O(log n)` — very fast.

**Why binary search is fast**

Every time, half the items are removed.

| Number of items | Linear search (worst) | Binary search (worst) |
|---|---|---|
| 100 | 100 checks | 7 checks |
| 1,000 | 1,000 checks | 10 checks |
| 1,000,000 | 1,000,000 checks | 20 checks |

**Difference**

| Linear search | Binary search |
|---|---|
| Array need not be sorted | Array **must** be sorted |
| Checks one by one | Checks the middle, then half |
| `O(n)` — slow | `O(log n)` — fast |
| Good for small lists | Good for big lists |

**Program**

```cpp
#include <iostream>
using namespace std;

// LINEAR SEARCH - one by one
int linearSearch(int a[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (a[i] == key)
            return i;           // found, return the position
    }
    return -1;                  // not found
}

// BINARY SEARCH - array must be sorted
int binarySearch(int a[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        cout << "   checking middle a[" << mid << "] = " << a[mid] << endl;

        if (a[mid] == key)
            return mid;             // found
        else if (a[mid] < key)
            low = mid + 1;          // go to the right half
        else
            high = mid - 1;         // go to the left half
    }
    return -1;                      // not found
}

int main() {
    int a[10] = {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};   // sorted

    cout << "Linear search for 70:" << endl;
    cout << "   found at position " << linearSearch(a, 10, 70) << endl;

    cout << endl << "Binary search for 70:" << endl;
    cout << "   found at position " << binarySearch(a, 10, 70) << endl;

    cout << endl << "Binary search for 35 (not present):" << endl;
    cout << "   result = " << binarySearch(a, 10, 35) << " (means not found)" << endl;
    return 0;
}
```

**Output**
```
Linear search for 70:
   found at position 6

Binary search for 70:
   checking middle a[4] = 50
   checking middle a[7] = 80
   checking middle a[5] = 60
   checking middle a[6] = 70
   found at position 6

Binary search for 35 (not present):
   checking middle a[4] = 50
   checking middle a[1] = 20
   checking middle a[2] = 30
   checking middle a[3] = 40
   result = -1 (means not found)
```

**Practice question**

**Q7.** Write four differences between linear search and binary search. What is the one condition
needed for binary search?

---

## 8. Sorting: bubble, insertion and selection

**What it is**

**Sorting** means arranging items in order (small to big).

**1. Bubble sort** — compare two items which are next to each other. If the left one is bigger,
swap them. After each round, the biggest item goes to the end.

**2. Selection sort** — find the **smallest** item and put it in the first place. Then find the next
smallest and put it in second place, and so on.

**3. Insertion sort** — take one item and put it in its correct place among the items already
sorted. Just like arranging playing cards in your hand.

**Comparison**

| | Bubble sort | Selection sort | Insertion sort |
|---|---|---|---|
| Best case | `O(n)` | `O(n²)` | `O(n)` |
| Average case | `O(n²)` | `O(n²)` | `O(n²)` |
| Worst case | `O(n²)` | `O(n²)` | `O(n²)` |
| Number of swaps | Many | **Very few** (`n−1`) | Many |
| Extra memory | `O(1)` | `O(1)` | `O(1)` |

All three are **slow** for big lists, but easy to understand.

**Program**

```cpp
#include <iostream>
using namespace std;

void display(int a[], int n) {
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
    cout << endl;
}

// BUBBLE SORT - compare side by side items and swap
void bubbleSort(int a[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            if (a[j] > a[j + 1]) {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
        cout << "   pass " << i + 1 << " : ";
        display(a, n);
    }
}

// SELECTION SORT - find smallest, put it in front
void selectionSort(int a[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int min = i;
        for (int j = i + 1; j < n; j++) {
            if (a[j] < a[min])
                min = j;
        }
        int temp = a[i];                // swap
        a[i] = a[min];
        a[min] = temp;

        cout << "   pass " << i + 1 << " : ";
        display(a, n);
    }
}

// INSERTION SORT - put each item in its correct place
void insertionSort(int a[], int n) {
    for (int i = 1; i < n; i++) {
        int key = a[i];
        int j = i - 1;
        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];            // move bigger items to the right
            j--;
        }
        a[j + 1] = key;

        cout << "   pass " << i << " : ";
        display(a, n);
    }
}

int main() {
    int x[5] = {64, 25, 12, 22, 11};
    int y[5] = {64, 25, 12, 22, 11};
    int z[5] = {64, 25, 12, 22, 11};

    cout << "BUBBLE SORT (start: 64 25 12 22 11)" << endl;
    bubbleSort(x, 5);

    cout << endl << "SELECTION SORT (start: 64 25 12 22 11)" << endl;
    selectionSort(y, 5);

    cout << endl << "INSERTION SORT (start: 64 25 12 22 11)" << endl;
    insertionSort(z, 5);
    return 0;
}
```

**Output**
```
BUBBLE SORT (start: 64 25 12 22 11)
   pass 1 : 25 12 22 11 64
   pass 2 : 12 22 11 25 64
   pass 3 : 12 11 22 25 64
   pass 4 : 11 12 22 25 64

SELECTION SORT (start: 64 25 12 22 11)
   pass 1 : 11 25 12 22 64
   pass 2 : 11 12 25 22 64
   pass 3 : 11 12 22 25 64
   pass 4 : 11 12 22 25 64

INSERTION SORT (start: 64 25 12 22 11)
   pass 1 : 25 64 12 22 11
   pass 2 : 12 25 64 22 11
   pass 3 : 12 22 25 64 11
   pass 4 : 11 12 22 25 64
```

**Practice question**

**Q8.** Show all the passes of **bubble sort** for this list: `5 1 4 2 8`

---

## 9. Merging two arrays

**What it is**

**Merging** means joining **two sorted arrays** into **one sorted array**.

**How it works** — keep one finger on each array. Compare the two items your fingers are on. Take
the **smaller** one and put it in the new array. Move that finger forward. Repeat.

At the end, if one array still has items left, copy all of them.

```
A =  10  20  30
B =  15  25

compare 10 and 15  ->  take 10
compare 20 and 15  ->  take 15
compare 20 and 25  ->  take 20
compare 30 and 25  ->  take 25
B is over, so copy 30

Answer =  10  15  20  25  30
```

- Time: **`O(m + n)`** where `m` and `n` are the sizes of the two arrays.
- Extra memory: `O(m + n)` for the new array.

**Note:** both arrays must already be **sorted**.

**Program**

```cpp
#include <iostream>
using namespace std;

void merge(int a[], int m, int b[], int n, int c[]) {
    int i = 0, j = 0, k = 0;

    // compare and take the smaller one
    while (i < m && j < n) {
        if (a[i] <= b[j]) {
            c[k] = a[i];
            i++;
        } else {
            c[k] = b[j];
            j++;
        }
        k++;
    }

    // if array A still has items left, copy them
    while (i < m) {
        c[k] = a[i];
        i++;
        k++;
    }

    // if array B still has items left, copy them
    while (j < n) {
        c[k] = b[j];
        j++;
        k++;
    }
}

int main() {
    int a[5] = {10, 20, 30, 45, 60};        // sorted
    int b[4] = {15, 25, 50, 70};            // sorted
    int c[9];                               // 5 + 4 = 9

    merge(a, 5, b, 4, c);

    cout << "Array A : ";
    for (int i = 0; i < 5; i++) cout << a[i] << " ";
    cout << endl;

    cout << "Array B : ";
    for (int i = 0; i < 4; i++) cout << b[i] << " ";
    cout << endl;

    cout << "Merged  : ";
    for (int i = 0; i < 9; i++) cout << c[i] << " ";
    cout << endl;
    return 0;
}
```

**Output**
```
Array A : 10 20 30 45 60
Array B : 15 25 50 70
Merged  : 10 15 20 25 30 45 50 60 70
```

**Practice question**

**Q9.** Merge these two sorted arrays by hand and write each step:
`A = 2 8 15` and `B = 5 9 12`

---
---

# Answers

**Q1.** The five qualities of a good algorithm:
1. **Input** — it takes zero or more inputs.
2. **Output** — it gives at least one output.
3. **Definiteness** — every step is clear and not confusing.
4. **Finiteness** — it stops after a fixed number of steps.
5. **Effectiveness** — every step is simple enough to be carried out.

**Q2.**
- (a) `O(n)`
- (b) `O(n²)`
- (c) `O(1)`
- (d) `O(log n)`

**Q3.**
- **`O` (Big-O)** — the **maximum** time an algorithm will take. Used for the **worst case**.
- **`Ω` (Omega)** — the **minimum** time an algorithm will take. Used for the **best case**.
- **`Θ` (Theta)** — the **exact** time, when the maximum and minimum are the same. Used for the
  **average case**.

**`O` (Big-O) is used for the worst case.**

**Q4.**
- **Linear:** Array, Stack, Queue, Linked list
- **Non-linear:** Tree, Graph
- **LIFO** = Last In First Out (used in a **stack**)
- **FIFO** = First In First Out (used in a **queue**)

**Q5.**
```
LOC(A[15]) = Base + w × (i − LB)
           = 2000 + 4 × (15 − 1)
           = 2000 + 4 × 14
           = 2000 + 56
           = 2056
```
**Answer = 2056**

(Note: `LB = 1` because the array is `A[1..50]`, so it starts from 1.)

**Q6.**
Inserting at the beginning is slower because **every item in the array has to move one step to the
right** to make space. If there are `n` items, then `n` items must move. But when we insert at the
end, **no item has to move**, so it is very fast.

- **Overflow** — trying to insert a new item when the array is already **full**.
- **Underflow** — trying to delete an item when the array is **empty**.

**Q7.** Differences:

| Linear search | Binary search |
|---|---|
| Array need not be sorted | Array **must be sorted** |
| Checks each item one by one from the start | Checks the middle item and removes half the list |
| Time is `O(n)` — slow | Time is `O(log n)` — fast |
| Good for small lists | Good for large lists |
| Works on linked lists also | Does not work well on linked lists |

**The one condition for binary search: the array must be sorted.**

**Q8.** Bubble sort on `5 1 4 2 8`:

| Pass | What happens | Result |
|---|---|---|
| Start | — | `5 1 4 2 8` |
| Pass 1 | 5>1 swap, 5>4 swap, 5>2 swap, 5<8 no swap | `1 4 2 5 8` |
| Pass 2 | 1<4 no, 4>2 swap, 4<5 no | `1 2 4 5 8` |
| Pass 3 | 1<2 no, 2<4 no | `1 2 4 5 8` |
| Pass 4 | 1<2 no | `1 2 4 5 8` |

**Final sorted list: `1 2 4 5 8`**

(Note: after Pass 1, the biggest number 8 is already at the end. After Pass 2 the list is already
sorted, but the loop still runs the remaining passes.)

**Q9.** Merging `A = 2 8 15` and `B = 5 9 12`:

| Step | Compare | Take | Result so far |
|---|---|---|---|
| 1 | 2 and 5 | 2 (from A) | `2` |
| 2 | 8 and 5 | 5 (from B) | `2 5` |
| 3 | 8 and 9 | 8 (from A) | `2 5 8` |
| 4 | 15 and 9 | 9 (from B) | `2 5 8 9` |
| 5 | 15 and 12 | 12 (from B) | `2 5 8 9 12` |
| 6 | B is over | copy 15 from A | `2 5 8 9 12 15` |

**Final answer: `2 5 8 9 12 15`**

---

[Back to top](#dsa--unit-1)
