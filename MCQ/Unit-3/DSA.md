# DSA MCQs — Unit 3

**Important:** in the real exam, DSA MCQ code snippets are given in **C**, so all code-output
questions here use **C** (with `malloc`, `struct`, `->`), not C++. (You still write DSA programs
in C++ for practice and assignments — see the [DSA Question Bank](../../DSA/Question-Bank.md).)

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run in C to confirm the answer, and every expression conversion/evaluation was checked by a
program — nothing here is guessed.

---

**Q1.** A stack works on which principle?
(a) FIFO — First In, First Out
(b) LIFO — Last In, First Out
(c) Items are removed in sorted order
(d) Items can be removed from any position

**Q2.** What is the output of this program?
```c
#include <stdio.h>
#define MAX 5
int stack[MAX], top = -1;
void push(int x) { stack[++top] = x; }
int pop() { return stack[top--]; }
int main() {
    push(10);
    push(20);
    pop();
    push(30);
    push(40);
    while (top != -1)
        printf("%d ", pop());
    return 0;
}
```
(a) `10 30 40`
(b) `40 30 20 10`
(c) `10 20 30 40`
(d) `40 30 10`

**Q3.** In an array stack with `top` starting at `-1`, the **overflow** condition is:
(a) `top == -1`
(b) `top == 0`
(c) `top == MAX`
(d) `top == MAX - 1`

**Q4.** What is the output of this program (stack using a linked list)?
```c
#include <stdio.h>
#include <stdlib.h>
struct Node { int data; struct Node *next; };
struct Node *top = NULL;
void push(int x) {
    struct Node *n = (struct Node*)malloc(sizeof(struct Node));
    n->data = x;
    n->next = top;
    top = n;
}
int main() {
    push(1);
    push(2);
    push(3);
    struct Node *p = top;
    while (p != NULL) {
        printf("%d ", p->data);
        p = p->next;
    }
    return 0;
}
```
(a) `3 2 1`
(b) `1 2 3`
(c) `3`
(d) `1`

**Q5.** Trying to **pop** from an empty stack is called:
(a) Overflow
(b) Garbage collection
(c) Underflow
(d) Segmentation

**Q6.** **Polish notation** is another name for:
(a) Infix notation
(b) Postfix notation
(c) Prefix notation
(d) Bracket notation

**Q7.** The postfix form of `A + B * C` is:
(a) `AB+C*`
(b) `+A*BC`
(c) `ABC*+`
(d) `AB*C+`

**Q8.** The prefix form of `(A + B) * (C - D)` is:
(a) `*+AB-CD`
(b) `AB+CD-*`
(c) `+*AB-CD`
(d) `*AB+CD-`

**Q9.** The postfix form of `(A + B) * C - D / E` is:
(a) `AB+C*D/E-`
(b) `ABC+*DE/-`
(c) `AB+CDE/-*`
(d) `AB+C*DE/-`

**Q10.** Which data structure is used to convert an infix expression to postfix, and to evaluate
a postfix expression?
(a) Queue
(b) Stack
(c) Priority queue
(d) Linked list with header

**Q11.** What is the output of this program (postfix evaluation)?
```c
#include <stdio.h>
int st[20], top = -1;
void push(int x) { st[++top] = x; }
int pop() { return st[top--]; }
int main() {
    char exp[] = "23*54*+9-";
    int i, a, b;
    for (i = 0; exp[i] != '\0'; i++) {
        char c = exp[i];
        if (c >= '0' && c <= '9')
            push(c - '0');
        else {
            b = pop();
            a = pop();
            if (c == '+') push(a + b);
            if (c == '-') push(a - b);
            if (c == '*') push(a * b);
            if (c == '/') push(a / b);
        }
    }
    printf("%d", pop());
    return 0;
}
```
(a) 23
(b) 17
(c) 35
(d) 9

