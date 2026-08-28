# C++ — Unit 1

Simple notes for all Unit 1 topics.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**
```bash
g++ program.cpp -o program
./program
```

### Topics
1. [Procedural vs Object Oriented Programming](#1-procedural-vs-object-oriented-programming)
2. [Concepts of OOP](#2-concepts-of-oop)
3. [Reading and writing data (cin and cout)](#3-reading-and-writing-data-cin-and-cout)
4. [Classes, objects and members](#4-classes-objects-and-members)
5. [Inline and non-inline member functions](#5-inline-and-non-inline-member-functions)
6. [Static data members and static member functions](#6-static-data-members-and-static-member-functions)
7. [Structure, Union, Enumeration and Class](#7-structure-union-enumeration-and-class)
8. [Default arguments](#8-default-arguments)
9. [Inline functions](#9-inline-functions)
10. [Manipulator functions](#10-manipulator-functions)
11. [Function overloading and scope rules](#11-function-overloading-and-scope-rules)
12. [Friend function and friend class](#12-friend-function-and-friend-class)

---

## 1. Procedural vs Object Oriented Programming

**What it is**

In **procedural programming**, the program is a set of functions. The data is kept separately, and
any function can change any data. C is a procedural language.

In **object oriented programming (OOP)**, data and the functions that work on that data are kept
together in one unit called a **class**. The data is hidden, so outside code cannot spoil it.
C++ supports OOP.

**Main differences**

| Procedural | Object Oriented |
|---|---|
| Basic unit is the **function** | Basic unit is the **object** |
| Data is kept outside the functions | Data is kept inside the object |
| Any function can change the data | Only the object's own functions can change it |
| No data hiding | Data hiding using `private` |
| Top-down approach | Bottom-up approach |
| Example: C | Example: C++, Java |

**Program**

```cpp
#include <iostream>
using namespace std;

// OOP style: data and functions together, data is private
class Student {
private:
    int marks;              // hidden from outside

public:
    void setMarks(int m) {
        if (m < 0 || m > 100)       // rule is checked here
            marks = 0;
        else
            marks = m;
    }
    void show() {
        cout << "Marks = " << marks << endl;
    }
};

int main() {
    Student s;
    s.setMarks(85);
    s.show();

    s.setMarks(500);        // wrong value, so it becomes 0
    s.show();

    // s.marks = 500;       // ERROR: marks is private
    return 0;
}
```

**Output**
```
Marks = 85
Marks = 0
```

**Practice question**

**Q1.** Write four differences between procedural and object oriented programming.

---

## 2. Concepts of OOP

**What it is**

OOP has four main ideas. These four are called the **pillars of OOP**.

| Concept | Meaning | Simple example |
|---|---|---|
| **Encapsulation** | Keeping data and functions together in one class, and making the data `private` | Marks are private, only `setMarks()` can change them |
| **Abstraction** | Showing only what is needed, hiding how it works inside | You press a TV remote button, you don't know the circuit inside |
| **Inheritance** | A new class takes the properties of an old class | `Car` takes properties of `Vehicle` |
| **Polymorphism** | Same name doing different work | `add(2,3)` and `add(2.5,3.5)` |

Other terms:
- **Class** — a blueprint or design. Example: a form.
- **Object** — a real item made from the class. Example: a filled form.

**Types of OOP languages**
- **Pure OOP** — everything is an object. Example: Smalltalk.
- **Hybrid OOP** — supports OOP but also normal functions. Example: **C++**, Java.

**Program**

```cpp
#include <iostream>
using namespace std;

// INHERITANCE: Car gets everything from Vehicle
class Vehicle {
public:
    void start() {
        cout << "Vehicle started" << endl;
    }
};

class Car : public Vehicle {     // Car is a Vehicle
public:
    void wheels() {
        cout << "Car has 4 wheels" << endl;
    }
};

// POLYMORPHISM: same name, different work
void add(int a, int b) {
    cout << "Sum of integers = " << a + b << endl;
}
void add(double a, double b) {
    cout << "Sum of decimals = " << a + b << endl;
}

int main() {
    Car c;
    c.start();          // taken from Vehicle
    c.wheels();         // its own

    add(2, 3);          // calls the int version
    add(2.5, 3.5);      // calls the double version
    return 0;
}
```

**Output**
```
Vehicle started
Car has 4 wheels
Sum of integers = 5
Sum of decimals = 6
```

**Practice question**

**Q2.** Name the four pillars of OOP and write one line about each.

---

## 3. Reading and writing data (cin and cout)

**What it is**

- `cout` is used to **print** on the screen. It uses `<<`.
- `cin` is used to **read** from the keyboard. It uses `>>`.
- Both are in the header file `<iostream>`.

**Important points**
- `cin >> name;` reads only **one word**. It stops at a space.
- To read a full line with spaces, use `getline(cin, name);`
- `endl` moves to the next line. `"\n"` also does the same.

| Object | Use |
|---|---|
| `cin` | input from keyboard |
| `cout` | output to screen |
| `cerr` | error messages |

**Program**

```cpp
#include <iostream>
using namespace std;

int main() {
    int roll;
    float marks;
    string name;

    cout << "Enter roll number: ";
    cin >> roll;

    cout << "Enter marks: ";
    cin >> marks;

    cin.ignore();                   // needed before getline, clears the Enter key

    cout << "Enter full name: ";
    getline(cin, name);             // reads the full line with spaces

    cout << endl;
    cout << "Roll  = " << roll << endl;
    cout << "Name  = " << name << endl;
    cout << "Marks = " << marks << endl;
    return 0;
}
```

**Output** (whatever the user types is shown in the input lines)
```
Enter roll number: 21
Enter marks: 87.5
Enter full name: Aarav Kumar

Roll  = 21
Name  = Aarav Kumar
Marks = 87.5
```

**Practice question**

**Q3.** Write a program to read the name, roll number and three subject marks of a student, then
print the total and the average.

---

## 4. Classes, objects and members

**What it is**

- A **class** is a design or blueprint. Writing a class does not take any memory.
- An **object** is made from the class. Memory is given when an object is made.
- Things inside a class are called **members**: data members and member functions.

**Access specifiers**

| Specifier | Who can use it |
|---|---|
| `private` | only the functions inside the same class |
| `public` | anyone, from anywhere |

In a `class`, members are **private by default**.

**How to use members**
- With an object → use a dot: `s.show();`
- With a pointer → use an arrow: `p->show();`

**Program**

```cpp
#include <iostream>
using namespace std;

class Student {
private:                       // hidden data
    int roll;
    string name;
    float marks;

public:                        // functions anyone can call
    void setData(int r, string n, float m) {
        roll  = r;
        name  = n;
        marks = m;
    }
    void display() {
        cout << roll << "  " << name << "  " << marks << endl;
    }
};                             // this semicolon is compulsory

int main() {
    Student s1, s2;            // two objects, memory is given here

    s1.setData(21, "Aarav", 87.5);
    s2.setData(22, "Diya", 91.0);

    s1.display();              // dot is used with an object
    s2.display();

    Student *p = &s1;          // pointer to an object
    p->display();              // arrow is used with a pointer
    return 0;
}
```

**Output**
```
21  Aarav  87.5
22  Diya  91
21  Aarav  87.5
```

**Practice question**

**Q4.** Write a class `Rectangle` with private `length` and `breadth`. Add a function to set the
values and a function to print the area. Create one object and show the area.

---

## 5. Inline and non-inline member functions

**What it is**

- If a member function is written **inside** the class, it is an **inline** function.
  The compiler copies the code where it is called, so there is no function call.
  Good for **small** functions.
- If a member function is written **outside** the class, it is a **non-inline** function.
  We use `::` (scope resolution operator) to tell which class it belongs to.

**Difference**

| Inline member function | Non-inline member function |
|---|---|
| Written inside the class | Written outside the class using `::` |
| No function call, code is copied | Normal function call takes place |
| Program size increases | Program size stays same |
| Used for small functions | Used for big functions |

**Program**

```cpp
#include <iostream>
using namespace std;

class Box {
private:
    int length, breadth;

public:
    // INLINE: written inside the class
    void setData(int l, int b) {
        length = l;
        breadth = b;
    }
    int area() { return length * breadth; }

    // Only declared here, written outside
    void display();
};

// NON-INLINE: written outside using Box::
void Box::display() {
    cout << "Length  = " << length << endl;
    cout << "Breadth = " << breadth << endl;
    cout << "Area    = " << area() << endl;
}

int main() {
    Box b;
    b.setData(5, 4);
    b.display();
    return 0;
}
```

**Output**
```
Length  = 5
Breadth = 4
Area    = 20
```

**Practice question**

**Q5.** Write a class `Circle` with radius. Write `area()` inside the class and `display()` outside
the class using `::`.

---

## 6. Static data members and static member functions

**What it is**

**Static data member**
- Normally every object has its own copy of the data.
- A **static** data member has only **one copy** for the whole class. All objects share it.
- It must be **defined outside the class**, like this: `int Student::count = 0;`
  If you forget this line, you get an error.

**Static member function**
- It belongs to the class, not to any object.
- It can use **only static data members**.
- It is called using the class name: `Student::showCount();`

**Program**

```cpp
#include <iostream>
using namespace std;

class Student {
private:
    int roll;
    static int count;           // only ONE copy, shared by all objects

public:
    void setRoll(int r) {
        roll = r;
        count++;                // every new student increases the count
    }
    void show() {
        cout << "Roll = " << roll << endl;
    }
    static void showCount() {   // static function
        cout << "Total students = " << count << endl;
    }
};

int Student::count = 0;         // COMPULSORY: defined outside the class

int main() {
    Student s1, s2, s3;

    s1.setRoll(21);
    s2.setRoll(22);
    s3.setRoll(23);

    s1.show();
    s2.show();
    s3.show();

    Student::showCount();       // called using class name, no object needed
    return 0;
}
```

**Output**
```
Roll = 21
Roll = 22
Roll = 23
Total students = 3
```

**Practice question**

**Q6.** Why must a static data member be defined outside the class? Also write why a static member
function cannot use a normal (non-static) data member.

---

## 7. Structure, Union, Enumeration and Class

**What it is**

| | Meaning |
|---|---|
| **Structure** | Groups different variables together. Members are **public** by default. |
| **Class** | Same as structure, but members are **private** by default. |
| **Union** | All members **share the same memory**. Only one member can be used at a time. |
| **Enumeration** | Gives names to numbers, so the program is easy to read. |

**Main points to remember**
- Structure and class are almost the same in C++. **The only difference is the default access.**
- In a union, the size is equal to the **biggest member**, not the total.
- In an enum, if you don't give values, they start from 0.

**Program**

```cpp
#include <iostream>
using namespace std;

struct Point {          // public by default
    int x, y;
};

class Marks {           // private by default
    int value;
public:
    void set(int v) { value = v; }
    void show() { cout << "Marks = " << value << endl; }
};

union Data {            // all members share the same memory
    int i;
    float f;
};

enum Day { MON, TUE, WED };     // MON=0, TUE=1, WED=2

int main() {
    Point p;
    p.x = 3;  p.y = 4;                  // allowed, struct is public
    cout << "Point = " << p.x << "," << p.y << endl;

    Marks m;
    // m.value = 90;                    // ERROR: private
    m.set(90);
    m.show();

    Data d;
    d.i = 65;
    cout << "d.i = " << d.i << endl;
    d.f = 3.5;                          // this ERASES the value of i
    cout << "after d.f = 3.5, d.i is now spoiled" << endl;

    cout << "Size of struct = " << sizeof(Point) << " bytes" << endl;
    cout << "Size of union  = " << sizeof(Data) << " bytes" << endl;

    Day today = TUE;
    cout << "TUE = " << today << endl;
    return 0;
}
```

**Output**
```
Point = 3,4
Marks = 90
d.i = 65
after d.f = 3.5, d.i is now spoiled
Size of struct = 8 bytes
Size of union  = 4 bytes
TUE = 1
```

**Practice question**

**Q7.** Write the difference between a structure and a union in four points.

---

## 8. Default arguments

**What it is**

A **default argument** is a value already given in the function. If we do not pass that value while
calling, the default value is used automatically.

**Rules**
1. Default values are given from **right to left**.
   Correct: `void f(int a, int b = 2, int c = 3);`
   Wrong: `void f(int a = 1, int b, int c);`
2. We cannot skip a middle value. `f(10, , 3)` is **not allowed**.

**Program**

```cpp
#include <iostream>
using namespace std;

// rate and years have default values
float simpleInterest(float p, float rate = 5.0, int years = 1) {
    return (p * rate * years) / 100;
}

int main() {
    cout << "SI(1000)            = " << simpleInterest(1000) << endl;
    cout << "SI(1000, 8)         = " << simpleInterest(1000, 8) << endl;
    cout << "SI(1000, 8, 2)      = " << simpleInterest(1000, 8, 2) << endl;
    return 0;
}
```

**Output**
```
SI(1000)            = 50
SI(1000, 8)         = 80
SI(1000, 8, 2)      = 160
```

**Practice question**

**Q8.** Which of these are correct and which are wrong? Give the reason.
(a) `void f(int a, int b = 2);`
(b) `void f(int a = 1, int b);`
(c) `void f(int a = 1, int b = 2);`

---

## 9. Inline functions

**What it is**

An **inline function** is a normal function written with the keyword `inline`. The compiler copies
its code at the place where it is called, instead of making a function call. This saves time.

**Points to remember**
- `inline` is only a **request**. The compiler may refuse it.
- The compiler usually refuses if the function is **big**, has a **loop**, or is **recursive**.
- Use it only for **small** functions.

**Advantage:** saves function call time.
**Disadvantage:** program size increases, because the code is copied everywhere.

**Program**

```cpp
#include <iostream>
using namespace std;

inline int square(int x) {
    return x * x;
}

inline int maximum(int a, int b) {
    return (a > b) ? a : b;
}

int main() {
    cout << "square(5)      = " << square(5) << endl;
    cout << "maximum(10, 7) = " << maximum(10, 7) << endl;
    return 0;
}
```

**Output**
```
square(5)      = 25
maximum(10, 7) = 10
```

**Practice question**

**Q9.** Write any three situations in which the compiler does not make a function inline.

---

## 10. Manipulator functions

**What it is**

**Manipulators** are used with `cout` to change how the output looks. They are used to print neat,
straight tables.

| Manipulator | Work | Header file |
|---|---|---|
| `endl` | new line | `<iostream>` |
| `setw(n)` | gives `n` spaces for the **next value only** | `<iomanip>` |
| `setprecision(n)` | number of digits after the decimal point | `<iomanip>` |
| `fixed` | shows a fixed number of decimal places | `<iostream>` |
| `setfill(c)` | fills the empty space with character `c` | `<iomanip>` |
| `left` / `right` | aligns to the left or right | `<iostream>` |

**Very important:** `setw()` works for **only the next value**. You must write it again for each
value.

For `setw`, `setprecision` and `setfill` you must write `#include <iomanip>`.

**Program**

```cpp
#include <iostream>
#include <iomanip>              // needed for setw and setprecision
using namespace std;

int main() {
    cout << left << setw(12) << "Item"
         << right << setw(8) << "Qty"
         << right << setw(12) << "Price" << endl;

    cout << fixed << setprecision(2);       // 2 digits after the decimal point

    cout << left << setw(12) << "Notebook"
         << right << setw(8) << 12
         << right << setw(12) << 546.00 << endl;

    cout << left << setw(12) << "Pen"
         << right << setw(8) << 40
         << right << setw(12) << 510.00 << endl;
    return 0;
}
```

**Output**
```
Item             Qty       Price
Notebook          12      546.00
Pen               40      510.00
```

**Practice question**

**Q10.** Print the multiplication table of 5 (from 5×1 to 5×10) using `setw(4)` so that all the
answers come in a straight line.

---

## 11. Function overloading and scope rules

**What it is**

**Function overloading** means writing **two or more functions with the same name**, but with
**different parameters**. The compiler decides which one to call.

The functions must differ in:
- the **number** of parameters, or
- the **type** of parameters.

**They cannot differ only in return type.** This is wrong:
```cpp
int add(int a, int b);
float add(int a, int b);     // ERROR
```

**Scope rules**

Scope means where a variable can be used.
- **Local variable** — declared inside a function, used only there.
- **Global variable** — declared outside all functions, used anywhere.
- If both have the same name, the **local one is used**.
- To use the global one, write `::` before it, like `::x`.

**Program**

```cpp
#include <iostream>
using namespace std;

// FUNCTION OVERLOADING: same name, different parameters
int add(int a, int b) {
    return a + b;
}
int add(int a, int b, int c) {          // different number
    return a + b + c;
}
double add(double a, double b) {        // different type
    return a + b;
}

int x = 100;                            // global variable

int main() {
    cout << "add(2, 3)      = " << add(2, 3) << endl;
    cout << "add(2, 3, 4)   = " << add(2, 3, 4) << endl;
    cout << "add(2.5, 3.5)  = " << add(2.5, 3.5) << endl;

    int x = 50;                         // local variable, same name

    cout << "local  x = " << x << endl;
    cout << "global x = " << ::x << endl;    // :: gives the global one
    return 0;
}
```

**Output**
```
add(2, 3)      = 5
add(2, 3, 4)   = 9
add(2.5, 3.5)  = 6
local  x = 50
global x = 100
```

**Practice question**

**Q11.** Write a program with three overloaded functions named `area()` — one for a square (one
value), one for a rectangle (two values), and one for a circle (one decimal value).

---

## 12. Friend function and friend class

**What it is**

**Friend function**
- A friend function is **not a member** of the class.
- But the class allows it to use its **private** data.
- It is declared inside the class using the keyword `friend`.
- It is **called normally**, like `show(obj)` — not `obj.show()`.

**Friend class**
- If class B is made a friend of class A, then **all functions of B** can use the private data of A.

**Points to remember**
- Friendship is **not both ways**. If A says B is a friend, B can see A, but A cannot see B.
- Friendship is **not inherited**.
- A friend function can use the private data of **two different classes**.

**Program**

```cpp
#include <iostream>
using namespace std;

class Chemistry;                  // told the compiler this class exists

class Physics {
private:
    int marks;
public:
    void setMarks(int m) { marks = m; }
    friend void total(Physics, Chemistry);      // friend function
};

class Chemistry {
private:
    int marks;
public:
    void setMarks(int m) { marks = m; }
    friend void total(Physics, Chemistry);      // friend of this class also
};

// Not a member of any class, so no Physics:: is written
void total(Physics p, Chemistry c) {
    cout << "Physics   = " << p.marks << endl;      // using private data
    cout << "Chemistry = " << c.marks << endl;
    cout << "Total     = " << p.marks + c.marks << endl;
}

int main() {
    Physics p;
    Chemistry c;

    p.setMarks(78);
    c.setMarks(85);

    total(p, c);            // called normally, not with a dot
    return 0;
}
```

**Output**
```
Physics   = 78
Chemistry = 85
Total     = 163
```

**Practice question**

**Q12.** What is a friend function? Write any three points about friendship.

---
---

# Answers

**Q1.** Four differences between procedural and OOP:

| Procedural | Object Oriented |
|---|---|
| Basic unit is the function | Basic unit is the object |
| Data is kept outside, separate from functions | Data and functions are kept together in a class |
| Any function can change the data | Only the class's own functions can change the data |
| No data hiding | Data hiding is possible using `private` |
| Follows top-down approach | Follows bottom-up approach |
| Example: C | Example: C++ |

**Q2.** The four pillars of OOP:
- **Encapsulation** — keeping data and functions together in one class and making the data private.
- **Abstraction** — showing only the needed things and hiding the inside details.
- **Inheritance** — a new class taking the properties of an existing class.
- **Polymorphism** — the same name doing different work in different situations.

**Q3.**
```cpp
#include <iostream>
using namespace std;

int main() {
    int roll;
    string name;
    float m1, m2, m3;

    cout << "Enter roll number: ";
    cin >> roll;
    cin.ignore();

    cout << "Enter name: ";
    getline(cin, name);

    cout << "Enter three marks: ";
    cin >> m1 >> m2 >> m3;

    float total = m1 + m2 + m3;

    cout << endl;
    cout << "Roll    = " << roll << endl;
    cout << "Name    = " << name << endl;
    cout << "Total   = " << total << endl;
    cout << "Average = " << total / 3 << endl;
    return 0;
}
```

**Q4.**
```cpp
#include <iostream>
using namespace std;

class Rectangle {
private:
    int length, breadth;

public:
    void setData(int l, int b) {
        length = l;
        breadth = b;
    }
    void showArea() {
        cout << "Area = " << length * breadth << endl;
    }
};

int main() {
    Rectangle r;
    r.setData(5, 4);
    r.showArea();
    return 0;
}
```
Output: `Area = 20`

**Q5.**
```cpp
#include <iostream>
using namespace std;

class Circle {
private:
    float radius;

public:
    void setRadius(float r) { radius = r; }
    float area() { return 3.14 * radius * radius; }     // inline
    void display();                                     // written outside
};

void Circle::display() {                                // non-inline
    cout << "Radius = " << radius << endl;
    cout << "Area   = " << area() << endl;
}

int main() {
    Circle c;
    c.setRadius(7);
    c.display();
    return 0;
}
```
Output:
```
Radius = 7
Area   = 153.86
```

**Q6.**
A static data member must be defined outside the class because writing it inside the class is only a
**declaration** — it just tells the compiler the name and type. Memory is not given. The line written
outside, like `int Student::count = 0;`, is what actually **creates the variable and gives it memory**.
If we forget this line, the program gives an error.

A static member function cannot use a normal data member because a static function is called
**without any object** (like `Student::showCount()`). A normal data member belongs to a particular
object. So there is no object to take the value from.

**Q7.** Difference between structure and union:

| Structure | Union |
|---|---|
| Every member gets its **own** memory | All members **share the same** memory |
| Size = total of all members | Size = size of the **biggest** member |
| All members can be used at the same time | Only **one** member can be used at a time |
| Changing one member does not affect others | Changing one member **spoils** the others |

**Q8.**
- (a) **Correct.** Default value is given from the right side.
- (b) **Wrong.** `a` has a default value but `b` and `c` after it do not. Default values must be
  given from **right to left**, without leaving a gap.
- (c) **Correct.** Both defaults are on the right side, one after the other.

**Q9.** The compiler does not make a function inline when:
1. The function is **too big**.
2. The function has a **loop** (`for`, `while`, `do-while`) or a `switch`.
3. The function is **recursive** (it calls itself).
4. The function is `virtual` and called using a base class pointer.

(Any three of these are enough.)

**Q10.**
```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    for (int i = 1; i <= 10; i++) {
        cout << setw(4) << 5
             << setw(4) << "x"
             << setw(4) << i
             << setw(4) << "="
             << setw(4) << 5 * i << endl;
    }
    return 0;
}
```
Output:
```
   5   x   1   =   5
   5   x   2   =  10
   5   x   3   =  15
   5   x   4   =  20
   5   x   5   =  25
   5   x   6   =  30
   5   x   7   =  35
   5   x   8   =  40
   5   x   9   =  45
   5   x  10   =  50
```

**Q11.**
```cpp
#include <iostream>
using namespace std;

int area(int side) {                    // square
    return side * side;
}
int area(int length, int breadth) {     // rectangle
    return length * breadth;
}
double area(double radius) {            // circle
    return 3.14 * radius * radius;
}

int main() {
    cout << "Square    = " << area(5) << endl;
    cout << "Rectangle = " << area(4, 6) << endl;
    cout << "Circle    = " << area(3.0) << endl;
    return 0;
}
```
Output:
```
Square    = 25
Rectangle = 24
Circle    = 28.26
```

**Q12.**
A **friend function** is a function that is not a member of a class, but the class allows it to use
its private data. It is declared inside the class using the keyword `friend`, and it is called
normally like `total(p, c)`, not with a dot.

Three points about friendship:
1. Friendship is **not both ways**. If class A makes B its friend, B can use A's private data, but A
   cannot use B's private data.
2. Friendship is **not inherited**. A friend of the parent class is not automatically a friend of the
   child class.
3. Only the class itself can give friendship. Outside code cannot take it by force.
4. A friend function can use the private data of **two different classes** at the same time.

(Any three points are enough.)

---

[Back to top](#c--unit-1)
