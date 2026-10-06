# C++ MCQs — Unit 3

Coding/output questions here use **C++** (the language used for coding practice).
For DSA MCQs, code is shown in **C**, matching the exam pattern — see [DSA MCQs](DSA.md).

Answer key is at the [end of this file](#answer-key). All code-output questions were compiled and
run to confirm the answer — nothing here is guessed.

---

**Q1.** Which header file must be included for file handling in C++?
(a) `<iostream>`
(b) `<fstream>`
(c) `<file.h>`
(d) `<stdio>`

**Q2.** Which class is used **only for reading** data from a file?
(a) `ofstream`
(b) `fstream`
(c) `ifstream`
(d) `ostream`

**Q3.** Which file mode adds new data at the **end** of a file without erasing the old data?
(a) `ios::app`
(b) `ios::out`
(c) `ios::trunc`
(d) `ios::in`

**Q4.** The default mode of an `ofstream` object is:
(a) `ios::in`
(b) `ios::app`
(c) `ios::binary`
(d) `ios::out`

**Q5.** What is the output of this program?
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main() {
    ofstream f("t.txt");
    f << "AB";
    f.close();
    f.open("t.txt", ios::app);
    f << "CD";
    f.close();
    ifstream g("t.txt");
    string s;
    g >> s;
    cout << s;
    return 0;
}
```
(a) `AB`
(b) `CD`
(c) `ABCD`
(d) `CDAB`

**Q6.** What is the output of this program?
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main() {
    ofstream f("t.txt");
    f << "AB";
    f.close();
    f.open("t.txt");
    f << "CD";
    f.close();
    ifstream g("t.txt");
    string s;
    g >> s;
    cout << s;
    return 0;
}
```
(a) `ABCD`
(b) `CD`
(c) `AB`
(d) `CDAB`

**Q7.** Which function reads a **full line** (including spaces) from a file into a `string`?
(a) `get()`
(b) `put()`
(c) `eof()`
(d) `getline()`

**Q8.** What is the output of this program?
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
int main() {
    ofstream f("msg.txt");
    f << "Hello World";
    f.close();
    ifstream g("msg.txt");
    string s;
    g >> s;
    cout << s;
    return 0;
}
```
(a) `Hello World`
(b) `Hello`
(c) `World`
(d) Nothing is printed

**Q9.** The function `seekg()` is used to:
(a) Move the get (read) pointer to a given position
(b) Move the put (write) pointer to a given position
(c) Tell the current position of the get pointer
(d) Close the file

**Q10.** What is the output of this program?
```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    ofstream f("d.txt");
    f << "0123456789";
    f.close();
    ifstream g("d.txt");
    char ch;
    g.seekg(-3, ios::end);
    g.get(ch);
    cout << ch;
    return 0;
}
```
(a) `7`
(b) `6`
(c) `3`
(d) `9`

**Q11.** Which function is used to write data to a **binary** file?
(a) `put()`
(b) `<<`
(c) `write()`
(d) `getline()`

**Q12.** What is the output of this program? (Assume `sizeof(int)` is 4.)
```cpp
#include <iostream>
#include <fstream>
using namespace std;
int main() {
    int a[4] = {1, 2, 3, 4};
    ofstream f("a.dat", ios::binary);
    f.write((char*)a, sizeof(a));
    f.close();
    ifstream g("a.dat", ios::binary);
    g.seekg(0, ios::end);
    cout << g.tellg();
    return 0;
}
```
(a) `4`
(b) `8`
(c) `32`
(d) `16`

**Q13.** Which statement about a **constructor** is TRUE?
(a) It has the same name as the class and has no return type
(b) It must have the return type `void`
(c) It must be called manually after creating an object
(d) A class can have only one constructor

**Q14.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class A {
    int x, y;
public:
    A(int a = 2, int b = 3) {
        x = a;
        y = b;
    }
    void show() { cout << x + y; }
};
int main() {
    A obj(5);
    obj.show();
    return 0;
}
```
(a) `5`
(b) `8`
(c) `10`
(d) `6`

**Q15.** The parameter of a copy constructor is passed by reference because:
(a) References use less memory than `int`
(b) The compiler does not allow objects as parameters
(c) Passing by value would call the copy constructor again and again (endless recursion)
(d) It makes the program run in parallel

**Q16.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class T {
public:
    T() { }
    T(const T &t) { cout << "C"; }
};
void f(T t) { }
int main() {
    T a;
    T b = a;
    f(b);
    return 0;
}
```
(a) `C`
(b) `CC`
(c) `CCC`
(d) Nothing is printed

**Q17.** Which statement about a **destructor** is TRUE?
(a) It can take arguments
(b) A class can have many destructors (overloading)
(c) It must be called manually before the program ends
(d) Its name is the class name with `~`, and it has no arguments and no return type

**Q18.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class X {
    int n;
public:
    X(int i) { n = i; }
    ~X() { cout << n; }
};
int main() {
    X a(1), b(2), c(3);
    return 0;
}
```
(a) `321`
(b) `123`
(c) `132`
(d) Nothing is printed

**Q19.** Which data members **must** be initialized using a constructor's initializer list?
(a) `static` members
(b) `public` members
(c) `const` members and reference members
(d) All `int` members

**Q20.** What is the output of this program?
```cpp
#include <iostream>
using namespace std;
class A {
    const int val;
public:
    A(int v) : val(v * 2) { }
    void show() { cout << val; }
};
int main() {
    A a(10);
    a.show();
    return 0;
}
```
(a) `10`
(b) `0`
(c) Compiler error, a `const` member cannot be given a value
(d) `20`

---

# Answer Key

| Q | Ans | Q | Ans |
|---|---|---|---|
| 1 | b | 11 | c |
| 2 | c | 12 | d |
| 3 | a | 13 | a |
| 4 | d | 14 | b |
| 5 | c | 15 | c |
| 6 | b | 16 | b |
| 7 | d | 17 | d |
| 8 | b | 18 | a |
| 9 | a | 19 | c |
| 10 | a | 20 | d |
