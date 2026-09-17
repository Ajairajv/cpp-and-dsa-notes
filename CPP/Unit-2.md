# C++ — Unit 2

Simple notes for all Unit 2 topics.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**
```bash
g++ program.cpp -o program
./program
```

### Topics
13. [Pointers: void pointer and pointer arithmetic](#13-pointers-void-pointer-and-pointer-arithmetic)
14. [Pointer to pointer, dangling, wild and null pointer](#14-pointer-to-pointer-dangling-wild-and-null-pointer)
15. [Classes containing pointers, pointer to objects, this pointer](#15-classes-containing-pointers-pointer-to-objects-this-pointer)
16. [Array of objects and multidimensional arrays](#16-array-of-objects-and-multidimensional-arrays)
17. [The Standard C++ string class](#17-the-standard-c-string-class)
18. [More member functions and modifiers of string class](#18-more-member-functions-and-modifiers-of-string-class)
19. [Difference between pointer and reference variables](#19-difference-between-pointer-and-reference-variables)
20. [Pointer to a data member](#20-pointer-to-a-data-member)

---

## 13. Pointers: void pointer and pointer arithmetic

**What it is**

A **pointer** is a variable that does not store a normal value — it stores the **address** of
another variable.

| Symbol | Meaning |
|---|---|
| `&` | "address of" — gives the address of a variable |
| `*` | "value at" (dereference) — gives the value stored at an address |

```
int x = 100;
int *p = &x;

   x            p
+-----+      +--------+
| 100 |  <----|  addr  |
+-----+      +--------+
 addr(x)
```

`*p` means "go to the address `p` is holding, and give me the value there" — so `*p` is `100`.

**Void pointer**

A `void*` pointer can hold the address of **any** data type. But before using the value, it must be
**typecast** to the correct type — the compiler does not know what type of data is there.

**Pointer arithmetic**

If `p` is a pointer to `int`, then `p + 1` does **not** move by 1 byte. It moves by
`sizeof(int)` bytes — so it jumps to the **next int**, not the next byte. This is how a pointer can
walk through an array using `*(p + i)` instead of `a[i]`.

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 100;
    int *p = &x;

    cout << "Value of x       = " << x << endl;
    cout << "Address of x     = " << &x << endl;
    cout << "p (address held) = " << p << endl;
    cout << "*p (value at p)  = " << *p << endl;
    cout << endl;

    // VOID POINTER - can hold address of any type, but must be typecast to use
    void *vp;
    int a = 50;
    vp = &a;
    cout << "Void pointer holds address of a = " << vp << endl;
    cout << "Value using typecast            = " << *(int*)vp << endl;
    cout << endl;

    // POINTER ARITHMETIC - moves by sizeof(type), not by 1 byte
    int arr[5] = {10, 20, 30, 40, 50};
    int *ptr = arr;                   // array name is the address of the first element

    cout << "Array using pointer arithmetic: ";
    for (int i = 0; i < 5; i++)
        cout << *(ptr + i) << " ";
    cout << endl;

    cout << "ptr       = " << ptr << endl;
    cout << "ptr + 1   = " << ptr + 1 << " (moved by " << sizeof(int) << " bytes, not 1 byte)" << endl;
    return 0;
}
```

**Output** (the exact addresses will be different on your computer, that is normal)
```
Value of x       = 100
Address of x     = 0x61fefc
p (address held) = 0x61fefc
*p (value at p)  = 100

Void pointer holds address of a = 0x61fef8
Value using typecast            = 50

Array using pointer arithmetic: 10 20 30 40 50
ptr       = 0x61fee4
ptr + 1   = 0x61fee8 (moved by 4 bytes, not 1 byte)
```

**Practice question**

**Q13.** What is a `void` pointer? Why must it be typecast before using the value it points to?

---

## 14. Pointer to pointer, dangling, wild and null pointer

**What it is**

**Pointer to a pointer** — a pointer that stores the address of another pointer, not of a normal
variable. Declared with two stars: `int **pp;`

```
   x           p            pp
+-----+     +------+     +------+
| 10  | <-- | addr |<--  | addr |
+-----+     +------+     +------+
```
`*p` gives the value stored in `p` (an address). `**pp` follows two arrows and gives `10`.

**Three problem pointers**

| Type | Meaning |
|---|---|
| **Null pointer** | Points to nothing. In modern C++, assigned using `nullptr`. Safe — you can check `if (p == nullptr)` before using it. |
| **Wild pointer** | Declared but **never given an address**. It holds a random/garbage value. Using it is dangerous. |
| **Dangling pointer** | Was pointing to valid memory, but that memory was already freed with `delete`. Using it after that is dangerous. |

**Good practice:** after `delete p;`, immediately write `p = nullptr;` — this turns a dangerous
dangling pointer into a safe null pointer that you can check before use.

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    int *p = &x;
    int **pp = &p;             // pointer to pointer

    cout << "x    = " << x << endl;
    cout << "*p   = " << *p << endl;
    cout << "**pp = " << **pp << endl;
    cout << endl;

    // NULL POINTER
    int *np = nullptr;          // points to nothing
    if (np == nullptr)
        cout << "np is a null pointer, it points to nothing" << endl;
    cout << endl;

    // DANGLING POINTER
    int *dp = new int;          // memory created
    *dp = 25;
    cout << "Before delete, *dp = " << *dp << endl;
    delete dp;                  // memory freed
    dp = nullptr;                // GOOD PRACTICE: set to nullptr right after delete
    cout << "After delete, dp is set to nullptr (this avoids a dangling pointer)" << endl;

    // WILD POINTER (shown only as a comment - using it would be undefined behaviour)
    // int *wp;       // not initialized -> wild pointer, holds a garbage address
    // cout << *wp;   // DANGEROUS: never do this
    cout << "A wild pointer is declared but never given an address (see comment in code)" << endl;
    return 0;
}
```

**Output**
```
x    = 10
*p   = 10
**pp = 10

np is a null pointer, it points to nothing

Before delete, *dp = 25
After delete, dp is set to nullptr (this avoids a dangling pointer)
A wild pointer is declared but never given an address (see comment in code)
```

**Practice question**

**Q14.** Give one difference each between: (a) a null pointer and a wild pointer, (b) a wild pointer
and a dangling pointer.

---

## 15. Classes containing pointers, pointer to objects, this pointer

**What it is**

**A class can contain a pointer as a data member.** This is very common — for example, a `Node`
class used in a linked list has a pointer to the *next* `Node`.

**Pointer to an object**
- With an object, use a **dot**: `obj.show();`
- With a **pointer** to an object, use an **arrow**: `ptr->show();`

**The `this` pointer**

Inside every member function, C++ secretly gives you a pointer called `this`, which points to
**the object that called the function**. It is mostly used when a parameter has the **same name**
as a data member — `this->x` clearly means the data member, not the parameter.

**Program**

```cpp
#include <iostream>
using namespace std;

class Point {
    int x, y;
public:
    void setX(int x) {          // parameter has same name as data member
        this->x = x;            // this-> tells C++ we mean the data member
    }
    void setY(int y) {
        this->y = y;
    }
    void show() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};

// A class that CONTAINS A POINTER as a data member
class Node {
public:
    int data;
    Node *next;                 // pointer to another object of the same class
};

int main() {
    Point p1;
    p1.setX(3);
    p1.setY(4);

    Point *ptr = &p1;           // pointer to an object
    cout << "Using object    : ";
    p1.show();
    cout << "Using pointer   : ";
    ptr->show();                // -> is used through a pointer
    cout << endl;

    // Class containing a pointer, linking two Node objects
    Node n1, n2;
    n1.data = 10;
    n2.data = 20;
    n1.next = &n2;               // n1 now points to n2
    n2.next = nullptr;

    cout << "n1.data = " << n1.data << endl;
    cout << "n1.next->data = " << n1.next->data << endl;
    return 0;
}
```

**Output**
```
Using object    : (3, 4)
Using pointer   : (3, 4)

n1.data = 10
n1.next->data = 20
```

**Practice question**

**Q15.** What is the `this` pointer? Why is it needed in the `setX()` function above?

---

## 16. Array of objects and multidimensional arrays

**What it is**

**Array of objects** — just like `int a[5]`, we can make an array of a class type:
`Student s[5];` creates 5 separate `Student` objects, all handled with one name and an index.

**Multidimensional array** — an array with more than one index, like a table with rows and
columns: `int a[2][3];` It can be declared:
- **Inside `main()`** — a normal local 2-D array.
- **Inside a class**, as a data member — every object of that class then has its own copy of the
  2-D array.

**Program**

```cpp
#include <iostream>
using namespace std;

class Student {
    int roll;
    float marks;
public:
    void setData(int r, float m) { roll = r; marks = m; }
    void show() { cout << "Roll " << roll << " -> Marks " << marks << endl; }
};

class Matrix {                        // 2-D array INSIDE a class
    int m[2][2];
public:
    void setData() {
        int val = 1;
        for (int i = 0; i < 2; i++)
            for (int j = 0; j < 2; j++)
                m[i][j] = val++;
    }
    void show() {
        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < 2; j++)
                cout << m[i][j] << " ";
            cout << endl;
        }
    }
};

int main() {
    // ARRAY OF OBJECTS
    Student s[3];
    s[0].setData(1, 78.5);
    s[1].setData(2, 91.0);
    s[2].setData(3, 65.5);

    cout << "Array of objects:" << endl;
    for (int i = 0; i < 3; i++)
        s[i].show();
    cout << endl;

    // MULTIDIMENSIONAL ARRAY INSIDE main()
    int a[2][3] = {{1, 2, 3}, {4, 5, 6}};
    cout << "2-D array inside main():" << endl;
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j < 3; j++)
            cout << a[i][j] << " ";
        cout << endl;
    }
    cout << endl;

    // MULTIDIMENSIONAL ARRAY INSIDE a class
    Matrix mat;
    mat.setData();
    cout << "2-D array inside a class:" << endl;
    mat.show();
    return 0;
}
```

**Output**
```
Array of objects:
Roll 1 -> Marks 78.5
Roll 2 -> Marks 91
Roll 3 -> Marks 65.5

2-D array inside main():
1 2 3
4 5 6

2-D array inside a class:
1 2
3 4
```

**Practice question**

**Q16.** Write a class `Book` with `title` and `price`. Create an array of 3 `Book` objects, set
data for all of them, and print the most expensive book.

---

## 17. The Standard C++ string class

**What it is**

The C++ `string` class (from header `<string>`) is much easier to use than a plain `char[]`
array — it grows automatically, and has ready-made functions for common jobs.

**Defining and assigning a string object** — any of these ways work:

```cpp
string s1 = "Hello";      // way 1
string s2("World");       // way 2
string s3;
s3 = "C++ Strings";       // way 3, assign later
```

**Some common member functions**

| Function | Work |
|---|---|
| `s.length()` or `s.size()` | number of characters |
| `s.substr(pos, len)` | part of the string, starting at `pos`, `len` characters long |
| `s.find("text")` | position where "text" starts (returns `string::npos` if not found) |
| `s + "!"` | joins ("concatenates") two strings using `+` |

**Program**

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1 = "Hello";           // defining and assigning, way 1
    string s2("World");            // way 2
    string s3;
    s3 = "C++ Strings";            // way 3, assign later

    cout << "s1 = " << s1 << endl;
    cout << "s2 = " << s2 << endl;
    cout << "s3 = " << s3 << endl;
    cout << endl;

    // MEMBER FUNCTIONS
    string s = "Data Structures";
    cout << "s              = " << s << endl;
    cout << "s.length()     = " << s.length() << endl;
    cout << "s.substr(0,4)  = " << s.substr(0, 4) << endl;
    cout << "s.find(STR)    = " << s.find("Str") << endl;
    cout << "s + BANG       = " << s + "!" << endl;
    return 0;
}
```

**Output**
```
s1 = Hello
s2 = World
s3 = C++ Strings

s              = Data Structures
s.length()     = 15
s.substr(0,4)  = Data
s.find(STR)    = 5
s + BANG       = Data Structures!
```

**Practice question**

**Q17.** Take a full name as a `string` using `getline()`. Print its length and the first 4
characters using `substr()`.

---

## 18. More member functions and modifiers of string class

**What it is**

More functions that **change (modify)** a `string`:

| Function | Work |
|---|---|
| `s.append(text)` | adds `text` at the end |
| `s.insert(pos, text)` | inserts `text` at position `pos` |
| `s.erase(pos, n)` | removes `n` characters starting at `pos` |

There is no single built-in function to make a string fully uppercase or to reverse it —
these are done **character by character**, using the index `[]`, just like an array:
- `toupper(ch)` (from `<cctype>`) converts one character to uppercase.
- Swapping characters from both ends towards the middle reverses the string.

**Program**

```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string s = "Hello";

    s.append(" World");                 // add text at the end
    cout << "After append : " << s << endl;

    s.insert(5, ",");                   // insert "," at position 5
    cout << "After insert  : " << s << endl;

    s.erase(5, 1);                      // remove 1 character from position 5
    cout << "After erase   : " << s << endl;

    // MODIFIER: convert to uppercase (character by character)
    string upper = s;
    for (int i = 0; i < (int)upper.length(); i++)
        upper[i] = toupper(upper[i]);
    cout << "Uppercase     : " << upper << endl;

    // MODIFIER: reverse the string
    string rev = s;
    int n = rev.length();
    for (int i = 0; i < n / 2; i++) {
        char temp = rev[i];
        rev[i] = rev[n - 1 - i];
        rev[n - 1 - i] = temp;
    }
    cout << "Reversed      : " << rev << endl;
    return 0;
}
```

**Output**
```
After append : Hello World
After insert  : Hello, World
After erase   : Hello World
Uppercase     : HELLO WORLD
Reversed      : dlroW olleH
```

**Practice question**

**Q18.** Take a string from the user. Count how many times the letter `'a'` (small or capital)
appears in it.

---

## 19. Difference between pointer and reference variables

**What it is**

A **reference variable** is another name (an alias) for an existing variable. It is declared with
`&` at the time of declaration: `int &ref = x;` — from then on, `ref` and `x` are the same memory
location; changing one changes the other.

**Main differences**

| Pointer | Reference |
|---|---|
| Stores an **address** | Is another **name** for a variable |
| Can be declared without a value, and given one later | **Must** be initialized at the time of declaration |
| Can be made to point to a different variable later | Once set, always refers to the **same** variable |
| Can be `nullptr` | Can never be null |
| Needs `*` to get the value | Used directly, just like a normal variable |

A common use of references is passing parameters to a function, so the function can change the
caller's variables directly — without needing pointers and `*`/`&` everywhere.

**Program**

```cpp
#include <iostream>
using namespace std;

void swapPointer(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}

void swapReference(int &a, int &b) {
    int t = a;
    a = b;
    b = t;
}

int main() {
    int x = 5, y = 10;
    cout << "Before swapPointer: x=" << x << " y=" << y << endl;
    swapPointer(&x, &y);                 // must pass addresses
    cout << "After swapPointer : x=" << x << " y=" << y << endl;
    cout << endl;

    int p = 5, q = 10;
    cout << "Before swapReference: p=" << p << " q=" << q << endl;
    swapReference(p, q);                 // pass variables directly
    cout << "After swapReference : p=" << p << " q=" << q << endl;
    cout << endl;

    int a = 100;
    int &ref = a;                        // reference must be initialized here
    ref = 200;                           // changing ref changes a too
    cout << "a = " << a << " (changed through its reference)" << endl;
    return 0;
}
```

**Output**
```
Before swapPointer: x=5 y=10
After swapPointer : x=10 y=5

Before swapReference: p=5 q=10
After swapReference : p=10 q=5

a = 200 (changed through its reference)
```

**Practice question**

**Q19.** Write any three differences between a pointer and a reference variable.

---

## 20. Pointer to a data member

**What it is**

A **pointer to a data member** is different from a normal pointer. A normal pointer stores a
fixed address. But a class's data member exists at a **different address in every object** — so
a pointer to a data member does not store an address by itself. It only stores **which member**
you mean; you must combine it with an actual object to get a real value.

**Declaring and using it**

```cpp
class Item {
public:
    int price;
};

int Item::*ptr = &Item::price;   // declare: Type ClassName::*ptr
```

To use it with an object, write `object.*ptr` (through an object) or `objectPointer->*ptr`
(through a pointer to an object).

**Program**

```cpp
#include <iostream>
using namespace std;

class Item {
public:
    int price;
};

int main() {
    int Item::*ptr = &Item::price;    // pointer to the data member "price"

    Item i1, i2;
    i1.price = 100;
    i2.price = 250;

    cout << "i1.price using pointer to member = " << i1.*ptr << endl;
    cout << "i2.price using pointer to member = " << i2.*ptr << endl;

    i1.*ptr = 500;                    // change price of i1 using the pointer
    cout << "i1.price after change             = " << i1.price << endl;
    return 0;
}
```

**Output**
```
i1.price using pointer to member = 100
i2.price using pointer to member = 250
i1.price after change             = 500
```

**Practice question**

**Q20.** Why does a pointer to a data member need to be combined with an object before it can give
a real value? Explain in 2–3 lines.

---
---

# Answers

**Q13.** A `void` pointer is a pointer that can hold the **address of any data type** — `int`,
`float`, `char`, or even an object. It must be **typecast** before the value is used, because a
`void*` does not carry any information about the type of data stored at that address, so the
compiler does not know how many bytes to read or how to interpret them — typecasting
(`*(int*)vp`) tells it exactly what type to treat that memory as.

**Q14.**
(a) A **null pointer** deliberately points to nothing (`nullptr`) and is **safe** to check before
use with `if (p == nullptr)`. A **wild pointer** was never given any address at all — it holds
whatever garbage value happened to be in memory, and using it is dangerous.
(b) A **wild pointer** was *never valid* in the first place (never initialized). A **dangling
pointer** *was* valid once, pointing to real memory, but that memory has since been freed with
`delete`, so continuing to use it is dangerous.

**Q15.** The `this` pointer is a hidden pointer available inside every member function, and it
points to the object that called that function. It is needed in `setX(int x)` because the
parameter is also named `x`, same as the data member — writing plain `x = x;` would just assign
the parameter to itself and never change the data member. `this->x = x;` makes it clear that the
left side is the data member and the right side is the parameter.

**Q16.**
```cpp
#include <iostream>
using namespace std;

class Book {
public:
    string title;
    float price;
    void setData(string t, float p) { title = t; price = p; }
};

int main() {
    Book b[3];
    b[0].setData("C++ Basics", 350.0);
    b[1].setData("DSA Guide", 550.0);
    b[2].setData("OOP Concepts", 420.0);

    int maxIndex = 0;
    for (int i = 1; i < 3; i++) {
        if (b[i].price > b[maxIndex].price)
            maxIndex = i;
    }

    cout << "Most expensive: " << b[maxIndex].title << " (Rs " << b[maxIndex].price << ")" << endl;
    return 0;
}
```
Output: `Most expensive: DSA Guide (Rs 550)`

**Q17.**
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter full name: ";
    getline(cin, name);

    cout << "Length = " << name.length() << endl;
    cout << "First 4 characters = " << name.substr(0, 4) << endl;
    return 0;
}
```

**Q18.**
```cpp
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

int main() {
    string s;
    cout << "Enter a string: ";
    getline(cin, s);

    int count = 0;
    for (int i = 0; i < (int)s.length(); i++) {
        if (tolower(s[i]) == 'a')
            count++;
    }
    cout << "Number of 'a' = " << count << endl;
    return 0;
}
```

**Q19.** Any three differences:
1. A pointer stores an **address**; a reference is just **another name** for the same variable.
2. A pointer can be declared without a value and given one later; a reference **must** be
   initialized at the time it is declared.
3. A pointer can later be made to point to a **different** variable; a reference always refers to
   the **same** variable for its whole life.
4. A pointer can be `nullptr`; a reference can **never** be null — it must always refer to a real
   variable.

(Any three of these are enough.)

**Q20.** A data member does not have one fixed address — the same member (say, `price`) exists at
a **different memory location in every object** of the class (`i1.price` and `i2.price` are two
separate memory spots). A pointer to a data member only stores information about **which member**
inside the class layout is meant, not an actual address. So it must be written together with a
real object (`i1.*ptr`) so C++ can combine "which member" with "which object" to find the actual
memory location and give a real value.

---

[Back to top](#c--unit-2)
