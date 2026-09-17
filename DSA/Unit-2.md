# DSA — Unit 2

Simple notes for all Unit 2 topics. All programs are in **C++**.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**
```bash
g++ program.cpp -o program
./program
```

### Topics
10. [Linked lists: introduction and memory representation](#10-linked-lists-introduction-and-memory-representation)
11. [Allocation and traversal](#11-allocation-and-traversal)
12. [Insertion in a linked list](#12-insertion-in-a-linked-list)
13. [Deletion in a linked list](#13-deletion-in-a-linked-list)
14. [Header linked lists: grounded and circular](#14-header-linked-lists-grounded-and-circular)
15. [Two-way (doubly) linked lists](#15-two-way-doubly-linked-lists)

---

## 10. Linked lists: introduction and memory representation

**What it is**

A **linked list** is a linear data structure, but unlike an array, its items are **not** stored
side by side in memory. Each item is stored separately, and they are **joined using addresses**
(pointers) — a bit like a treasure hunt, where each clue tells you where to find the next one.

Each item is called a **node**. A node has two parts:

```
+--------+---------+
|  data  |  next   |   <- one Node
+--------+---------+
             |
             v
        (address of the next node)
```

The list is reached using a pointer called `head`, which stores the address of the **first**
node. The **last** node's `next` is `nullptr` — that is how we know the list has ended.

```
head
  |
  v
+----+----+     +----+----+     +----+----+
| 10 |  *-+---->| 20 |  *-+---->| 30 | NULL|
+----+----+     +----+----+     +----+----+
```

**Array vs Linked list**

| Array | Linked list |
|---|---|
| Memory is **contiguous** (side by side) | Memory is **not** contiguous — nodes can be anywhere |
| Fixed size | Can grow or shrink while the program runs |
| `a[5]` gives direct access | Must start from `head` and follow `next`, one by one |
| Inserting/deleting in the middle is slow (shifting) | Inserting/deleting is fast, no shifting needed |

**Program**

```cpp
#include <iostream>
using namespace std;

// A NODE has two parts: data, and address of the next node
struct Node {
    int data;
    Node *next;
};

int main() {
    // Creating three nodes by hand and linking them
    Node n1, n2, n3;

    n1.data = 10;  n1.next = &n2;
    n2.data = 20;  n2.next = &n3;
    n3.data = 30;  n3.next = nullptr;      // last node points to nothing

    Node *head = &n1;                      // head stores the address of the first node

    cout << "Linked list: ";
    Node *p = head;
    while (p != nullptr) {
        cout << p->data << " -> ";
        p = p->next;
    }
    cout << "NULL" << endl;
    return 0;
}
```

**Output**
```
Linked list: 10 -> 20 -> 30 -> NULL
```

**Practice question**

**Q10.** Give two advantages of a linked list over an array, and one disadvantage.

---

## 11. Allocation and traversal

**What it is**

**Allocation** means creating a new node while the program is running, using the `new` keyword.
Unlike the nodes we made by hand in the last topic, `new` gives a node memory at runtime, and we
get back a **pointer** to it.

```cpp
Node *newNode = new Node;     // allocates memory for one Node
newNode->data = 25;           // fills it in
newNode->next = nullptr;
```

**Traversal** means visiting every node once, starting from `head` and moving through `next`
pointers, until we reach `nullptr`.

```cpp
Node *p = head;
while (p != nullptr) {
    // do something with p->data
    p = p->next;
}
```

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

int countNodes(Node *head) {
    int count = 0;
    Node *p = head;
    while (p != nullptr) {
        count++;
        p = p->next;
    }
    return count;
}

int main() {
    int n;
    cout << "How many numbers? ";
    cin >> n;

    Node *head = nullptr, *last = nullptr;

    for (int i = 0; i < n; i++) {
        int val;
        cout << "Enter number " << i + 1 << ": ";
        cin >> val;

        Node *newNode = new Node;          // ALLOCATION: create a new node
        newNode->data = val;
        newNode->next = nullptr;

        if (head == nullptr)
            head = newNode;                // first node
        else
            last->next = newNode;          // link previous node to this one
        last = newNode;
    }

    cout << "List: ";
    Node *p = head;                        // TRAVERSAL
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;

    cout << "Total nodes = " << countNodes(head) << endl;
    return 0;
}
```

**Output** (whatever the user types is shown in the input lines)
```
How many numbers? 3
Enter number 1: 10
Enter number 2: 20
Enter number 3: 30
List: 10 20 30
Total nodes = 3
```

**Practice question**

**Q11.** Write a function `sumNodes(Node *head)` that traverses a linked list and returns the sum
of all the data values.

---

## 12. Insertion in a linked list

**What it is**

A new node can be inserted in **three** places:

1. **At the beginning** — the new node's `next` must be set to the old `head` **first**, and only
   then should `head` be updated. Doing it in the wrong order loses the rest of the list.
2. **At the end** — walk to the last node (the one whose `next` is `nullptr`), and link it to the
   new node.
3. **After a given node** — walk to that node, then link the new node in between it and whatever
   came after it.

```
Insert at beginning:
   new -----> old head -----> ...
    ^
  head now points here

Insert after a node X:
   ... -> X -> new -> (X's old next) -> ...
```

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

void display(Node *head) {
    Node *p = head;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

// insert at the beginning
Node* insertBeginning(Node *head, int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = head;      // new node points to old head FIRST
    head = newNode;             // then head is updated
    return head;
}

// insert at the end
Node* insertEnd(Node *head, int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = nullptr;

    if (head == nullptr)
        return newNode;

    Node *p = head;
    while (p->next != nullptr)
        p = p->next;
    p->next = newNode;
    return head;
}

// insert after a given position (1-based)
Node* insertAfter(Node *head, int pos, int val) {
    Node *p = head;
    for (int i = 1; i < pos && p != nullptr; i++)
        p = p->next;

    if (p == nullptr) {
        cout << "Position not found" << endl;
        return head;
    }

    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = p->next;
    p->next = newNode;
    return head;
}

int main() {
    Node *head = nullptr;
    head = insertEnd(head, 20);
    head = insertEnd(head, 30);
    cout << "Start          : ";
    display(head);

    head = insertBeginning(head, 10);
    cout << "After insert beginning (10): ";
    display(head);

    head = insertEnd(head, 40);
    cout << "After insert end (40)      : ";
    display(head);

    head = insertAfter(head, 2, 15);
    cout << "After insert after pos 2 (15): ";
    display(head);
    return 0;
}
```

**Output**
```
Start          : 20 30
After insert beginning (10): 10 20 30
After insert end (40)      : 10 20 30 40
After insert after pos 2 (15): 10 20 15 30 40
```

**Practice question**

**Q12.** Why must the new node's `next` be set **before** updating `head`, when inserting at the
beginning of a list?

---

## 13. Deletion in a linked list

**What it is**

A node can be deleted from **three** places:

1. **The first node** — move `head` to the second node, then `delete` the old first node.
2. **The last node** — walk to the **second-last** node, `delete` the last node, and set the
   second-last node's `next` to `nullptr`.
3. **A node with a given value** — walk until you find the node **just before** the one to be
   deleted, then skip over it by re-linking `next`, and `delete` the removed node.

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

void display(Node *head) {
    Node *p = head;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

Node* insertEnd(Node *head, int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = nullptr;
    if (head == nullptr) return newNode;
    Node *p = head;
    while (p->next != nullptr) p = p->next;
    p->next = newNode;
    return head;
}

// delete the first node
Node* deleteFirst(Node *head) {
    if (head == nullptr) return nullptr;
    Node *temp = head;
    head = head->next;
    delete temp;
    return head;
}

// delete the last node
Node* deleteLast(Node *head) {
    if (head == nullptr || head->next == nullptr) {
        delete head;
        return nullptr;
    }
    Node *p = head;
    while (p->next->next != nullptr)
        p = p->next;
    delete p->next;
    p->next = nullptr;
    return head;
}

// delete a node with a given value
Node* deleteValue(Node *head, int val) {
    if (head == nullptr) return nullptr;

    if (head->data == val) {           // value is in the first node
        Node *temp = head;
        head = head->next;
        delete temp;
        return head;
    }

    Node *p = head;
    while (p->next != nullptr && p->next->data != val)
        p = p->next;

    if (p->next == nullptr) {
        cout << "Value not found" << endl;
        return head;
    }

    Node *temp = p->next;
    p->next = p->next->next;
    delete temp;
    return head;
}

int main() {
    Node *head = nullptr;
    head = insertEnd(head, 10);
    head = insertEnd(head, 20);
    head = insertEnd(head, 30);
    head = insertEnd(head, 40);
    cout << "Start                 : ";
    display(head);

    head = deleteFirst(head);
    cout << "After delete first    : ";
    display(head);

    head = deleteLast(head);
    cout << "After delete last     : ";
    display(head);

    head = insertEnd(head, 25);
    cout << "After insert end (25) : ";
    display(head);

    head = deleteValue(head, 20);
    cout << "After delete value 20 : ";
    display(head);
    return 0;
}
```

**Output**
```
Start                 : 10 20 30 40
After delete first    : 20 30 40
After delete last     : 20 30
After insert end (25) : 20 30 25
After delete value 20 : 30 25
```

**Practice question**

**Q13.** In `deleteValue()`, why do we need to keep a pointer `p` at the node **before** the one
being deleted, instead of directly finding the node to delete?

---

## 14. Header linked lists: grounded and circular

**What it is**

A **header linked list** has one extra special node at the very front, called the **header**
node. It does not store real data — it is just a fixed starting point that never changes, even
if the first real node is inserted or deleted.

| Type | Last node's `next` points to |
|---|---|
| **Grounded** header list | `NULL`, like a normal list |
| **Circular** header list | back to the **header** node, forming a circle |

```
Grounded header list:
[header] -> [10] -> [20] -> [30] -> NULL

Circular header list:
[header] -> [100] -> [200] -> [300] -+
    ^                                |
    +--------------------------------+
```

**Important:** for a circular list, you cannot check `while (p != NULL)` to stop the loop —
`next` never becomes `NULL`, so that would run forever. Instead, stop when you come back to the
**header** (or the starting node) again.

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

int main() {
    // GROUNDED HEADER LINKED LIST
    // header node does not store real data, it is just a starting point
    Node header, n1, n2, n3;
    header.data = 0;              // header value is not used
    header.next = &n1;

    n1.data = 10; n1.next = &n2;
    n2.data = 20; n2.next = &n3;
    n3.data = 30; n3.next = nullptr;         // GROUNDED: last node points to NULL

    cout << "Grounded header list: ";
    Node *p = header.next;                   // start after the header
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;

    // CIRCULAR HEADER LINKED LIST
    Node cheader, c1, c2, c3;
    cheader.data = 0;
    cheader.next = &c1;

    c1.data = 100; c1.next = &c2;
    c2.data = 200; c2.next = &c3;
    c3.data = 300; c3.next = &cheader;       // CIRCULAR: last node points back to header

    cout << "Circular header list: ";
    Node *q = cheader.next;
    while (q != &cheader) {                  // stop when we come back to the header
        cout << q->data << " ";
        q = q->next;
    }
    cout << endl;
    return 0;
}
```

**Output**
```
Grounded header list: 10 20 30
Circular header list: 100 200 300
```

**Practice question**

**Q14.** Why can we not use `while (p != NULL)` to traverse a circular linked list? What should we
check instead?

---

## 15. Two-way (doubly) linked lists

**What it is**

A **doubly (two-way) linked list** gives each node **two** pointers instead of one:

```
+------+------+------+
| prev | data | next |   <- one Node
+------+------+------+
```

- `next` points to the following node (same as a normal linked list).
- `prev` points to the **previous** node.

This lets us walk the list in **both directions** — forward using `next`, and backward using
`prev` — something a normal (singly) linked list cannot do.

```
NULL <- [10] <-> [20] <-> [30] -> NULL
        prev/next   prev/next
```

**Difference from a singly linked list**

| Singly linked list | Doubly linked list |
|---|---|
| One pointer (`next`) per node | Two pointers (`prev`, `next`) per node |
| Can only move forward | Can move forward and backward |
| Less memory per node | More memory per node (extra pointer) |

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *prev;
    Node *next;
};

Node* insertEnd(Node *head, int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = nullptr;

    if (head == nullptr) {
        newNode->prev = nullptr;
        return newNode;
    }
    Node *p = head;
    while (p->next != nullptr)
        p = p->next;
    p->next = newNode;
    newNode->prev = p;
    return head;
}

Node* insertBeginning(Node *head, int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->prev = nullptr;
    newNode->next = head;
    if (head != nullptr)
        head->prev = newNode;
    return newNode;
}

void displayForward(Node *head) {
    Node *p = head;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

void displayBackward(Node *tail) {
    Node *p = tail;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->prev;
    }
    cout << endl;
}

int main() {
    Node *head = nullptr;
    head = insertEnd(head, 20);
    head = insertEnd(head, 30);
    head = insertBeginning(head, 10);

    cout << "Forward  : ";
    displayForward(head);

    // find the last node to traverse backward
    Node *tail = head;
    while (tail->next != nullptr)
        tail = tail->next;

    cout << "Backward : ";
    displayBackward(tail);
    return 0;
}
```

**Output**
```
Forward  : 10 20 30
Backward : 30 20 10
```

**Practice question**

**Q15.** Give one advantage and one disadvantage of a doubly linked list, compared to a singly
linked list.

---
---

# Answers

**Q10.** Two advantages of a linked list over an array:
1. Its **size can grow or shrink** while the program runs — it is not fixed like an array.
2. **Inserting or deleting at the beginning is fast** — no need to shift every other item, we
   just change a few `next` pointers.

One disadvantage: there is **no direct access**. To reach the 5th node, we must start at `head`
and follow `next` pointers one by one — we cannot jump straight to it like `a[5]` in an array.

**Q11.**
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

int sumNodes(Node *head) {
    int sum = 0;
    Node *p = head;
    while (p != nullptr) {
        sum += p->data;
        p = p->next;
    }
    return sum;
}
```

**Q12.** If we updated `head` to the new node **first**, we would lose the address of the old
first node forever — nothing would point to it anymore, and the rest of the list would be lost.
That is why the new node's `next` must be linked to the old `head` **first**, and only after that
should `head` be changed to point to the new node.

**Q13.** We need a pointer `p` at the node **before** the one being deleted because a singly
linked list has no `prev` pointer. To remove a node from the chain, we must change the `next` of
the node **before** it (skipping over the node being deleted). If we only had a pointer to the
node being deleted itself, we would have no way to reach the node before it to fix its `next`.

**Q14.** We cannot use `while (p != NULL)` because in a circular list, the last node's `next`
does not point to `NULL` — it points back into the list (to the first node or the header). So `p`
would never become `NULL`, and the loop would run forever. Instead, we should check whether `p`
has come back to the **starting node** (or header) again, and stop there.

**Q15.** Advantage: a doubly linked list can be traversed **backward as well as forward**, using
the `prev` pointer — a singly linked list can only move forward. Disadvantage: it uses **more
memory**, because every node needs an extra `prev` pointer in addition to `next`.

---

[Back to top](#dsa--unit-2)
