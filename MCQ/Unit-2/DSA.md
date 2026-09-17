# DSA MCQs — Unit 2

**Important:** in the real exam, DSA MCQ code snippets are given in **C**, so all code-output
questions here use **C** (with `malloc`, `struct`, `->`), not C++. (You still write DSA programs
in C++ for practice and assignments — see the [DSA Question Bank](../../DSA/Question-Bank.md).)

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run in C to confirm the answer — nothing here is guessed.

---

**Q1.** A node in a singly linked list usually contains:
(a) Only data
(b) Only a pointer
(c) Data and a pointer to the next node
(d) Two pointers and no data

**Q2.** Compared to an array, a linked list:
(a) Has a fixed size decided at compile time
(b) Can grow or shrink at runtime and uses non-contiguous memory
(c) Always uses less memory than an array
(d) Allows direct (random) access using an index

**Q3.** Which C function is used to dynamically allocate memory for a new node?
(a) `alloc()`
(b) `malloc()`
(c) `new()`
(d) `create()`

**Q4.** What is the output of this program?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
int main() {
    struct Node *head, *second, *third;
    head = (struct Node*)malloc(sizeof(struct Node));
    second = (struct Node*)malloc(sizeof(struct Node));
    third = (struct Node*)malloc(sizeof(struct Node));

    head->data = 10;
    head->next = second;
    second->data = 20;
    second->next = third;
    third->data = 30;
    third->next = NULL;

    struct Node *p = head;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    return 0;
}
```
(a) `10 20 30`
(b) `30 20 10`
(c) `10 20`
(d) Infinite loop

**Q5.** In a singly linked list, you know you have reached the end when:
(a) `data` becomes 0
(b) The current pointer becomes `NULL`
(c) `next` points back to `head`
(d) The loop runs exactly 10 times

**Q6.** What is the output of this program?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
int countNodes(struct Node *head) {
    int c = 0;
    while (head != NULL) {
        c++;
        head = head->next;
    }
    return c;
}
int main() {
    struct Node n3 = {30, NULL};
    struct Node n2 = {20, &n3};
    struct Node n1 = {10, &n2};
    printf("%d", countNodes(&n1));
    return 0;
}
```
(a) 2
(b) 3
(c) 30
(d) 0

**Q7.** When inserting a new node at the **beginning** of a linked list, the correct order is:
(a) Update `head` first, then set the new node's `next`
(b) Set the new node's `next` to the old `head` first, then update `head` to the new node
(c) Order does not matter
(d) Delete the old head first

**Q8.** What is the output of this program (insertion at the beginning)?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
int main() {
    struct Node *head = NULL;
    struct Node *a = (struct Node*)malloc(sizeof(struct Node));
    a->data = 5; a->next = NULL;
    head = a;

    struct Node *b = (struct Node*)malloc(sizeof(struct Node));
    b->data = 1;
    b->next = head;
    head = b;

    struct Node *p = head;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    return 0;
}
```
(a) `5 1`
(b) `1 5`
(c) `1`
(d) `5`

**Q9.** What is the output of this program (deletion of the first node)?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
int main() {
    struct Node *n1 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n2 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n3 = (struct Node*)malloc(sizeof(struct Node));
    n1->data = 7; n1->next = n2;
    n2->data = 8; n2->next = n3;
    n3->data = 9; n3->next = NULL;

    struct Node *head = n1;
    struct Node *temp = head;
    head = head->next;
    free(temp);

    struct Node *p = head;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    return 0;
}
```
(a) `7 8 9`
(b) `8 9`
(c) `7 8`
(d) `9`

**Q10.** Which C keyword frees the memory of a deleted node?
(a) `remove`
(b) `delete`
(c) `free`
(d) `clear`

**Q11.** A header linked list has:
(a) No `head` pointer at all
(b) One extra special node at the front that does not store real data
(c) Two `head` pointers
(d) Only one node total

**Q12.** In a **grounded** header linked list, the last node's `next` points to:
(a) The header node
(b) The first data node
(c) `NULL`
(d) Itself

**Q13.** In a **circular** linked list, the last node's `next` points to:
(a) `NULL`
(b) The first node (or header, in a circular header list)
(c) A random address
(d) Nothing, `next` is removed

**Q14.** What is the output of this program (traversing a circular linked list once)?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
int main() {
    struct Node *n1 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n2 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n3 = (struct Node*)malloc(sizeof(struct Node));
    n1->data = 1; n1->next = n2;
    n2->data = 2; n2->next = n3;
    n3->data = 3; n3->next = n1;

    struct Node *p = n1;
    int i;
    for (i = 0; i < 3; i++) {
        printf("%d ", p->data);
        p = p->next;
    }
    return 0;
}
```
(a) `1 2 3`
(b) `1 2 3 1 2 3 ...` (infinite)
(c) `3 2 1`
(d) `1 1 1`

**Q15.** Why can a circular linked list **not** be traversed with the condition
`while (p != NULL)`?
(a) Because `p` is never `NULL` to begin with
(b) Because the last node's `next` points back into the list, so `p` never becomes `NULL`
(c) Because circular lists do not use pointers
(d) Because `NULL` is not allowed in C

**Q16.** A doubly (two-way) linked list node has:
(a) Only a `next` pointer
(b) Only a `prev` pointer
(c) Both `prev` and `next` pointers
(d) No pointers, only data

**Q17.** What is the output of this program (traversing a doubly linked list backward)?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *prev; struct Node *next; };
int main() {
    struct Node *n1 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n2 = (struct Node*)malloc(sizeof(struct Node));
    struct Node *n3 = (struct Node*)malloc(sizeof(struct Node));
    n1->data = 100; n1->prev = NULL; n1->next = n2;
    n2->data = 200; n2->prev = n1;   n2->next = n3;
    n3->data = 300; n3->prev = n2;   n3->next = NULL;

    struct Node *p = n3;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->prev;
    }
    return 0;
}
```
(a) `100 200 300`
(b) `300 200 100`
(c) `300`
(d) `100`

**Q18.** A key advantage of a doubly linked list over a singly linked list is:
(a) It uses less memory per node
(b) It allows traversal in both directions
(c) It cannot be traversed at all
(d) It does not need a `head` pointer

**Q19.** A key disadvantage of a doubly linked list compared to a singly linked list is:
(a) It cannot store data
(b) Extra memory is needed for the additional `prev` pointer in every node
(c) It cannot be inserted into
(d) It can only hold one node

**Q20.** Linked lists (compared to arrays) are especially useful when:
(a) The exact number of elements is fixed and known in advance and random access is required
(b) Frequent insertions and deletions are needed and the size keeps changing
(c) Memory must always be contiguous
(d) Binary search is required

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | c | 11 | b |
| 2 | b | 12 | c |
| 3 | b | 13 | b |
| 4 | a | 14 | a |
| 5 | b | 15 | b |
| 6 | b | 16 | c |
| 7 | b | 17 | b |
| 8 | b | 18 | b |
| 9 | b | 19 | b |
| 10 | c | 20 | b |
