# C++ MCQs — Unit 1

Coding/output questions here use **C++** (the language used for coding practice).
For DSA MCQs, code is shown in **C**, matching the exam pattern — see [DSA MCQs](DSA.md).

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run to confirm the answer — nothing here is guessed.

---

**Q1.** Which of these is **not** a feature of Object Oriented Programming?
(a) Encapsulation
(b) Inheritance
(c) Goto statement
(d) Polymorphism

**Q2.** The default access specifier of a `class` in C++ is:
(a) public
(b) private
(c) protected
(d) friend

**Q3.** Which header file is required to use `cin` and `cout`?
(a) `<conio.h>`
(b) `<iostream>`
(c) `<stdio.h>`
(d) `<string.h>`

**Q4.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class Counter {
public:
    static int count;
    Counter() { count++; }
};
int Counter::count = 0;
int main() {
    Counter a, b, c;
    cout << Counter::count;
    return 0;
}
```
(a) 0
(b) 1
(c) 2
(d) 3

**Q5.** A static member function of a class can directly access:
(a) Only static data members
(b) Only non-static data members
(c) Both static and non-static data members
(d) No data members at all

**Q6.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
int mul(int a, int b = 4, int c = 2) {
    return a * b * c;
}
int main() {
    cout << mul(5, 3);
    return 0;
}
```
(a) 10
(b) 15
(c) 30
(d) 40

**Q7.** Which of these default-argument declarations is **invalid**?
(a) `void f(int a, int b = 2);`
(b) `void f(int a = 1, int b);`
(c) `void f(int a = 1, int b = 2);`
(d) `void f(int a, int b, int c = 3);`

**Q8.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
void show(int x) { cout << "int:" << x; }
void show(double x) { cout << "double:" << x; }
int main() {
    show(10);
    return 0;
}
```
(a) int:10
(b) double:10
(c) Compiler error
(d) int:10double:10

**Q9.** Two overloaded functions can differ only in:
(a) Return type
(b) Function name
(c) Number or type of parameters
(d) Access specifier

**Q10.** A friend function of a class:
(a) Is a member of the class
(b) Can access the class's private data even though it is not a member
(c) Cannot access private data at all
(d) Must be defined inside the class

**Q11.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class Box {
    int volume;
public:
    Box(int v) : volume(v) {}
    friend void printVolume(Box b);
};
void printVolume(Box b) {
    cout << b.volume;
}
int main() {
    Box b(50);
    printVolume(b);
    return 0;
}
```
(a) 0
(b) 50
(c) Compiler error, private member cannot be accessed
(d) Garbage value

**Q12.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
inline int square(int x) { return x * x; }
int main() {
    cout << square(6);
    return 0;
}
```
(a) 6
(b) 12
(c) 36
(d) 66

**Q13.** The `inline` keyword before a function is:
(a) A strict command the compiler must always obey
(b) A request to the compiler, which it may or may not honour
(c) Only usable outside a class
(d) Applicable only to `main()`

**Q14.** Which manipulator is used to fix the number of digits after the decimal point?
(a) `setw`
(b) `endl`
(c) `setprecision`
(d) `flush`

**Q15.** By default, a `struct` in C++ has its members as:
(a) private
(b) public
(c) protected
(d) static

**Q16.** In a `union`, all members:
(a) Have separate memory locations
(b) Share the same memory location
(c) Must be of the same data type
(d) Cannot be accessed at all

**Q17.** The scope resolution operator in C++ is:
(a) `->`
(b) `::`
(c) `.`
(d) `&`

**Q18.** Which of the following correctly defines a member function `show()` of class `Point`
outside the class?
(a) `void show() Point { }`
(b) `Point void show() { }`
(c) `void Point::show() { }`
(d) `void Point.show() { }`

**Q19.** A non-inline (outer) member function is:
(a) Declared and defined both inside the class
(b) Declared inside the class, defined outside using `::`
(c) Declared outside, defined inside
(d) Not allowed in C++

**Q20.** An `enum` in C++ is best described as:
(a) A set of named integer constants
(b) A pointer type
(c) A kind of loop
(d) A built-in sorting function

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | c | 11 | b |
| 2 | b | 12 | c |
| 3 | b | 13 | b |
| 4 | d | 14 | c |
| 5 | a | 15 | b |
| 6 | c | 16 | b |
| 7 | b | 17 | b |
| 8 | a | 18 | c |
| 9 | c | 19 | b |
| 10 | b | 20 | a |
