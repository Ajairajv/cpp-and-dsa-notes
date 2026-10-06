# DSA — Unit 3

Simple notes for all Unit 3 topics. All programs are in **C++**.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**
```bash
g++ program.cpp -o program
./program
```

### Topics
16. [Stack: introduction and array representation](#16-stack-introduction-and-array-representation)
17. [Stack: linked list representation](#17-stack-linked-list-representation)
18. [Arithmetic expressions and Polish notation](#18-arithmetic-expressions-and-polish-notation)
19. [Evaluation of postfix and prefix expressions](#19-evaluation-of-postfix-and-prefix-expressions)
20. [Transformation: infix to postfix and prefix](#20-transformation-infix-to-postfix-and-prefix)
21. [Queue: introduction and array representation](#21-queue-introduction-and-array-representation)
22. [Circular queue](#22-circular-queue)
23. [Queue: linked list representation](#23-queue-linked-list-representation)
24. [Priority queues](#24-priority-queues)
25. [Deques (double-ended queues)](#25-deques-double-ended-queues)

---

## 16. Stack: introduction and array representation

**What it is**

A **stack** is a linear data structure where items are added and removed from **one end only**.
This end is called the **top**.

Think of a pile of plates. You put a new plate on the top, and you also take a plate from the
top. The plate you put **last** is the one you take out **first**. This rule is called
**LIFO — Last In, First Out**.

```
        push 40 |      | pop
                v      ^
             +------+
   top -->   |  30  |   <- last in, so first out
             +------+
             |  20  |
             +------+
             |  10  |   <- first in, so last out
             +------+
```

**Operations on a stack**

| Operation | What it does |
|---|---|
| **push** | Add an item on the top |
| **pop** | Remove the top item |
| **peek** (or top) | Only look at the top item, do not remove it |
| **traversal** (display) | Visit every item, from top to bottom |
| **isEmpty / isFull** | Check if the stack is empty / full |

**Array representation**

We use an array `stackArr[MAX]` and an integer `top`, which stores the index of the top item.

- At the start, `top = -1` (the stack is empty).
- **push:** first `top++`, then `stackArr[top] = value`.
- **pop:** first take `stackArr[top]`, then `top--`.

```
index:     0    1    2    3    4        (MAX = 5)
         +----+----+----+----+----+
         | 10 | 20 | 30 |    |    |
         +----+----+----+----+----+
                     ^
                    top = 2
```

**Two special cases**

| Case | When it happens | Condition |
|---|---|---|
| **Overflow** | You try to **push** into a stack that is already **full** | `top == MAX - 1` |
| **Underflow** | You try to **pop** from a stack that is **empty** | `top == -1` |

**Program**

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int stackArr[MAX];     // array to hold the stack items
int top = -1;          // top = -1 means the stack is empty

// PUSH: add an item on the top
void push(int val) {
    if (top == MAX - 1) {
        cout << "Stack Overflow! Cannot push " << val << endl;
        return;
    }
    top++;
    stackArr[top] = val;
    cout << "Pushed " << val << endl;
}

// POP: remove the top item and return it
int pop() {
    if (top == -1) {
        cout << "Stack Underflow! Nothing to pop" << endl;
        return -1;
    }
    int val = stackArr[top];
    top--;
    return val;
}

// PEEK: only look at the top item (do not remove it)
int peek() {
    if (top == -1) {
        cout << "Stack is empty" << endl;
        return -1;
    }
    return stackArr[top];
}

// TRAVERSAL: print all items from top to bottom
void display() {
    if (top == -1) {
        cout << "Stack is empty" << endl;
        return;
    }
    cout << "Stack (top to bottom): ";
    for (int i = top; i >= 0; i--)
        cout << stackArr[i] << " ";
    cout << endl;
}

int main() {
    push(10);
    push(20);
    push(30);
    push(40);
    push(50);
    push(60);              // stack is full, so this gives overflow
    display();

    cout << "Top item (peek) = " << peek() << endl;

    int x = pop();
    cout << "Popped " << x << endl;
    x = pop();
    cout << "Popped " << x << endl;
    display();

    while (top != -1)      // pop everything that is left
        pop();
    display();
    pop();                 // stack is empty, so this gives underflow
    return 0;
}
```

**Output**
```
Pushed 10
Pushed 20
Pushed 30
Pushed 40
Pushed 50
Stack Overflow! Cannot push 60
Stack (top to bottom): 50 40 30 20 10
Top item (peek) = 50
Popped 50
Popped 40
Stack (top to bottom): 30 20 10
Stack is empty
Stack Underflow! Nothing to pop
```

**Practice question**

**Q16.** Write a C++ program that uses an array stack to **reverse a word**. Push every letter of
`"STACK"`, then pop them all back. What is printed?

---

## 17. Stack: linked list representation

**What it is**

An array stack has a **fixed size** (`MAX`). If we do not know how many items will come, we can
build the stack using a **linked list** instead.

- The **first node** of the list is the **top** of the stack.
- **push** = insert a new node **at the beginning** (same as Unit 2, topic 12).
- **pop** = delete the **first node** (same as Unit 2, topic 13).

Both operations happen at the beginning, so they are fast — no need to walk the whole list.

```
top
 |
 v
+----+----+     +----+----+     +----+-----+
| 25 |  *-+---->| 15 |  *-+---->|  5 | NULL|
+----+----+     +----+----+     +----+-----+
(pushed last)                   (pushed first)
```

**Array stack vs Linked list stack**

| Array stack | Linked list stack |
|---|---|
| Fixed size (`MAX`) | No fixed size, grows while the program runs |
| **Overflow** can happen when the array is full | No overflow (only if the computer's memory runs out) |
| `top` is an **index** (int) | `top` is a **pointer** to the first node |
| Empty when `top == -1` | Empty when `top == nullptr` |
| No extra memory for links | Extra memory for the `next` pointer in every node |

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

Node *top = nullptr;      // top of the stack (empty at the start)

// PUSH: insert a new node at the beginning
void push(int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = top;   // new node points to old top
    top = newNode;         // new node becomes the top
    cout << "Pushed " << val << endl;
}

// POP: delete the first node
int pop() {
    if (top == nullptr) {
        cout << "Stack Underflow! Nothing to pop" << endl;
        return -1;
    }
    Node *temp = top;
    int val = temp->data;
    top = top->next;       // second node becomes the top
    delete temp;
    return val;
}

int peek() {
    if (top == nullptr) {
        cout << "Stack is empty" << endl;
        return -1;
    }
    return top->data;
}

void display() {
    if (top == nullptr) {
        cout << "Stack is empty" << endl;
        return;
    }
    cout << "Stack (top to bottom): ";
    Node *p = top;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

int main() {
    push(5);
    push(15);
    push(25);
    display();

    cout << "Top item (peek) = " << peek() << endl;

    int x = pop();
    cout << "Popped " << x << endl;
    display();

    pop();
    pop();
    display();
    pop();                 // nothing left, so this gives underflow
    return 0;
}
```

**Output**
```
Pushed 5
Pushed 15
Pushed 25
Stack (top to bottom): 25 15 5
Top item (peek) = 25
Popped 25
Stack (top to bottom): 15 5
Stack is empty
Stack Underflow! Nothing to pop
```

**Practice question**

**Q17.** In a linked list stack, why do we push and pop at the **beginning** of the list, and not
at the end?

---

## 18. Arithmetic expressions and Polish notation

**What it is**

An arithmetic expression has **operands** (values like `A`, `B`, `5`) and **operators**
(`+ - * / ^`). There are **three** ways to write the same expression:

| Notation | Where the operator goes | Example |
|---|---|---|
| **Infix** | **Between** the operands | `A + B` |
| **Prefix** (Polish notation) | **Before** the operands | `+ A B` |
| **Postfix** (Reverse Polish notation) | **After** the operands | `A B +` |

Prefix is called **Polish notation** because it was invented by a Polish mathematician, **Jan
Łukasiewicz**. Postfix is called **Reverse Polish notation (RPN)**.

**Why do we need prefix and postfix?**

- Infix is easy for **humans**, but hard for the computer — it needs brackets and precedence rules
  to know what to do first.
- Prefix and postfix need **no brackets** and **no precedence rules**. The order of the symbols
  already tells the computer what to do first.
- So a computer (compiler) usually changes infix to **postfix**, and then evaluates the postfix
  using a **stack**.

**Precedence and associativity**

**Precedence** tells which operator is done first. **Associativity** tells the order when two
operators have the **same** precedence.

| Operator | Precedence | Associativity |
|---|---|---|
| `( )` brackets | done first | — |
| `^` (power) | Highest (3) | **Right to left** (`A^B^C` = `A^(B^C)`) |
| `*` `/` | Middle (2) | Left to right (`A/B*C` = `(A/B)*C`) |
| `+` `-` | Lowest (1) | Left to right (`A-B+C` = `(A-B)+C`) |

**How to convert by hand (bracket method)**

1. Put brackets around each part, following precedence and associativity.
2. Convert the **innermost** bracket first. Move its operator to the **front** (for prefix) or to
   the **end** (for postfix).
3. Keep going outward, treating each converted part as one operand.

**Example 1:** `A + B * C` (`*` is done first)

```
Postfix:  A + (B * C)  ->  A + (BC*)  ->  A BC* +   =  ABC*+
Prefix:   A + (B * C)  ->  A + (*BC)  ->  + A *BC   =  +A*BC
```

**Example 2:** `(A + B) * (C - D)`

```
Postfix:  (AB+) * (CD-)  ->  AB+ CD- *   =  AB+CD-*
Prefix:   (+AB) * (-CD)  ->  * +AB -CD   =  *+AB-CD
```

**Example 3:** `A + B * C - D / E`  (`*` and `/` first, then `+` and `-` from left to right)

```
Brackets: ((A + (B * C)) - (D / E))
Postfix:  ((A BC* +) - (DE/))  ->  ABC*+ DE/ -   =  ABC*+DE/-
Prefix:   ((+ A *BC) - (/DE))  ->  - +A*BC /DE   =  -+A*BC/DE
```

**More examples** (all checked by a program)

| Infix | Postfix | Prefix |
|---|---|---|
| `A+B` | `AB+` | `+AB` |
| `A+B*C` | `ABC*+` | `+A*BC` |
| `(A+B)*C` | `AB+C*` | `*+ABC` |
| `A-B+C` | `AB-C+` | `+-ABC` |
| `A^B^C` | `ABC^^` | `^A^BC` |
| `(A+B)*(C-D)` | `AB+CD-*` | `*+AB-CD` |
| `A*(B+C)/D` | `ABC+*D/` | `/*A+BCD` |
| `A+B*(C-D)/E` | `ABCD-*E/+` | `+A/*B-CDE` |
| `(A+B)*C-D/E` | `AB+C*DE/-` | `-*+ABC/DE` |

**Tip:** in all three notations, the operands (`A`, `B`, `C` ...) stay in the **same order**. Only
the operators move.

**Program**

This program prints the precedence values, and finds the notation of an expression just by
looking at its **first** and **last** symbol.

```cpp
#include <iostream>
#include <cstring>
using namespace std;

bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/' || c == '^';
}

// bigger number = higher precedence (done first)
int precedence(char op) {
    if (op == '^') return 3;
    if (op == '*' || op == '/') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;
}

// look at the first and last symbol to find the notation
void findNotation(const char exp[]) {
    int n = strlen(exp);
    cout << exp << " -> ";
    if (isOperator(exp[0]))
        cout << "Prefix (operator comes first)" << endl;
    else if (isOperator(exp[n - 1]))
        cout << "Postfix (operator comes last)" << endl;
    else
        cout << "Infix (operator is in between)" << endl;
}

int main() {
    cout << "Precedence: ^ = " << precedence('^')
         << ", * / = " << precedence('*')
         << ", + - = " << precedence('+') << endl;

    findNotation("A+B");
    findNotation("+AB");
    findNotation("AB+");
    findNotation("A+B*C");
    findNotation("+A*BC");
    findNotation("ABC*+");
    return 0;
}
```

**Output**
```
Precedence: ^ = 3, * / = 2, + - = 1
A+B -> Infix (operator is in between)
+AB -> Prefix (operator comes first)
AB+ -> Postfix (operator comes last)
A+B*C -> Infix (operator is in between)
+A*BC -> Prefix (operator comes first)
ABC*+ -> Postfix (operator comes last)
```

**Practice question**

**Q18.** Convert these infix expressions to **postfix** and **prefix** by hand:
(a) `(A + B) * C - D`
(b) `A * B + C / D`

---

## 19. Evaluation of postfix and prefix expressions

**What it is**

"Evaluation" means finding the **final value** of an expression. A postfix or prefix expression
is evaluated very easily using **one stack**.

**Algorithm: evaluate a POSTFIX expression** (scan from **left to right**)

1. Read the next symbol.
2. If it is an **operand**, **push** it on the stack.
3. If it is an **operator**:
   - pop the top item → this is the **right** operand `B`
   - pop the next item → this is the **left** operand `A`
   - find `A operator B` and **push** the result back.
4. Repeat till the end. The **one** value left on the stack is the answer.

**Example:** postfix `5 3 + 8 2 - *`  (infix: `(5 + 3) * (8 - 2)`)

| Symbol | Action | Stack (bottom → top) |
|---|---|---|
| 5 | push | 5 |
| 3 | push | 5 3 |
| + | pop 3, pop 5, 5 + 3 = 8, push | 8 |
| 8 | push | 8 8 |
| 2 | push | 8 8 2 |
| - | pop 2, pop 8, 8 - 2 = 6, push | 8 6 |
| * | pop 6, pop 8, 8 * 6 = 48, push | 48 |

Answer = **48**

**Careful with `-` and `/`:** the **first** popped item goes on the **right**. For `8 2 -`, we pop
2 first, then 8, and do `8 - 2 = 6` (not `2 - 8`).

**Algorithm: evaluate a PREFIX expression** (scan from **right to left**)

Same idea, but we read the expression **from the end**. Now the **first** popped item is the
**left** operand `A`, and the second popped item is the **right** operand `B`.

**Example:** prefix `* + 2 3 - 8 4`  (infix: `(2 + 3) * (8 - 4)`)

| Symbol (right to left) | Action | Stack (bottom → top) |
|---|---|---|
| 4 | push | 4 |
| 8 | push | 4 8 |
| - | pop 8, pop 4, 8 - 4 = 4, push | 4 |
| 3 | push | 4 3 |
| 2 | push | 4 3 2 |
| + | pop 2, pop 3, 2 + 3 = 5, push | 4 5 |
| * | pop 5, pop 4, 5 * 4 = 20, push | 20 |

Answer = **20**

**Program**

(Operands are single digits `0`–`9`, so each character is one symbol.)

```cpp
#include <iostream>
#include <iomanip>
#include <cstring>
using namespace std;

int st[50];
int top = -1;

void push(int x) { st[++top] = x; }
int  pop()       { return st[top--]; }

void showStack() {
    for (int i = 0; i <= top; i++)          // bottom to top
        cout << st[i] << " ";
    cout << endl;
}

int power(int a, int b) {
    int r = 1;
    for (int i = 0; i < b; i++) r = r * a;
    return r;
}

int apply(int a, char op, int b) {
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
        case '^': return power(a, b);
    }
    return 0;
}

// POSTFIX: scan LEFT to RIGHT
int evalPostfix(const char exp[]) {
    top = -1;
    cout << "Postfix: " << exp << endl;
    cout << left << setw(8) << "Symbol" << setw(14) << "Action" << "Stack" << endl;
    for (int i = 0; exp[i] != '\0'; i++) {
        char c = exp[i];
        cout << setw(8) << c;
        if (c >= '0' && c <= '9') {
            push(c - '0');                   // operand: push it
            cout << setw(14) << "push";
        } else {
            int b = pop();                   // first pop  = RIGHT operand
            int a = pop();                   // second pop = LEFT operand
            int r = apply(a, c, b);
            push(r);
            cout << a << " " << c << " " << b << " = " << setw(6) << r;
        }
        showStack();
    }
    return pop();
}

// PREFIX: scan RIGHT to LEFT
int evalPrefix(const char exp[]) {
    top = -1;
    cout << "Prefix: " << exp << endl;
    cout << left << setw(8) << "Symbol" << setw(14) << "Action" << "Stack" << endl;
    for (int i = strlen(exp) - 1; i >= 0; i--) {
        char c = exp[i];
        cout << setw(8) << c;
        if (c >= '0' && c <= '9') {
            push(c - '0');
            cout << setw(14) << "push";
        } else {
            int a = pop();                   // first pop  = LEFT operand
            int b = pop();                   // second pop = RIGHT operand
            int r = apply(a, c, b);
            push(r);
            cout << a << " " << c << " " << b << " = " << setw(6) << r;
        }
        showStack();
    }
    return pop();
}

int main() {
    int r1 = evalPostfix("53+82-*");
    cout << "Result = " << r1 << endl << endl;

    int r2 = evalPrefix("*+23-84");
    cout << "Result = " << r2 << endl;
    return 0;
}
```

**Output**
```
Postfix: 53+82-*
Symbol  Action        Stack
5       push          5
3       push          5 3
+       5 + 3 = 8     8
8       push          8 8
2       push          8 8 2
-       8 - 2 = 6     8 6
*       8 * 6 = 48    48
Result = 48

Prefix: *+23-84
Symbol  Action        Stack
4       push          4
8       push          4 8
-       8 - 4 = 4     4
3       push          4 3
2       push          4 3 2
+       2 + 3 = 5     4 5
*       5 * 4 = 20    20
Result = 20
```

**Practice question**

**Q19.** Evaluate the postfix expression `6 2 3 + - 3 8 2 / + *` using a stack. Show the stack
after every symbol.

---

## 20. Transformation: infix to postfix and prefix

**What it is**

"Transformation" means **changing** an infix expression into postfix (or prefix). A computer does
this using a **stack of operators**.

**Algorithm: infix → postfix** (scan from **left to right**)

1. **Operand** (`A`, `B`, ...) → write it directly to the postfix output.
2. **`(`** → push it on the stack.
3. **`)`** → pop operators to the output until `(` comes. Then pop the `(` too (do not write it).
4. **Operator** → while the stack top is an operator with **higher** precedence (or **equal**
   precedence, for left-to-right operators), pop it to the output. Then push the new operator.
   (For `^`, which is right-to-left, pop only if the top has **higher** precedence.)
5. At the end → pop **everything** left on the stack to the output.

**Example:** `A + B * (C - D) / E`

| Symbol | Stack | Postfix |
|---|---|---|
| A | | A |
| + | + | A |
| B | + | AB |
| * | + * | AB |
| ( | + * ( | AB |
| C | + * ( | ABC |
| - | + * ( - | ABC |
| D | + * ( - | ABCD |
| ) | + * | ABCD- |
| / | + / | ABCD-* |
| E | + / | ABCD-*E |
| (end) | | ABCD-*E/+ |

Postfix = **`ABCD-*E/+`**

(When `/` came, the top was `*` with the **same** precedence, so `*` was popped first. `+` has
lower precedence, so it stayed.)

**Algorithm: infix → prefix**

1. **Reverse** the infix expression. While reversing, change every `(` to `)` and every `)` to `(`.
2. Find the **postfix** of this reversed expression (same algorithm as above, with one small
   change: for equal precedence, pop only for `^`).
3. **Reverse** the result. That is the prefix.

**Example:** `(A + B) * C`

```
Step 1: reverse          ->  C * (B + A)
Step 2: postfix of that  ->  C B A + *
Step 3: reverse          ->  * + A B C      =  *+ABC
```

**Program**

```cpp
#include <iostream>
#include <iomanip>
#include <string>
using namespace std;

char st[50];
int top = -1;

void push(char c) { st[++top] = c; }
char pop()        { return st[top--]; }
char peek()       { return st[top]; }
bool isEmpty()    { return top == -1; }

int precedence(char op) {
    if (op == '^') return 3;
    if (op == '*' || op == '/') return 2;
    if (op == '+' || op == '-') return 1;
    return 0;                       // for '('
}

bool isOperand(char c) {
    return (c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9');
}

string stackText() {
    string s = "";
    for (int i = 0; i <= top; i++) s += st[i];
    return s;
}

// INFIX -> POSTFIX (set showSteps = true to print the table)
string toPostfix(string infix, bool showSteps) {
    top = -1;
    string post = "";
    if (showSteps)
        cout << left << setw(8) << "Symbol" << setw(10) << "Stack" << "Postfix" << endl;

    for (int i = 0; i < (int)infix.length(); i++) {
        char c = infix[i];
        if (isOperand(c)) {
            post += c;                              // 1. operand -> output
        } else if (c == '(') {
            push(c);                                // 2. '(' -> push
        } else if (c == ')') {
            while (peek() != '(')                   // 3. ')' -> pop till '('
                post += pop();
            pop();                                  //    remove '(' itself
        } else {                                    // 4. operator
            while (!isEmpty() && peek() != '(' &&
                   (precedence(peek()) > precedence(c) ||
                    (precedence(peek()) == precedence(c) && c != '^')))
                post += pop();
            push(c);
        }
        if (showSteps)
            cout << setw(8) << c << setw(10) << stackText() << post << endl;
    }
    while (!isEmpty())                              // 5. pop what is left
        post += pop();
    if (showSteps)
        cout << setw(8) << "(end)" << setw(10) << stackText() << post << endl;
    return post;
}

// INFIX -> PREFIX
string toPrefix(string infix) {
    // step 1: reverse the infix and swap '(' with ')'
    string rev = "";
    for (int i = infix.length() - 1; i >= 0; i--) {
        char c = infix[i];
        if (c == '(') c = ')';
        else if (c == ')') c = '(';
        rev += c;
    }
    // step 2: get the "postfix" of the reversed string
    //         (equal precedence: pop only for '^')
    top = -1;
    string out = "";
    for (int i = 0; i < (int)rev.length(); i++) {
        char c = rev[i];
        if (isOperand(c)) out += c;
        else if (c == '(') push(c);
        else if (c == ')') {
            while (peek() != '(') out += pop();
            pop();
        } else {
            while (!isEmpty() && peek() != '(' &&
                   (precedence(peek()) > precedence(c) ||
                    (precedence(peek()) == precedence(c) && c == '^')))
                out += pop();
            push(c);
        }
    }
    while (!isEmpty()) out += pop();

    // step 3: reverse the result
    string pre = "";
    for (int i = out.length() - 1; i >= 0; i--) pre += out[i];
    return pre;
}

int main() {
    string e = "A+B*(C-D)/E";
    cout << "Infix: " << e << endl;
    string p = toPostfix(e, true);
    cout << "Postfix: " << p << endl << endl;

    string list[] = {"A+B*C", "(A+B)*C", "A-B+C", "A^B^C", "A*(B+C)/D"};
    for (int i = 0; i < 5; i++) {
        cout << left << setw(12) << list[i]
             << "Postfix: " << setw(10) << toPostfix(list[i], false)
             << "Prefix: " << toPrefix(list[i]) << endl;
    }
    return 0;
}
```

**Output**
```
Infix: A+B*(C-D)/E
Symbol  Stack     Postfix
A                 A
+       +         A
B       +         AB
*       +*        AB
(       +*(       AB
C       +*(       ABC
-       +*(-      ABC
D       +*(-      ABCD
)       +*        ABCD-
/       +/        ABCD-*
E       +/        ABCD-*E
(end)             ABCD-*E/+
Postfix: ABCD-*E/+

A+B*C       Postfix: ABC*+     Prefix: +A*BC
(A+B)*C     Postfix: AB+C*     Prefix: *+ABC
A-B+C       Postfix: AB-C+     Prefix: +-ABC
A^B^C       Postfix: ABC^^     Prefix: ^A^BC
A*(B+C)/D   Postfix: ABC+*D/   Prefix: /*A+BCD
```

**Practice question**

**Q20.** Convert the infix expression `A + ( B * C - ( D / E ^ F ) * G ) * H` to **postfix**
using a stack. Show the stack and output after each symbol.

---

## 21. Queue: introduction and array representation

**What it is**

A **queue** is a linear data structure where items are **inserted at one end** and **deleted from
the other end**.

- The end where we insert is called the **rear**.
- The end where we delete is called the **front**.

Think of a line at a ticket counter. A new person joins at the **back** (rear), and the person at
the **front** gets the ticket and leaves first. This rule is called **FIFO — First In, First Out**.

```
 delete here                          insert here
 (dequeue)                            (enqueue)
     <---   +----+----+----+----+   <---
            | 10 | 20 | 30 | 40 |
            +----+----+----+----+
              ^              ^
            front           rear
```

**Stack vs Queue**

| Stack | Queue |
|---|---|
| LIFO — Last In, First Out | FIFO — First In, First Out |
| Insert and delete at the **same** end (top) | Insert at **rear**, delete from **front** |
| One pointer/index: `top` | Two pointers/indexes: `front` and `rear` |
| Example: pile of plates, undo button | Example: ticket line, printer jobs |

**Operations on a queue**

| Operation | What it does |
|---|---|
| **enqueue** (insertion) | Add an item at the **rear** |
| **dequeue** (deletion) | Remove the item at the **front** |
| **traversal** (display) | Visit every item from front to rear |

**Array representation**

We use an array `queueArr[MAX]` and two indexes, `front` and `rear`. At the start both are `-1`.

- **enqueue:** `rear++`, then `queueArr[rear] = value` (also set `front = 0` for the first item).
- **dequeue:** take `queueArr[front]`, then `front++`.
- **Overflow:** `rear == MAX - 1`. **Underflow (empty):** `front == -1` or `front > rear`.

**The problem with a simple (linear) array queue**

`front` and `rear` only move **forward**. After some deletions, the boxes at the start of the
array become free, but we **cannot use them again**. The queue says "full" even when it has
empty space.

```
After deleting 10 and 20, and inserting 40 and 50 (MAX = 5):

index:   0    1    2    3    4
       +----+----+----+----+----+
       |    |    | 30 | 40 | 50 |
       +----+----+----+----+----+
       (free)(free) ^         ^
                  front     rear = MAX-1  ->  "Overflow!" even though 2 boxes are free
```

The program below shows this problem. The fix is the **circular queue** (next topic).

**Program**

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int queueArr[MAX];
int front = -1, rear = -1;     // -1 means the queue is empty

// ENQUEUE: insert at the REAR
void enqueue(int val) {
    if (rear == MAX - 1) {
        cout << "Queue Overflow! Cannot insert " << val << endl;
        return;
    }
    if (front == -1)           // first item
        front = 0;
    rear++;
    queueArr[rear] = val;
    cout << "Inserted " << val << endl;
}

// DEQUEUE: delete from the FRONT
int dequeue() {
    if (front == -1 || front > rear) {
        cout << "Queue Underflow! Nothing to delete" << endl;
        return -1;
    }
    int val = queueArr[front];
    front++;
    return val;
}

// TRAVERSAL: print from front to rear
void display() {
    if (front == -1 || front > rear) {
        cout << "Queue is empty" << endl;
        return;
    }
    cout << "Queue (front to rear): ";
    for (int i = front; i <= rear; i++)
        cout << queueArr[i] << " ";
    cout << endl;
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    display();

    int x = dequeue();
    cout << "Deleted " << x << endl;
    x = dequeue();
    cout << "Deleted " << x << endl;
    display();

    enqueue(40);
    enqueue(50);
    enqueue(60);          // rear is at the end, so "full" even though
                          // index 0 and 1 are free now!
    display();
    cout << "front = " << front << ", rear = " << rear << endl;
    return 0;
}
```

**Output**
```
Inserted 10
Inserted 20
Inserted 30
Queue (front to rear): 10 20 30
Deleted 10
Deleted 20
Queue (front to rear): 30
Inserted 40
Inserted 50
Queue Overflow! Cannot insert 60
Queue (front to rear): 30 40 50
front = 2, rear = 4
```

**Practice question**

**Q21.** In the program above, the queue had 2 free boxes, but inserting `60` still gave
"Overflow". Why? How can we fix this?

---

## 22. Circular queue

**What it is**

In a **circular queue**, the last box of the array is joined back to the first box, like a
circle. When `rear` reaches the last index, it **wraps around** to index `0` (if that box is
free). So no space is wasted.

```
             [0]
         +---------+
   [4]   |         |   [1]
         |  circle |
   [3]   |         |   [2]
         +---------+
   after index 4, the next index is 0 again
```

The wrap-around is done with the **`%` (modulus)** operator:

| Action | Formula |
|---|---|
| Move rear forward | `rear = (rear + 1) % MAX` |
| Move front forward | `front = (front + 1) % MAX` |
| Queue is **full** | `(rear + 1) % MAX == front` |
| Queue is **empty** | `front == -1` |

Example with `MAX = 5`: if `rear = 4`, then `(4 + 1) % 5 = 0`, so the next item goes to index 0.

```
After inserting 10..50, deleting 10 and 20, then inserting 60 and 70:

index:   0    1    2    3    4
       +----+----+----+----+----+
       | 60 | 70 | 30 | 40 | 50 |
       +----+----+----+----+----+
              ^    ^
            rear  front

Order from front to rear: 30 40 50 60 70
```

**When only one item is left** and we delete it, we set `front = rear = -1` again, so the queue
becomes empty.

**Program**

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int cq[MAX];
int front = -1, rear = -1;

bool isFull()  { return (rear + 1) % MAX == front; }
bool isEmpty() { return front == -1; }

void enqueue(int val) {
    if (isFull()) {
        cout << "Queue Overflow! Cannot insert " << val << endl;
        return;
    }
    if (isEmpty())
        front = 0;
    rear = (rear + 1) % MAX;          // wrap around to 0 after the last index
    cq[rear] = val;
    cout << "Inserted " << val << " at index " << rear << endl;
}

int dequeue() {
    if (isEmpty()) {
        cout << "Queue Underflow! Nothing to delete" << endl;
        return -1;
    }
    int val = cq[front];
    if (front == rear)                 // that was the only item
        front = rear = -1;
    else
        front = (front + 1) % MAX;
    return val;
}

void display() {
    if (isEmpty()) {
        cout << "Queue is empty" << endl;
        return;
    }
    cout << "Queue (front to rear): ";
    int i = front;
    while (true) {
        cout << cq[i] << " ";
        if (i == rear) break;
        i = (i + 1) % MAX;
    }
    cout << endl;
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    enqueue(40);
    enqueue(50);
    enqueue(60);              // full

    int x = dequeue();
    cout << "Deleted " << x << endl;
    x = dequeue();
    cout << "Deleted " << x << endl;

    enqueue(60);              // goes to index 0 (wraps around)
    enqueue(70);              // goes to index 1
    display();
    cout << "front = " << front << ", rear = " << rear << endl;

    while (!isEmpty())
        dequeue();
    display();
    return 0;
}
```

**Output**
```
Inserted 10 at index 0
Inserted 20 at index 1
Inserted 30 at index 2
Inserted 40 at index 3
Inserted 50 at index 4
Queue Overflow! Cannot insert 60
Deleted 10
Deleted 20
Inserted 60 at index 0
Inserted 70 at index 1
Queue (front to rear): 30 40 50 60 70
front = 2, rear = 1
Queue is empty
```

**Practice question**

**Q22.** A circular queue has `MAX = 5`, `front = 3` and `rear = 1`.
(a) How many items are in the queue?
(b) At which index will the next item be inserted?
(c) Is the queue full?

---

## 23. Queue: linked list representation

**What it is**

A queue can also be made using a **linked list**. Then it has **no fixed size**, and there is no
wasted space problem.

We keep **two** pointers:
- `front` → the **first** node (we **delete** from here)
- `rear` → the **last** node (we **insert** after this)

```
front                              rear
  |                                  |
  v                                  v
+-----+---+     +-----+---+     +-----+-----+
| 200 | *-+---->| 300 | *-+---->| 400 | NULL|
+-----+---+     +-----+---+     +-----+-----+
```

- **enqueue** = insert at the **end**. Because we have `rear`, we do not need to walk the whole
  list — just `rear->next = newNode` and `rear = newNode`.
- **dequeue** = delete the **first** node (move `front` to `front->next`).
- If the queue becomes empty after a delete, set **both** `front` and `rear` to `nullptr`.

**Program**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node *next;
};

Node *front = nullptr;     // delete from here
Node *rear  = nullptr;     // insert here

// ENQUEUE: insert at the end (rear)
void enqueue(int val) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->next = nullptr;

    if (rear == nullptr) {         // queue was empty
        front = rear = newNode;
    } else {
        rear->next = newNode;      // link old rear to new node
        rear = newNode;            // new node is the rear now
    }
    cout << "Inserted " << val << endl;
}

// DEQUEUE: delete from the beginning (front)
int dequeue() {
    if (front == nullptr) {
        cout << "Queue Underflow! Nothing to delete" << endl;
        return -1;
    }
    Node *temp = front;
    int val = temp->data;
    front = front->next;
    if (front == nullptr)          // queue became empty
        rear = nullptr;
    delete temp;
    return val;
}

void display() {
    if (front == nullptr) {
        cout << "Queue is empty" << endl;
        return;
    }
    cout << "Queue (front to rear): ";
    Node *p = front;
    while (p != nullptr) {
        cout << p->data << " ";
        p = p->next;
    }
    cout << endl;
}

int main() {
    enqueue(100);
    enqueue(200);
    enqueue(300);
    display();

    int x = dequeue();
    cout << "Deleted " << x << endl;
    display();

    enqueue(400);
    display();

    dequeue();
    dequeue();
    dequeue();
    display();
    dequeue();                     // nothing left, so this gives underflow
    return 0;
}
```

**Output**
```
Inserted 100
Inserted 200
Inserted 300
Queue (front to rear): 100 200 300
Deleted 100
Queue (front to rear): 200 300
Inserted 400
Queue (front to rear): 200 300 400
Queue is empty
Queue Underflow! Nothing to delete
```

**Practice question**

**Q23.** In `dequeue()`, why do we also set `rear = nullptr` when `front` becomes `nullptr`? What
can go wrong if we forget it?

---

## 24. Priority queues

**What it is**

A **priority queue** is a queue where every item has a **priority** (importance). The item with
the **highest priority** is deleted **first**, even if it came later.

**Rules**
1. An item with **higher priority** is served **before** an item with lower priority.
2. Two items with the **same** priority are served in the order they came (**FIFO**).

Real-life example: in a hospital, a serious patient is treated first, even if they came after
others. The CPU also uses priority queues to choose which job to run next.

In these notes, a **smaller number = higher priority** (priority 1 is the most important).

**Ways to represent a priority queue**

| Representation | Idea |
|---|---|
| **One-way (linked) list, kept sorted** | Each node has `data`, `priority`, `next`. Insert the new node at the right place so the list stays sorted by priority. Delete is always from the front. |
| **Array (sorted)** | Same idea using an array: keep it sorted by priority, delete the front item. Insert needs shifting. |
| **Array of queues (2-D array)** | One separate queue (row) for each priority level. Delete from the first non-empty queue. |
| **Heap** | A special tree, used by `std::priority_queue` in C++ (you will study heaps later). |

**Sorted linked list representation**

```
Insert A(3), B(1), C(2), D(1), E(4):

front
  |
  v
[B|1] -> [D|1] -> [C|2] -> [A|3] -> [E|4] -> NULL
  ^ deleted first

D has the same priority as B, but came later, so it goes AFTER B.
```

**Program**

The last part of the program also shows the ready-made `priority_queue` from the C++ STL. By
default it gives the **largest** value first.

```cpp
#include <iostream>
#include <queue>
using namespace std;

// Each node stores: data, its priority, and the next address
// RULE: smaller priority number = more important (served first)
struct Node {
    char data;
    int priority;
    Node *next;
};

Node *front = nullptr;

// INSERT: keep the list SORTED by priority
void insert(char val, int pr) {
    Node *newNode = new Node;
    newNode->data = val;
    newNode->priority = pr;

    // goes at the front if the list is empty, or it is more important than front
    if (front == nullptr || pr < front->priority) {
        newNode->next = front;
        front = newNode;
    } else {
        // move ahead while the next node has priority <= pr
        // ("<=" keeps the first-come-first-served order for equal priority)
        Node *p = front;
        while (p->next != nullptr && p->next->priority <= pr)
            p = p->next;
        newNode->next = p->next;
        p->next = newNode;
    }
    cout << "Inserted " << val << " (priority " << pr << ")" << endl;
}

// DELETE: always remove the front node (highest priority)
char removeTop() {
    if (front == nullptr) {
        cout << "Priority queue is empty" << endl;
        return '-';
    }
    Node *temp = front;
    char val = temp->data;
    front = front->next;
    delete temp;
    return val;
}

void display() {
    cout << "Priority queue: ";
    Node *p = front;
    while (p != nullptr) {
        cout << p->data << "(" << p->priority << ") ";
        p = p->next;
    }
    cout << endl;
}

int main() {
    insert('A', 3);
    insert('B', 1);
    insert('C', 2);
    insert('D', 1);         // same priority as B, so it goes after B
    insert('E', 4);
    display();

    char x = removeTop();
    cout << "Deleted " << x << endl;
    x = removeTop();
    cout << "Deleted " << x << endl;
    display();

    // Ready-made priority queue in C++ STL (bigger value comes out first)
    priority_queue<int> pq;
    pq.push(30);
    pq.push(10);
    pq.push(50);
    pq.push(20);
    cout << "STL priority_queue: ";
    while (!pq.empty()) {
        cout << pq.top() << " ";
        pq.pop();
    }
    cout << endl;
    return 0;
}
```

**Output**
```
Inserted A (priority 3)
Inserted B (priority 1)
Inserted C (priority 2)
Inserted D (priority 1)
Inserted E (priority 4)
Priority queue: B(1) D(1) C(2) A(3) E(4)
Deleted B
Deleted D
Priority queue: C(2) A(3) E(4)
STL priority_queue: 50 30 20 10
```

**Practice question**

**Q24.** These items are inserted into a priority queue (smaller number = higher priority), in
this order: `P(2), Q(1), R(3), S(1), T(2)`. In what order will they be deleted?

---

## 25. Deques (double-ended queues)

**What it is**

A **deque** (say "deck") is a **double-ended queue**. In a deque, we can **insert and delete at
both ends** — at the front and at the rear.

```
 insert/delete                           insert/delete
   <------>   +----+----+----+----+   <------>
              |  5 | 10 | 20 | 30 |
              +----+----+----+----+
               front            rear
```

**Four operations**

| Operation | What it does |
|---|---|
| **insertFront** | Add an item at the front |
| **insertRear** | Add an item at the rear (like a normal queue) |
| **deleteFront** | Remove the item at the front (like a normal queue) |
| **deleteRear** | Remove the item at the rear |

**Two special types of deque**

| Type | Insertion | Deletion |
|---|---|---|
| **Input-restricted deque** | Only at **one** end (rear) | At **both** ends |
| **Output-restricted deque** | At **both** ends | Only at **one** end (front) |

**Note:** a deque is very flexible. If we use only one end, it works like a **stack**. If we insert
at one end and delete from the other, it works like a **queue**.

**Array (circular) representation**

We use a circular array, like the circular queue. The two new operations move **backward**:

| Action | Formula |
|---|---|
| insertFront: move front back | `front = (front - 1 + MAX) % MAX` |
| deleteRear: move rear back | `rear = (rear - 1 + MAX) % MAX` |

We add `MAX` before `%` so that index `0` goes back to `MAX - 1` (and never becomes `-1`).

```
After insertRear(20), insertRear(30), insertFront(10), insertFront(5)   (MAX = 5):

index:   0    1    2    3    4
       +----+----+----+----+----+
       | 20 | 30 |    |  5 | 10 |
       +----+----+----+----+----+
              ^         ^
            rear      front

Order from front to rear: 5 10 20 30
```

**Program**

```cpp
#include <iostream>
using namespace std;

#define MAX 5

int dq[MAX];
int front = -1, rear = -1;

bool isFull()  { return (rear + 1) % MAX == front; }
bool isEmpty() { return front == -1; }

// INSERT AT REAR (same as a normal circular queue)
void insertRear(int val) {
    if (isFull()) {
        cout << "Deque Overflow! Cannot insert " << val << endl;
        return;
    }
    if (isEmpty())
        front = rear = 0;
    else
        rear = (rear + 1) % MAX;
    dq[rear] = val;
    cout << "Inserted " << val << " at rear" << endl;
}

// INSERT AT FRONT (front moves one step BACK, with wrap-around)
void insertFront(int val) {
    if (isFull()) {
        cout << "Deque Overflow! Cannot insert " << val << endl;
        return;
    }
    if (isEmpty())
        front = rear = 0;
    else
        front = (front - 1 + MAX) % MAX;     // 0 goes back to MAX-1
    dq[front] = val;
    cout << "Inserted " << val << " at front" << endl;
}

// DELETE FROM FRONT (same as a normal circular queue)
int deleteFront() {
    if (isEmpty()) {
        cout << "Deque Underflow!" << endl;
        return -1;
    }
    int val = dq[front];
    if (front == rear)
        front = rear = -1;
    else
        front = (front + 1) % MAX;
    return val;
}

// DELETE FROM REAR (rear moves one step BACK, with wrap-around)
int deleteRear() {
    if (isEmpty()) {
        cout << "Deque Underflow!" << endl;
        return -1;
    }
    int val = dq[rear];
    if (front == rear)
        front = rear = -1;
    else
        rear = (rear - 1 + MAX) % MAX;
    return val;
}

void display() {
    if (isEmpty()) {
        cout << "Deque is empty" << endl;
        return;
    }
    cout << "Deque (front to rear): ";
    int i = front;
    while (true) {
        cout << dq[i] << " ";
        if (i == rear) break;
        i = (i + 1) % MAX;
    }
    cout << endl;
}

int main() {
    insertRear(20);
    insertRear(30);
    insertFront(10);
    insertFront(5);
    display();

    int x = deleteFront();
    cout << "Deleted from front: " << x << endl;
    x = deleteRear();
    cout << "Deleted from rear : " << x << endl;
    display();

    insertRear(40);
    insertRear(50);
    insertRear(60);
    insertRear(70);         // full
    display();
    return 0;
}
```

**Output**
```
Inserted 20 at rear
Inserted 30 at rear
Inserted 10 at front
Inserted 5 at front
Deque (front to rear): 5 10 20 30
Deleted from front: 5
Deleted from rear : 30
Deque (front to rear): 10 20
Inserted 40 at rear
Inserted 50 at rear
Inserted 60 at rear
Deque Overflow! Cannot insert 70
Deque (front to rear): 10 20 40 50 60
```

**Practice question**

**Q25.** What is the difference between an **input-restricted** deque and an **output-restricted**
deque? Which deque operations would you use to make a deque work like a **stack**?

---
---

# Answers

**Q16.**
```cpp
#include <iostream>
#include <cstring>
using namespace std;

#define MAX 50

char st[MAX];
int top = -1;

void push(char c) {
    if (top == MAX - 1) {
        cout << "Stack Overflow" << endl;
        return;
    }
    st[++top] = c;
}

char pop() {
    if (top == -1) {
        cout << "Stack Underflow" << endl;
        return '\0';
    }
    return st[top--];
}

int main() {
    char word[] = "STACK";
    int n = strlen(word);

    for (int i = 0; i < n; i++)      // push every letter
        push(word[i]);

    for (int i = 0; i < n; i++)      // pop them back: last letter comes out first
        word[i] = pop();

    cout << "Reversed: " << word << endl;
    return 0;
}
```

**Output**
```
Reversed: KCATS
```

The last letter pushed (`K`) is the first one popped, so the word comes out reversed. This is
LIFO in action.

**Q17.** Because pushing and popping at the **beginning** of a linked list is very fast — we only
change the `top` pointer and one `next` pointer. We do not need to walk through the list. If we
used the **end** of the list as the top, then every push and pop would need to walk through the
whole list to reach the last node (and for pop, the second-last node), which is slow.

**Q18.**

(a) `(A + B) * C - D`
```
Brackets: (((A + B) * C) - D)
Postfix:  AB+ -> AB+C* -> AB+C*D-        =  AB+C*D-
Prefix:   +AB -> *+ABC -> -*+ABCD        =  -*+ABCD
```

(b) `A * B + C / D`
```
Brackets: ((A * B) + (C / D))
Postfix:  AB* , CD/  ->  AB*CD/+          =  AB*CD/+
Prefix:   *AB , /CD  ->  +*AB/CD          =  +*AB/CD
```

**Q19.** Postfix `6 2 3 + - 3 8 2 / + *`

| Symbol | Action | Stack (bottom → top) |
|---|---|---|
| 6 | push | 6 |
| 2 | push | 6 2 |
| 3 | push | 6 2 3 |
| + | 2 + 3 = 5 | 6 5 |
| - | 6 - 5 = 1 | 1 |
| 3 | push | 1 3 |
| 8 | push | 1 3 8 |
| 2 | push | 1 3 8 2 |
| / | 8 / 2 = 4 | 1 3 4 |
| + | 3 + 4 = 7 | 1 7 |
| * | 1 * 7 = 7 | 7 |

Answer = **7**. (Infix form: `(6 - (2 + 3)) * (3 + 8 / 2)` = `1 * 7` = 7.)

**Q20.** Infix `A + ( B * C - ( D / E ^ F ) * G ) * H`

| Symbol | Stack | Postfix |
|---|---|---|
| A | | A |
| + | + | A |
| ( | + ( | A |
| B | + ( | AB |
| * | + ( * | AB |
| C | + ( * | ABC |
| - | + ( - | ABC* |
| ( | + ( - ( | ABC* |
| D | + ( - ( | ABC*D |
| / | + ( - ( / | ABC*D |
| E | + ( - ( / | ABC*DE |
| ^ | + ( - ( / ^ | ABC*DE |
| F | + ( - ( / ^ | ABC*DEF |
| ) | + ( - | ABC*DEF^/ |
| * | + ( - * | ABC*DEF^/ |
| G | + ( - * | ABC*DEF^/G |
| ) | + | ABC*DEF^/G*- |
| * | + * | ABC*DEF^/G*- |
| H | + * | ABC*DEF^/G*-H |
| (end) | | ABC*DEF^/G*-H*+ |

Postfix = **`ABC*DEF^/G*-H*+`**

**Q21.** In a simple (linear) array queue, `rear` only moves forward. Once `rear` reaches
`MAX - 1`, the program says "Overflow", even if some boxes at the start are free (because
`front` has moved forward after deletions). Those free boxes can never be used again. The fix is
a **circular queue**: when `rear` reaches the last index, it wraps around to index `0` using
`rear = (rear + 1) % MAX`, so the free boxes are used again.

**Q22.**
(a) Number of items = `(rear - front + MAX) % MAX + 1` = `(1 - 3 + 5) % 5 + 1` = `3 + 1` = **4**
items (at indexes 3, 4, 0, 1).
(b) Next index = `(rear + 1) % MAX` = `(1 + 1) % 5` = **2**.
(c) **Not full.** The queue is full only when `(rear + 1) % MAX == front`, and here
`2 != 3`. There is still one free box (index 2).

**Q23.** When the last item is deleted, `front` becomes `nullptr`. But `rear` would still point to
that **deleted** node. If we forget to set `rear = nullptr`, the next `enqueue()` will think the
queue is not empty and do `rear->next = newNode` on a node that no longer exists. This is a bug
(the program can crash), and `front` would stay `nullptr`, so the new item would be lost.

**Q24.** Smaller number goes first, and equal priorities keep their arrival order:

`Q(1), S(1), P(2), T(2), R(3)` → deletion order is **Q S P T R**.

**Q25.** An **input-restricted** deque allows **insertion at only one end** (rear), but deletion
at both ends. An **output-restricted** deque allows **deletion at only one end** (front), but
insertion at both ends.

To make a deque work like a **stack**, use the **same end** for both insert and delete, for
example `insertRear()` + `deleteRear()` (or `insertFront()` + `deleteFront()`). Then the last item
inserted is the first one deleted (LIFO).

---

[Back to top](#dsa--unit-3)
