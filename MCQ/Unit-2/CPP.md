# C++ MCQs — Unit 2

Coding/output questions here use **C++** (the language used for coding practice).
For DSA MCQs, code is shown in **C**, matching the exam pattern — see [DSA MCQs](DSA.md).

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run to confirm the answer — nothing here is guessed.

---

**Q1.** A pointer variable stores:
(a) The value of another variable
(b) The address of another variable
(c) The name of another variable
(d) A copy of the whole program

**Q2.** Which operator gives the address of a variable?
(a) `*`
(b) `&`
(c) `->`
(d) `::`

**Q3.** A `void*` pointer:
(a) Can hold the address of any data type but must be typecast before dereferencing
(b) Can never hold any address
(c) Can only point to `void` functions
(d) Is the same as a `NULL` pointer

**Q4.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int a[5] = {10, 20, 30, 40, 50};
    int *p = a;
    cout << *(p + 2);
    return 0;
}
```
(a) 10
(b) 20
(c) 30
(d) 2

**Q5.** A dangling pointer is one that:
(a) Was never initialized
(b) Points to memory that has already been freed/deleted
(c) Always holds the value 0
(d) Points to another pointer

**Q6.** A wild pointer is one that:
(a) Points to freed memory
(b) Is declared but never initialized, so it holds a garbage address
(c) Always points to the first element of an array
(d) Cannot be declared in C++

**Q7.** In modern C++, a null pointer is assigned using:
(a) `void`
(b) `0.0`
(c) `nullptr`
(d) `empty`

**Q8.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int x = 25;
    int *p = &x;
    int **pp = &p;
    cout << **pp;
    return 0;
}
```
(a) 25
(b) The address of x
(c) The address of p
(d) Compiler error

**Q9.** The `this` pointer inside a member function points to:
(a) The class itself
(b) The object that called the function
(c) The first data member declared
(d) Nothing, it is always `NULL`

**Q10.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class Point {
    int x;
public:
    void setX(int x) {
        this->x = x;
    }
    void show() { cout << x; }
};
int main() {
    Point p;
    p.setX(9);
    p.show();
    return 0;
}
```
(a) 0
(b) 9
(c) Garbage value
(d) Compiler error

**Q11.** Accessing a member through a pointer to an object uses which operator?
(a) `.`
(b) `->`
(c) `&`
(d) `::`

**Q12.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
int main() {
    int a[2][3] = {{1,2,3},{4,5,6}};
    cout << a[1][2];
    return 0;
}
```
(a) 3
(b) 5
(c) 6
(d) Compiler error

**Q13.** Which header file must be included to use the C++ `string` class?
(a) `<cstring>`
(b) `<string>`
(c) `<iostream>`
(d) `<strings.h>`

**Q14.** What is the output of this program?
```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    string s = "Data Structures";
    cout << s.length();
    return 0;
}
```
(a) 14
(b) 15
(c) 16
(d) 13

**Q15.** What is the output of this program?
```cpp
#include <iostream>
#include <string>
using namespace std;
int main() {
    string s = "programming";
    cout << s.substr(3, 4);
    return 0;
}
```
(a) `prog`
(b) `gram`
(c) `ramm`
(d) `ming`

**Q16.** If `s.find("text")` does not find "text" inside the string `s`, it returns:
(a) `-1`
(b) `0`
(c) `string::npos`
(d) `NULL`

**Q17.** A reference variable in C++:
(a) Must be initialized at the time of declaration
(b) Can be left uninitialized like a pointer
(c) Can be reassigned to refer to a different variable later
(d) Can hold the value `nullptr`

**Q18.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
void swapRef(int &a, int &b) {
    int t = a; a = b; b = t;
}
int main() {
    int x = 3, y = 7;
    swapRef(x, y);
    cout << x << " " << y;
    return 0;
}
```
(a) `3 7`
(b) `7 3`
(c) `0 0`
(d) Compiler error

**Q19.** Compared to a pointer, a key advantage of a reference variable is:
(a) It can point to multiple variables at once
(b) It is simpler to use and always refers to a valid variable once initialized
(c) It uses less memory than an `int`
(d) It does not need a data type

**Q20.** A pointer to a data member (`Type ClassName::*ptr`) is different from a normal pointer
because:
(a) It stores a fixed memory address on its own
(b) It only makes sense when combined with an actual object of that class
(c) It can only point to static members
(d) It cannot be declared in C++

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | b | 11 | b |
| 2 | b | 12 | c |
| 3 | a | 13 | b |
| 4 | c | 14 | b |
| 5 | b | 15 | b |
| 6 | b | 16 | c |
| 7 | c | 17 | a |
| 8 | a | 18 | b |
| 9 | b | 19 | b |
| 10 | b | 20 | b |