**Q12.** The value of the postfix expression `5 6 2 + * 12 4 / -` is:
(a) 37
(b) 28
(c) 40
(d) 20

**Q13.** The value of the prefix expression `- + 8 / 6 3 2` is:
(a) 6
(b) 4
(c) 10
(d) 8

**Q14.** The expression `A ^ B ^ C` is evaluated as:
(a) `(A ^ B) ^ C`, because `^` is left to right
(b) `A ^ (B ^ C)`, because `^` is right to left
(c) Both give the same answer, so the order does not matter
(d) It is an invalid expression

**Q15.** What is the output of this program (array queue)?
```c
#include <stdio.h>
#define MAX 5
int q[MAX], front = -1, rear = -1;
void enqueue(int x) {
    if (front == -1) front = 0;
    q[++rear] = x;
}
int dequeue() { return q[front++]; }
int main() {
    int i;
    enqueue(5);
    enqueue(10);
    enqueue(15);
    dequeue();
    enqueue(20);
    for (i = front; i <= rear; i++)
        printf("%d ", q[i]);
    return 0;
}
```
(a) `5 10 15 20`
(b) `5 10 15`
(c) `10 15 20`
(d) `20 15 10`

**Q16.** In a circular queue of size `MAX`, the queue is **full** when:
(a) `rear == MAX - 1`
(b) `front == -1`
(c) `front == rear`
(d) `(rear + 1) % MAX == front`

**Q17.** What is the output of this program (circular queue)?
```c
#include <stdio.h>
#define MAX 4
int q[MAX], front = -1, rear = -1;
void enqueue(int x) {
    if (front == -1) front = 0;
    rear = (rear + 1) % MAX;
    q[rear] = x;
}
void dequeue() { front = (front + 1) % MAX; }
int main() {
    enqueue(1);
    enqueue(2);
    enqueue(3);
    enqueue(4);
    dequeue();
    dequeue();
    enqueue(5);
    printf("front=%d rear=%d value=%d", front, rear, q[rear]);
    return 0;
}
```
(a) `front=2 rear=0 value=5`
(b) `front=2 rear=4 value=5`
(c) `front=0 rear=0 value=1`
(d) `front=1 rear=3 value=4`

**Q18.** In a queue made with a linked list (with `front` and `rear` pointers), a new node is
inserted at the ______ and deleted from the ______.
(a) front, rear
(b) rear, front
(c) front, front
(d) middle, rear

**Q19.** In a priority queue, if two items have the **same** priority, they are deleted:
(a) In random order
(b) Larger value first
(c) In the order they were inserted (first come, first served)
(d) They cannot both be in the queue

**Q20.** What is the output of this program (deque using a circular array)?
```c
#include <stdio.h>
#define MAX 5
int dq[MAX], front = -1, rear = -1;
void insertFront(int x) {
    if (front == -1) front = rear = 0;
    else front = (front - 1 + MAX) % MAX;
    dq[front] = x;
}
void insertRear(int x) {
    if (front == -1) front = rear = 0;
    else rear = (rear + 1) % MAX;
    dq[rear] = x;
}
int main() {
    int i;
    insertRear(2);
    insertFront(1);
    insertRear(3);
    insertFront(0);
    i = front;
    while (1) {
        printf("%d ", dq[i]);
        if (i == rear) break;
        i = (i + 1) % MAX;
    }
    printf("| front=%d", front);
    return 0;
}
```
(a) `0 1 2 3 | front=0`
(b) `0 1 2 3 | front=3`
(c) `1 0 2 3 | front=3`
(d) `2 3 0 1 | front=0`

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | b | 11 | b |
| 2 | d | 12 | a |
| 3 | d | 13 | d |
| 4 | a | 14 | b |
| 5 | c | 15 | c |
| 6 | c | 16 | d |
| 7 | c | 17 | a |
| 8 | a | 18 | b |
| 9 | d | 19 | c |
| 10 | b | 20 | b |
