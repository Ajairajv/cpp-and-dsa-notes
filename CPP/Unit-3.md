# C++ — Unit 3

Simple notes for all Unit 3 topics.
For each topic: **what it is → a program → one practice question.**

Answers to all practice questions are at the [end of this file](#answers).

**How to run any program:**

```bash
g++ program.cpp -o program
./program
```

**Note:** the file programs in this unit **create files** (like `notes.txt`, `nums.dat`) in the same
folder where you run the program. That is normal — open them to see what was written.

### Topics

21. [Opening and closing files, modes of file](#21-opening-and-closing-files-modes-of-file)
22. [File stream functions, reading and writing files](#22-file-stream-functions-reading-and-writing-files)
23. [Sequential access and random access](#23-sequential-access-and-random-access)
24. [Binary file operations](#24-binary-file-operations)
25. [Classes, structures and file operations](#25-classes-structures-and-file-operations)
26. [Manager functions, default constructor, constructor with default arguments](#26-manager-functions-default-constructor-constructor-with-default-arguments)
27. [Parameterized constructor](#27-parameterized-constructor)
28. [Copy constructor](#28-copy-constructor)
29. [Destructors](#29-destructors)
30. [Initializer lists](#30-initializer-lists)

---

## 21. Opening and closing files, modes of file

**What it is**

Normal variables are lost when the program ends. A **file** stores data on the disk, so the data
stays even after the program ends.

To work with files, include the header **`<fstream>`**. It gives three classes:

| Class        | Work                                                              |
| ------------ | ----------------------------------------------------------------- |
| `ofstream` | **o**utput file stream — used to **write** to a file |
| `ifstream` | **i**nput file stream — used to **read** from a file |
| `fstream`  | used for **both** reading and writing                        |

```
          write (<<)                    read (>>)
Program  ------------>  FILE on disk  ------------>  Program
         ofstream                       ifstream
```

**Two ways to open a file**

```cpp
ofstream fout("notes.txt");            // way 1: using the constructor

ofstream fout;
fout.open("notes.txt");                // way 2: using the open() function
```

**Closing a file** — `fout.close();` saves the data and frees the file. Always close a file when
you are done with it.

**Checking if the file opened** — `if (!fout)` or `if (fout.is_open())`. Opening can fail, for
example when you try to read a file that does not exist.

**Modes of file** — the second argument of `open()` tells **how** to open the file:

| Mode            | Meaning                                                                          |
| --------------- | -------------------------------------------------------------------------------- |
| `ios::in`     | open for **reading** (default for `ifstream`)                             |
| `ios::out`    | open for **writing** (default for `ofstream`) — old data is erased       |
| `ios::app`    | **append** — all new data is added at the **end**, old data is kept |
| `ios::ate`    | open the file and jump to the **end** right away (you can still move anywhere later) |
| `ios::trunc`  | erase all old data if the file already exists                                    |
| `ios::binary` | open in **binary** mode (raw bytes, not text)                               |

Modes can be joined using `|`, for example: `fstream f("a.txt", ios::in | ios::out);`

**Program**

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // 1. OPEN USING CONSTRUCTOR - ofstream, default mode is ios::out
    ofstream fout("notes.txt");            // creates the file (old data is erased)
    if (!fout) {
        cout << "File could not be opened" << endl;
        return 1;
    }
    fout << "Line 1" << endl;
    fout.close();                          // always close the file
    cout << "notes.txt written using ios::out" << endl;

    // 2. OPEN USING open() - ios::app adds data at the END
    ofstream fapp;
    fapp.open("notes.txt", ios::app);      // old data is kept
    fapp << "Line 2 (appended)" << endl;
    fapp.close();
    cout << "One line added using ios::app" << endl;

    // 3. OPEN FOR READING - ifstream, default mode is ios::in
    ifstream fin;
    fin.open("notes.txt");
    if (fin.is_open())
        cout << "notes.txt is open for reading" << endl;

    string line;
    cout << "File contents:" << endl;
    while (getline(fin, line))
        cout << "  " << line << endl;
    fin.close();
    if (!fin.is_open())
        cout << "notes.txt is now closed" << endl;

    // 4. Opening a file that does not exist (for reading) FAILS
    ifstream f2("nofile.txt");
    if (!f2)
        cout << "nofile.txt could not be opened (it does not exist)" << endl;
    return 0;
}
```

**Output**

```
notes.txt written using ios::out
One line added using ios::app
notes.txt is open for reading
File contents:
  Line 1
  Line 2 (appended)
notes.txt is now closed
nofile.txt could not be opened (it does not exist)
```

**Practice question**

**Q21.** What is the difference between the file modes `ios::out`, `ios::app` and `ios::ate`?

---

## 22. File stream functions, reading and writing files

**What it is**

Once a file is open, we use **file stream functions** to write and read data. A file stream works
just like `cin` and `cout` — the only change is that the data goes to / comes from a file.

| Function            | Work                                                                             |
| ------------------- | -------------------------------------------------------------------------------- |
| `fout << x`       | writes`x` to the file (same as `cout <<`)                                    |
| `fin >> x`        | reads one **word / number** from the file — stops at a space or new line |
| `getline(fin, s)` | reads one **full line** (with spaces) into string `s`                     |
| `fout.put(ch)`    | writes **one character**                                                    |
| `fin.get(ch)`     | reads **one character** (spaces and new lines too)                          |
| `fin.eof()`       | returns`true` (1) when the **end of file** is reached                    |

**Reading till the end of the file** — the safe way is to put the read itself inside the loop:

```cpp
while (getline(fin, line)) { ... }    // stops when no more lines
while (fin.get(ch))        { ... }    // stops when no more characters
```

When the read fails at the end, the loop stops by itself. After that, `fin.eof()` gives `1`.

**Program**

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // WRITING to a file
    ofstream fout("data.txt");
    fout << "Ravi 85" << endl;            // << writes data, just like cout
    fout << "Neha 92" << endl;
    fout.put('#');                         // put() writes ONE character
    fout.put('\n');
    fout.close();
    cout << "data.txt written" << endl << endl;

    // READING word by word using >>
    ifstream fin("data.txt");
    string name;
    int marks;
    fin >> name >> marks;                  // >> stops at a space or new line
    cout << "Using >>      : " << name << " " << marks << endl;
    fin.close();

    // READING line by line using getline()
    ifstream fin2("data.txt");
    string line;
    cout << "Using getline():" << endl;
    while (getline(fin2, line))
        cout << "  [" << line << "]" << endl;
    fin2.close();

    // READING character by character using get()
    ifstream fin3("data.txt");
    char ch;
    int count = 0;
    while (fin3.get(ch))                   // get() reads ONE character (spaces too)
        count++;
    cout << "Using get()   : " << count << " characters read" << endl;
    cout << "eof() now     : " << fin3.eof() << " (1 means end of file reached)" << endl;
    fin3.close();
    return 0;
}
```

**Output**

```
data.txt written

Using >>      : Ravi 85
Using getline():
  [Ravi 85]
  [Neha 92]
  [#]
Using get()   : 18 characters read
eof() now     : 1 (1 means end of file reached)
```

(18 characters = `Ravi 85` + new line (8) + `Neha 92` + new line (8) + `#` + new line (2).)

**Practice question**

**Q22.** Write a program that writes the names of 3 cities into a file `city.txt` (one per line),
then reads the file back, prints every line, and prints the total number of lines.

---

## 23. Sequential access and random access

**What it is**

**Sequential access** — read the file from the **start to the end**, one item after another, in
order. Like listening to a song on a cassette tape. All programs so far used sequential access.

**Random access** — **jump directly** to any position in the file and read/write there. Like
choosing any song on a phone. No need to read everything before it.

Every file stream keeps a **position (pointer)** that says where the next read/write will happen:

- **get pointer** — position for the next **read** (input)
- **put pointer** — position for the next **write** (output)

| Function       | Work                                                   |
| -------------- | ------------------------------------------------------ |
| `seekg(pos)` | move the **get** pointer to byte `pos`          |
| `seekp(pos)` | move the **put** pointer to byte `pos`          |
| `tellg()`    | tells the current position of the **get** pointer |
| `tellp()`    | tells the current position of the **put** pointer |

(Easy to remember: **g** = **g**et = read, **p** = **p**ut = write.)

`seekg` and `seekp` can also take a **starting point** as the second argument:

| Starting point | Meaning                                                 |
| -------------- | ------------------------------------------------------- |
| `ios::beg`   | count from the **beginning** of the file (default) |
| `ios::cur`   | count from the **current** position                |
| `ios::end`   | count from the **end** of the file                 |

```
File:      A   B   C   D   E   F   G   H   I   J
Position:  0   1   2   3   4   5   6   7   8   9   10 (end)

seekg(4)            -> at E
seekg(2, ios::cur)  -> move 2 ahead from where you are
seekg(-1, ios::end) -> at J (1 back from the end)
seekg(0, ios::end); tellg()  -> 10 = size of the file
```

**Program**

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream fout("letters.txt");
    fout << "ABCDEFGHIJ";                  // 10 characters, positions 0 to 9
    fout.close();

    // SEQUENTIAL ACCESS - read from start to end, one by one
    ifstream fin("letters.txt");
    char ch;
    cout << "Sequential read : ";
    while (fin.get(ch))
        cout << ch;
    cout << endl;
    fin.close();

    // RANDOM ACCESS - jump to any position
    ifstream f("letters.txt");
    cout << "Start position  : " << f.tellg() << endl;

    f.seekg(4);                            // go to position 4 (from beginning)
    f.get(ch);
    cout << "seekg(4)        : " << ch << ", now at " << f.tellg() << endl;

    f.seekg(2, ios::cur);                  // move 2 ahead from current position
    f.get(ch);
    cout << "seekg(2,cur)    : " << ch << endl;

    f.seekg(-1, ios::end);                 // 1 position back from the end
    f.get(ch);
    cout << "seekg(-1,end)   : " << ch << endl;

    f.seekg(0, ios::end);                  // go to the end
    cout << "File size       : " << f.tellg() << " bytes" << endl;
    f.close();

    // seekp() - change ONE character in the middle of the file
    fstream fs("letters.txt", ios::in | ios::out);
    fs.seekp(4);                           // put pointer at position 4
    fs.put('*');                           // overwrite 'E' with '*'
    fs.seekg(0);                           // get pointer back to start
    cout << "After seekp(4)  : ";
    while (fs.get(ch))
        cout << ch;
    cout << endl;
    fs.close();
    return 0;
}
```

**Output**

```
Sequential read : ABCDEFGHIJ
Start position  : 0
seekg(4)        : E, now at 5
seekg(2,cur)    : H
seekg(-1,end)   : J
File size       : 10 bytes
After seekp(4)  : ABCD*FGHIJ
```

**Practice question**

**Q23.** Write a program that finds the **size of a file** (in bytes) using `seekg()` and `tellg()`.

---

## 24. Binary file operations

**What it is**

So far we wrote **text** files — numbers were saved as characters (`85` was saved as `'8'` and
`'5'`). A **binary file** saves data **exactly as it is stored in memory** (raw bytes). An `int`
always takes `sizeof(int)` = 4 bytes, whatever its value.

| Text file                            | Binary file                                          |
| ------------------------------------ | ---------------------------------------------------- |
| Data saved as readable characters    | Data saved as raw bytes (looks like junk in Notepad) |
| Uses`<<`, `>>`, `getline()`    | Uses`write()` and `read()`                       |
| Size depends on the number of digits | Size is fixed:`sizeof(type)` per item              |
| Slower (data must be converted)      | Faster (no conversion)                               |

Open a binary file with the mode **`ios::binary`**.

**The two functions**

```cpp
fout.write((char*)&x, sizeof(x));   // write the bytes of x into the file
fin.read((char*)&x, sizeof(x));     // read bytes from the file into x
```

- 1st argument — the **address** of the data, typecast to `char*` (because `write()`/`read()`
  work with bytes, and one `char` = one byte). `reinterpret_cast<char*>(&x)` does the same job.
- 2nd argument — **how many bytes** to write/read, usually `sizeof(x)`.

Since every item has a fixed size, random access is easy: item number `n` (starting from 0) is at
byte `n * sizeof(item)`. Also, `gcount()` tells how many bytes the last `read()` actually got.

**Program**

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    int nums[5] = {10, 20, 30, 40, 50};

    // WRITE the whole array in binary form
    ofstream fout("nums.dat", ios::binary);
    fout.write((char*)nums, sizeof(nums));       // write raw bytes
    fout.close();
    cout << "Wrote " << sizeof(nums) << " bytes to nums.dat" << endl;

    // READ the whole array back
    int x[5];
    ifstream fin("nums.dat", ios::binary);
    fin.read((char*)x, sizeof(x));               // read raw bytes
    cout << "Read back       : ";
    for (int i = 0; i < 5; i++)
        cout << x[i] << " ";
    cout << endl;

    // RANDOM ACCESS in a binary file: read only the 3rd number
    int n;
    fin.seekg(2 * sizeof(int), ios::beg);        // skip the first 2 ints
    fin.read((char*)&n, sizeof(n));
    cout << "3rd number      : " << n << endl;

    // gcount() tells how many bytes the last read() got
    cout << "Bytes last read : " << fin.gcount() << endl;
    fin.close();

    // A single double, using reinterpret_cast (same job as (char*))
    double pi = 3.14159, y = 0;
    ofstream f1("pi.dat", ios::binary);
    f1.write(reinterpret_cast<char*>(&pi), sizeof(pi));
    f1.close();
    ifstream f2("pi.dat", ios::binary);
    f2.read(reinterpret_cast<char*>(&y), sizeof(y));
    f2.close();
    cout << "double read back: " << y << endl;
    return 0;
}
```

**Output**

```
Wrote 20 bytes to nums.dat
Read back       : 10 20 30 40 50
3rd number      : 30
Bytes last read : 4
double read back: 3.14159
```

**Practice question**

**Q24.** Why do we open a binary file with `ios::binary`, and why is the address typecast to
`(char*)` in `write()` and `read()`?

---

## 25. Classes, structures and file operations

**What it is**

A whole **structure variable** or a whole **object** can be written to a binary file in one go,
using `write()`, and read back using `read()` — exactly like an `int` in the last topic:

```cpp
fout.write((char*)&s, sizeof(s));    // save the full struct / object
fin.read((char*)&s, sizeof(s));      // load it back
```

This is how small "record" programs work — student records, bank accounts, library books.
Each record has the same size, so:

- **Read all records** — `while (fin.read((char*)&s, sizeof(s)))` — stops at the end of file.
- **Read record number n** directly — `seekg((n - 1) * sizeof(s))` then `read()`.
- **Count the records** — file size ÷ `sizeof(s)`.

**Important:** use a `char` array (like `char name[20]`) for text inside such records, **not** a
`string`. A `string` keeps its letters somewhere else in memory and only stores a pointer to them —
so writing the raw bytes of a `string` saves only an address, not the actual name.

**Program**

```cpp
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

// STRUCTURE with file
struct Student {
    int roll;
    char name[20];
    float marks;
};

// CLASS with file
class Book {
    int id;
    char title[30];
    float price;
public:
    void setData(int i, const char *t, float p) {
        id = i;
        strcpy(title, t);
        price = p;
    }
    void show() {
        cout << id << "  " << title << "  Rs " << price << endl;
    }
};

int main() {
    // ---- Structures ----
    Student s[3] = { {1, "Aman", 78.5}, {2, "Riya", 91}, {3, "Karan", 66} };

    ofstream fout("students.dat", ios::binary);
    for (int i = 0; i < 3; i++)
        fout.write((char*)&s[i], sizeof(Student));   // write one struct at a time
    fout.close();

    Student t;
    ifstream fin("students.dat", ios::binary);
    cout << "Students read from file:" << endl;
    while (fin.read((char*)&t, sizeof(Student)))      // loop stops at end of file
        cout << t.roll << "  " << t.name << "  " << t.marks << endl;
    fin.close();
    cout << endl;

    // ---- Class objects ----
    Book b[3];
    b[0].setData(101, "C++ Basics", 350);
    b[1].setData(102, "DSA Guide", 550);
    b[2].setData(103, "OOP Concepts", 420);

    ofstream bout("books.dat", ios::binary);
    bout.write((char*)b, sizeof(b));                  // write all 3 objects at once
    bout.close();

    Book x;
    ifstream bin("books.dat", ios::binary);
    bin.seekg(1 * sizeof(Book), ios::beg);            // jump straight to the 2nd object
    bin.read((char*)&x, sizeof(Book));
    cout << "2nd book (random access): ";
    x.show();

    bin.seekg(0, ios::end);
    cout << "Number of books in file : " << bin.tellg() / sizeof(Book) << endl;
    bin.close();
    return 0;
}
```

**Output**

```
Students read from file:
1  Aman  78.5
2  Riya  91
3  Karan  66

2nd book (random access): 102  DSA Guide  Rs 550
Number of books in file : 3
```

**Practice question**

**Q25.** Write a `struct Employee` with `id`, `name` (char array) and `salary`. Write 3 employee
records to a binary file `emp.dat`, then read the file and print only the employees whose salary
is more than 30000.

---

## 26. Manager functions, default constructor, constructor with default arguments

**What it is**

**Manager functions** are special member functions that **manage the life of an object** — they
set it up when it is born and clean up when it dies. They are mainly the **constructors** and the
**destructor**. (The copy constructor is also a type of constructor.)

|              | Constructor                                                 | Destructor                                                    |
| ------------ | ----------------------------------------------------------- | ------------------------------------------------------------- |
| Name         | same as the class:`Box()`                                 | same as the class with`~`: `~Box()`                       |
| When it runs | **automatically** when an object is **created** | **automatically** when an object is **destroyed** |
| Job          | give starting values to data members                        | clean up (free memory, close files)                           |
| Return type  | none (not even`void`)                                     | none (not even`void`)                                       |
| Arguments    | can take arguments                                          | **never** takes arguments                               |
| Overloading  | can be overloaded (many constructors)                       | **only one** per class                                  |

Constructors should be written in the `public` section, so that objects can be created in `main()`.

**Default constructor** — a constructor that takes **no arguments**: `Box()`. It runs when you
write `Box b;`.
If you do not write **any** constructor, the compiler makes an empty default constructor for you.
But if you write **any** constructor yourself, the compiler does **not** make one.

**Constructor with default arguments** — a constructor whose parameters have default values,
like `Rect(int l = 5, int w = 2)`. One constructor can then be called with 0, 1 or 2 values.
It also works as a default constructor (because it can be called with no values).

**Careful:** do not write both `Rect()` and `Rect(int l = 5, int w = 2)` in the same class.
For `Rect r;` the compiler cannot decide which one to call — **ambiguity error**.

**Program**

```cpp
#include <iostream>
using namespace std;

class Box {
    int length, width;
public:
    Box() {                                   // DEFAULT CONSTRUCTOR - no arguments
        length = 1;
        width = 1;
        cout << "Default constructor called" << endl;
    }
    void show() {
        cout << "Box: " << length << " x " << width << endl;
    }
};

class Rect {
    int length, width;
public:
    Rect(int l = 5, int w = 2) {              // CONSTRUCTOR WITH DEFAULT ARGUMENTS
        length = l;
        width = w;
    }
    void show() {
        cout << "Rect: " << length << " x " << width
             << ", area = " << length * width << endl;
    }
};

int main() {
    Box b;                  // constructor is called AUTOMATICALLY here
    b.show();
    cout << endl;

    Rect r1;                // no values      -> l = 5, w = 2
    Rect r2(10);            // one value      -> l = 10, w = 2
    Rect r3(10, 4);         // both values    -> l = 10, w = 4
    r1.show();
    r2.show();
    r3.show();
    return 0;
}
```

**Output**

```
Default constructor called
Box: 1 x 1

Rect: 5 x 2, area = 10
Rect: 10 x 2, area = 20
Rect: 10 x 4, area = 40
```

**Practice question**

**Q26.** What is a default constructor? When does the compiler create one by itself? What problem
happens if a class has both `A()` and `A(int x = 0)`?

---

## 27. Parameterized constructor

**What it is**

A **parameterized constructor** is a constructor that **takes arguments**. It lets every object
start with **different values**, given at the time of creating the object.

```cpp
Point(int a, int b) { x = a; y = b; }
```

**Ways to call it**

| Way                              | Code                            |
| -------------------------------- | ------------------------------- |
| Implicit call (short, most used) | `Point p1(3, 4);`             |
| Explicit call                    | `Point p2 = Point(5, 6);`     |
| With`new` (dynamic object)     | `Point *p = new Point(7, 8);` |

**Constructor overloading** — a class can have many constructors with different parameter lists
(like function overloading). Below, `Point` has a default constructor **and** a parameterized one.

**Remember:** if a class has **only** a parameterized constructor, then `Point p;` gives an
**error** — the compiler does not make a default constructor any more. Add a default constructor
yourself if you need it.

**Program**

```cpp
#include <iostream>
using namespace std;

class Point {
    int x, y;
public:
    Point() {                         // default constructor
        x = 0;
        y = 0;
    }
    Point(int a, int b) {             // PARAMETERIZED CONSTRUCTOR
        x = a;
        y = b;
    }
    void show() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};

int main() {
    Point p1(3, 4);                   // implicit call (short form, most common)
    Point p2 = Point(5, 6);           // explicit call
    Point p3;                         // default constructor
    Point *p4 = new Point(7, 8);      // with new (dynamic object)

    cout << "p1 = "; p1.show();
    cout << "p2 = "; p2.show();
    cout << "p3 = "; p3.show();
    cout << "p4 = "; p4->show();
    delete p4;
    return 0;
}
```

**Output**

```
p1 = (3, 4)
p2 = (5, 6)
p3 = (0, 0)
p4 = (7, 8)
```

**Practice question**

**Q27.** Write a class `Rectangle` with `length` and `breadth`. Use a parameterized constructor to
set them, and a function `area()` that returns the area. Create two objects and print their areas.

---

## 28. Copy constructor

**What it is**

A **copy constructor** makes a **new object as a copy of an existing object** of the same class.

```cpp
Student(const Student &s) { ... }     // parameter: reference to an object of the same class
```

**When is it called?**

1. When an object is created from another object: `Student b(a);`
2. Same thing written with `=` at creation: `Student c = a;`
3. When an object is **passed by value** to a function: `display(a);`
4. When a function **returns** an object by value (the compiler often skips this copy to save time).

(Note: `c = a;` on an object that **already exists** is assignment, not the copy constructor.)

**Why must the parameter be a reference (`&`)?** If it were passed by value, then passing the
object would itself need a copy... which calls the copy constructor again... and again —
endless calls. So it is always a reference, usually `const` so the original cannot be changed.

**Shallow copy vs deep copy**

If you do not write a copy constructor, the compiler makes one that copies every member as it is
— a **shallow copy**. This is fine for normal members. But if a member is a **pointer**, both
objects get the **same address**, so they share the same memory:

```
Shallow copy:                         Deep copy:
a.marks ---+                          a.marks ---> [ 80 ]
           +---> [ 80 ]               b.marks ---> [ 80 ]   (its own memory)
b.marks ---+
(change b -> a also changes,          (change b -> a stays the same)
 and both will delete the same memory)
```

A **deep copy** (our own copy constructor) gives the copy its **own new memory** with the same value.

**Program**

```cpp
#include <iostream>
using namespace std;

class Student {
    int roll;
    int *marks;                               // pointer member
public:
    Student(int r, int m) {
        roll = r;
        marks = new int(m);
    }
    Student(const Student &s) {               // COPY CONSTRUCTOR (deep copy)
        roll = s.roll;
        marks = new int(*s.marks);            // new memory for the copy
        cout << "Copy constructor called" << endl;
    }
    void setMarks(int m) { *marks = m; }
    void show() {
        cout << "Roll " << roll << ", Marks " << *marks << endl;
    }
    ~Student() { delete marks; }
};

void display(Student s) {                     // pass BY VALUE -> copy is made
    s.show();
}

int main() {
    Student a(1, 80);

    Student b(a);                             // case 1: object made from another object
    Student c = a;                            // case 2: same thing, written with =
    cout << "Passing to a function by value:" << endl;
    display(a);                               // case 3: pass by value

    b.setMarks(95);                           // change ONLY the copy
    cout << endl << "After changing b:" << endl;
    cout << "a -> "; a.show();
    cout << "b -> "; b.show();
    cout << "c -> "; c.show();
    return 0;
}
```

**Output**

```
Copy constructor called
Copy constructor called
Passing to a function by value:
Copy constructor called
Roll 1, Marks 80

After changing b:
a -> Roll 1, Marks 80
b -> Roll 1, Marks 95
c -> Roll 1, Marks 80
```

Changing `b` did **not** change `a` — because of the deep copy, each object has its own `marks`.

**Practice question**

**Q28.** Why must the parameter of a copy constructor be a reference? Write any three situations
in which the copy constructor is called.

---

## 29. Destructors

**What it is**

A **destructor** is a special member function that runs **automatically when an object is
destroyed** (goes out of scope, or is `delete`d). Its job is **clean-up** — free memory taken with
`new`, close files, etc.

```cpp
~Test() { ... }      // tilde (~) + class name
```

**Rules**

- Same name as the class, with a `~` in front.
- No return type, and **no arguments**.
- So it **cannot be overloaded** — only one destructor per class.
- You never call it yourself; C++ calls it.

**When does it run?**

- Local object — at the closing `}` of the block / function where it was created.
- Object made with `new` — only when you write `delete`.

**Order of destruction** — objects are destroyed in the **reverse order** of creation
(last created = first destroyed), like plates in a stack.

```
Created:    t1  ->  t2  ->  t3
Destroyed:  t3  ->  t2  ->  t1
```

**Constructors, destructors and file handling** — a very good use: open a file in the
**constructor** and close it in the **destructor**. Then the file is always closed, even if you
forget to call `close()`. (In fact, `ofstream`/`ifstream` themselves close the file in their own
destructors.)

**Program**

```cpp
#include <iostream>
#include <fstream>
using namespace std;

class Test {
    int id;
public:
    Test(int i) {
        id = i;
        cout << "Constructor " << id << endl;
    }
    ~Test() {                                 // DESTRUCTOR
        cout << "Destructor  " << id << endl;
    }
};

// Constructor opens the file, destructor closes it
class Logger {
    ofstream fout;
public:
    Logger(const char *fname) {
        fout.open(fname);
        cout << "Logger: file opened" << endl;
    }
    void write(const char *msg) { fout << msg << endl; }
    ~Logger() {
        fout.close();
        cout << "Logger: file closed by destructor" << endl;
    }
};

int main() {
    Test t1(1);
    Test t2(2);
    {
        Test t3(3);
        cout << "Leaving inner block" << endl;
    }                                         // t3 is destroyed here
    Test *p = new Test(4);
    delete p;                                 // destructor of 4 runs here
    cout << endl;

    {
        Logger log("log.txt");
        log.write("Program started");
    }                                         // log goes out of scope -> file closed

    cout << endl << "End of main" << endl;
    return 0;
}                                             // t2 then t1 destroyed (reverse order)
```

**Output**

```
Constructor 1
Constructor 2
Constructor 3
Leaving inner block
Destructor  3
Constructor 4
Destructor  4

Logger: file opened
Logger: file closed by destructor

End of main
Destructor  2
Destructor  1
```

**Practice question**

**Q29.** Write a program to show that destructors are called in the **reverse order** of
constructors. Create 3 objects and print a message in both the constructor and the destructor.

---

## 30. Initializer lists

**What it is**

An **initializer list** is a short way to give values to data members in a constructor. It is
written **after the `:`** and **before the body `{ }`** of the constructor:

```cpp
Point(int a, int b) : x(a), y(b) { }      // x gets a, y gets b
```

This does the same job as `x = a; y = b;` inside the body — but the members get their values
**while they are being created**, not after.

**When is it a MUST?**

| Member type                               | Why the initializer list is needed                                                              |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `const` member                          | A`const` cannot be changed after creation, so `roll = r;` in the body is an **error** |
| Reference member (`int &`)              | A reference **must** be bound when it is created (topic 19)                                |
| Member object with no default constructor | It must be given its arguments at creation time                                                 |

**Order rule:** members are always initialized in the order they are **declared in the class**,
not in the order written in the list. So write the list in the same order to avoid confusion.

**Program**

```cpp
#include <iostream>
#include <string>
using namespace std;

class Point {
    int x, y;
public:
    Point(int a, int b) : x(a), y(b) {      // INITIALIZER LIST
    }
    void show() { cout << "(" << x << ", " << y << ")" << endl; }
};

class Student {
    const int roll;                          // const member
    int &marks;                              // reference member
    string name;
public:
    // const and reference members MUST be set in the initializer list
    Student(int r, int &m, string n) : roll(r), marks(m), name(n) {
    }
    void show() {
        cout << "Roll " << roll << ", " << name << ", Marks " << marks << endl;
    }
};

int main() {
    Point p(3, 4);
    cout << "Point   : ";
    p.show();

    int m = 80;
    Student s(1, m, "Aman");
    cout << "Student : ";
    s.show();

    m = 90;                                  // marks is a reference to m
    cout << "After m = 90 -> ";
    s.show();
    return 0;
}
```

**Output**

```
Point   : (3, 4)
Student : Roll 1, Aman, Marks 80
After m = 90 -> Roll 1, Aman, Marks 90
```

**Practice question**

**Q30.** Which types of data members **must** be initialized using an initializer list? Write a
class `Circle` with a `const float PI` member and a `radius`, set both using an initializer list,
and print the area.

---

---

# Answers

**Q21.**

- `ios::out` — opens the file for **writing**. If the file already has data, **all old data is
  erased** and writing starts from the beginning. It is the default mode of `ofstream`.
- `ios::app` — **append** mode. Old data is **kept**, and **every** write always goes to the
  **end** of the file.
- `ios::ate` — "at end". The file opens and the pointer is placed at the **end** at the start,
  but you **can move** it anywhere later using `seekp()`/`seekg()` and write/read there.

So the main difference: `out` erases old data; `app` keeps it and always writes at the end; `ate`
only *starts* at the end but allows moving anywhere.

**Q22.**

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    ofstream fout("city.txt");
    fout << "Delhi" << endl;
    fout << "Mumbai" << endl;
    fout << "Jalandhar" << endl;
    fout.close();

    ifstream fin("city.txt");
    string line;
    int count = 0;
    while (getline(fin, line)) {
        cout << line << endl;
        count++;
    }
    fin.close();
    cout << "Number of lines = " << count << endl;
    return 0;
}
```

Output:

```
Delhi
Mumbai
Jalandhar
Number of lines = 3
```

**Q23.**

```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ofstream fout("sample.txt", ios::binary);
    fout << "Hello File";                  // 10 characters
    fout.close();

    ifstream fin("sample.txt", ios::binary);
    if (!fin) {
        cout << "File not found" << endl;
        return 1;
    }
    fin.seekg(0, ios::end);                // go to the end of the file
    cout << "Size of file = " << fin.tellg() << " bytes" << endl;
    fin.close();
    return 0;
}
```

Output: `Size of file = 10 bytes`

(`seekg(0, ios::end)` moves the get pointer to the very end, and `tellg()` then tells how many
bytes are before it — which is the size of the file.)

**Q24.**

- **`ios::binary`** tells C++ to read/write the bytes **exactly as they are**, with no changes.
  In text mode (especially on Windows), some bytes are changed — for example a new line `\n` is
  saved as two bytes `\r\n`. In a binary file, any byte of an `int` or `float` may look like `\n`,
  so text mode could damage the data. Binary mode stops this.
- **`(char*)` typecast** — `write()` and `read()` are made to work with **bytes**, and their first
  parameter is a `char*` (one `char` = one byte). The address of an `int`, `float`, struct or
  object is a different pointer type, so it must be typecast to `char*` to say "treat this memory
  as a row of bytes". `reinterpret_cast<char*>(&x)` is the C++-style way of writing the same cast.

**Q25.**

```cpp
#include <iostream>
#include <fstream>
using namespace std;

struct Employee {
    int id;
    char name[20];
    float salary;
};

int main() {
    Employee e[3] = { {1, "Ajay", 25000}, {2, "Priya", 42000}, {3, "Rohit", 35000} };

    ofstream fout("emp.dat", ios::binary);
    for (int i = 0; i < 3; i++)
        fout.write((char*)&e[i], sizeof(Employee));
    fout.close();

    Employee t;
    ifstream fin("emp.dat", ios::binary);
    cout << "Employees with salary > 30000:" << endl;
    while (fin.read((char*)&t, sizeof(Employee))) {
        if (t.salary > 30000)
            cout << t.id << "  " << t.name << "  " << t.salary << endl;
    }
    fin.close();
    return 0;
}
```

Output:

```
Employees with salary > 30000:
2  Priya  42000
3  Rohit  35000
```

**Q26.** A **default constructor** is a constructor that can be called with **no arguments**, like
`A()`. It runs when an object is created without any values: `A obj;`.
The compiler creates an (empty) default constructor by itself **only when the class has no
constructor at all**. If you write even one constructor (for example a parameterized one), the
compiler does not create it.
If a class has both `A()` and `A(int x = 0)`, then `A obj;` can match **both** of them (the second
one can also be called with no value). The compiler cannot choose, so it gives an **ambiguity
error**.

**Q27.**

```cpp
#include <iostream>
using namespace std;

class Rectangle {
    int length, breadth;
public:
    Rectangle(int l, int b) {          // parameterized constructor
        length = l;
        breadth = b;
    }
    int area() {
        return length * breadth;
    }
};

int main() {
    Rectangle r1(4, 5);
    Rectangle r2(10, 3);
    cout << "Area of r1 = " << r1.area() << endl;
    cout << "Area of r2 = " << r2.area() << endl;
    return 0;
}
```

Output:

```
Area of r1 = 20
Area of r2 = 30
```

**Q28.** The parameter must be a **reference** because if it were passed **by value**, C++ would
need to make a copy of the argument to pass it — and making a copy means calling the copy
constructor again, which again needs a copy, and so on **forever** (infinite recursion). With a
reference, no copy is made, so this problem does not happen. (The compiler gives an error if you
try to pass by value.) It is usually made `const` so the original object cannot be changed by
mistake.

The copy constructor is called when:

1. An object is created from another object: `Student b(a);`
2. An object is created and given another object with `=`: `Student c = a;`
3. An object is **passed by value** to a function: `display(a);`
4. A function **returns** an object by value (the compiler may skip this copy as an optimization).

(Any three are enough.)

**Q29.**

```cpp
#include <iostream>
using namespace std;

class Demo {
    char name;
public:
    Demo(char n) {
        name = n;
        cout << "Object " << name << " created" << endl;
    }
    ~Demo() {
        cout << "Object " << name << " destroyed" << endl;
    }
};

int main() {
    Demo a('A');
    Demo b('B');
    Demo c('C');
    cout << "--- end of main ---" << endl;
    return 0;
}
```

Output:

```
Object A created
Object B created
Object C created
--- end of main ---
Object C destroyed
Object B destroyed
Object A destroyed
```

The objects were created A, B, C but destroyed C, B, A — the **reverse order**.

**Q30.** These data members **must** be initialized using an initializer list:

1. `const` data members
2. Reference data members (`int &x`)
3. Member objects of a class that has no default constructor

```cpp
#include <iostream>
using namespace std;

class Circle {
    const float PI;                   // const member
    float radius;
public:
    Circle(float r) : PI(3.14), radius(r) {     // initializer list
    }
    float area() {
        return PI * radius * radius;
    }
};

int main() {
    Circle c(10);
    cout << "Area = " << c.area() << endl;
    return 0;
}
```

Output: `Area = 314`

---

[Back to top](#c--unit-3)
