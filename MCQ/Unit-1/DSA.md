# DSA MCQs — Unit 1

**Important:** in the real exam, DSA MCQ code snippets are given in **C**, so all code-output
questions here use **C**, not C++. (You still write DSA programs in C++ for practice and
assignments — see the [DSA Question Bank](../../DSA/Question-Bank.md).)

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run in C to confirm the answer — nothing here is guessed.

---

**Q1.** Which of these is **not** one of the five qualities of a good algorithm?
(a) Finiteness
(b) Input
(c) Compilation
(d) Effectiveness

**Q2.** Pseudocode is:
(a) A compiled machine language
(b) A plain, step-by-step description of logic, not tied to any programming language
(c) A type of data structure
(d) An error message

**Q3.** What is the output of this program?
```c
#include <stdio.h>
int main() {
    int a[5] = {2, 4, 6, 8, 10};
    int sum = 0;
    for (int i = 0; i < 5; i++)
        sum += a[i];
    printf("%d", sum);
    return 0;
}
```
(a) 20
(b) 30
(c) 10
(d) 40

**Q4.** Big-O notation represents:
(a) The best case (minimum) time
(b) The worst case (maximum) time
(c) The average case only
(d) The exact memory address used

**Q5.** Time complexity of a single loop that runs `n` times is:
(a) `O(1)`
(b) `O(n)`
(c) `O(n²)`
(d) `O(log n)`

**Q6.** Time complexity of two nested loops, each running `n` times, is:
(a) `O(n)`
(b) `O(2n)`
(c) `O(n²)`
(d) `O(log n)`

**Q7.** What is the output of this program?
```c
#include <stdio.h>
int main() {
    int n = 4, count = 0;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            count++;
    printf("%d", count);
    return 0;
}
```
(a) 4
(b) 8
(c) 12
(d) 16

**Q8.** Which data structure follows LIFO (Last In First Out)?
(a) Queue
(b) Stack
(c) Array
(d) Tree

**Q9.** Which data structure follows FIFO (First In First Out)?
(a) Stack
(b) Queue
(c) Linked list
(d) Graph

**Q10.** Which of the following is a **non-linear** data structure?
(a) Array
(b) Stack
(c) Queue
(d) Tree

**Q11.** For an array `A` with base address `Base` and element size `w`, the address of `A[i]`
(lower bound `LB`) is given by:
(a) `Base + w × i`
(b) `Base + w × (i − LB)`
(c) `Base − w × (i − LB)`
(d) `Base / w × (i − LB)`

**Q12.** An array `A[10]` has base address `1000`, and each element takes `4` bytes. The address
of `A[6]` (lower bound 0) is:
(a) 1006
(b) 1020
(c) 1024
(d) 1004

**Q13.** What is the output of this program?
```c
#include <stdio.h>
int main() {
    int a[6] = {5, 3, 8, 1, 9, 2};
    int key = 9, pos = -1;
    for (int i = 0; i < 6; i++) {
        if (a[i] == key) { pos = i; break; }
    }
    printf("%d", pos);
    return 0;
}
```
(a) 2
(b) 3
(c) 4
(d) -1

**Q14.** Binary search requires the array to be:
(a) Unsorted
(b) Sorted
(c) Circular
(d) Of even length only

**Q15.** What is the output of this program?
```c
#include <stdio.h>
int main() {
    int a[7] = {1, 3, 5, 7, 9, 11, 13};
    int low = 0, high = 6, mid;
    mid = (low + high) / 2;
    printf("%d", a[mid]);
    return 0;
}
```
(a) 5
(b) 7
(c) 9
(d) 3

**Q16.** What is the output of this program (one pass of bubble sort)?
```c
#include <stdio.h>
int main() {
    int a[5] = {5, 1, 4, 2, 8};
    int i, temp;
    for (i = 0; i < 4; i++) {
        if (a[i] > a[i+1]) {
            temp = a[i];
            a[i] = a[i+1];
            a[i+1] = temp;
        }
    }
    for (i = 0; i < 5; i++)
        printf("%d ", a[i]);
    return 0;
}
```
(a) `1 2 4 5 8`
(b) `1 4 2 5 8`
(c) `5 1 4 2 8`
(d) `1 4 5 2 8`

**Q17.** What is the output of this program (selection sort — finding the minimum)?
```c
#include <stdio.h>
int main() {
    int a[5] = {29, 10, 14, 37, 13};
    int i, minIdx = 0;
    for (i = 1; i < 5; i++) {
        if (a[i] < a[minIdx])
            minIdx = i;
    }
    printf("%d", a[minIdx]);
    return 0;
}
```
(a) 29
(b) 13
(c) 10
(d) 14

**Q18.** In selection sort, the maximum number of swaps needed for `n` elements is:
(a) `n²`
(b) `n − 1`
(c) `n × (n − 1)`
(d) `log n`

**Q19.** What is the output of this program?
```c
#include <stdio.h>
int main() {
    int a[10];
    printf("%d", (int)(sizeof(a) / sizeof(a[0])));
    return 0;
}
```
(a) 4
(b) 10
(c) 40
(d) 1

**Q20.** To merge two arrays into one sorted array using the two-pointer technique (without
sorting again afterwards), both input arrays must already be:
(a) Equal in size
(b) Sorted
(c) Circular
(d) Non-empty and unsorted

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | c | 11 | b |
| 2 | b | 12 | c |
| 3 | b | 13 | c |
| 4 | b | 14 | b |
| 5 | b | 15 | b |
| 6 | c | 16 | b |
| 7 | d | 17 | c |
| 8 | b | 18 | b |
| 9 | b | 19 | b |
| 10 | d | 20 | b |
