# C++ — Question Bank (Unit 1, Unit 2 & Unit 3)

Basic to advanced questions for practice. Theory questions need short written answers.
Coding questions must be **typed and run** in a compiler, not just read.

Short answers for the theory questions are at the [end of this file](#answers).
Coding questions have no fixed answer — check your output against what the question asks.

---

## How to use this question bank

- **Basic** = definitions, one-line differences, very short code.
- **Intermediate** = write a small program, predict output, spot the error.
- **Advanced** = programs with more than one class/concept combined.

---

## Unit 1

### 1. Procedural vs Object Oriented Programming

**Basic**
1. What is procedural programming? Give one example language.
2. What is Object Oriented Programming (OOP)? Give one example language.
3. Name any four features of OOP.

**Intermediate**
4. Give two differences between procedural programming and OOP.
5. Why is data less safe in procedural programming than in OOP?

**Advanced**
6. A college wants to manage Student records (roll number, name, marks). Explain in 3–4 lines
   how you would design this the OOP way instead of the procedural way.

### 2. Concepts of OOP

**Basic**
1. Define: Class, Object.
2. Define: Encapsulation.
3. Define: Abstraction.
4. Define: Inheritance.
5. Define: Polymorphism.

**Intermediate**
6. Give a real-life example each for encapsulation and inheritance.
7. What is the difference between abstraction and encapsulation?

**Advanced**
8. Write a class `Car` with private data members `speed` and `fuel`, and public member
   functions to set and show them. Which OOP concept does the `private` keyword demonstrate?

### 3. Reading and writing data (cin and cout)

**Basic**
1. Which header file is needed for `cin` and `cout`?
2. What does `cin >>` do? What does `cout <<` do?
3. What is `endl` used for?

**Intermediate**
4. Write a program that reads a student's name and one mark using `cin` and prints them using `cout`.
5. What happens if you type text (like `abc`) when the program expects an `int` with `cin >> x`?

**Advanced**
6. Write a program that reads three subject marks with a single `cin` statement (chained `>>`),
   finds their total and average, and prints both.

### 4. Classes, objects and members

**Basic**
1. What is a data member? What is a member function?
2. How do you create (declare) an object of a class?
3. What is the default access specifier of a class in C++?

**Intermediate**
4. Write a class `Rectangle` with `length` and `breadth` as private data members, a function
   `setData()` to take input, and a function `area()` to print the area.
5. Can a class have more than one object? Show it with one line of code.

**Advanced**
6. Write a program with a class `Book` (title, price) that creates an array of 3 `Book` objects,
   takes input for all of them, and prints the most expensive book.

### 5. Inline and non-inline member functions

**Basic**
1. What is an inline member function (defined inside the class)?
2. What is a non-inline (outer) member function?
3. Which operator is used to define a member function outside the class?

**Intermediate**
4. Write the same function `display()` of a class `Point` in two ways: once inside the class,
   once outside using the scope resolution operator.
5. Does writing a function inside the class automatically make it an `inline` function
   (in the compiler's eyes)?

**Advanced**
6. Write a class `Time` (hours, minutes) with `setTime()` and `showTime()` defined outside the
   class. Explain why keeping large functions outside the class is a better practice.

### 6. Static data members and static member functions

**Basic**
1. What is a static data member?
2. What is a static member function?
3. Can a static member function access a normal (non-static) data member directly? Why or why not?

**Intermediate**
4. Write a class `Counter` with a static data member `count` that increases by 1 every time an
   object is created. Print the count after creating 3 objects.
5. Where must a static data member be defined/initialized, besides being declared in the class?

**Advanced**
6. Write a program with a class `Employee` that uses a static function `totalEmployees()` to
   return how many `Employee` objects exist, without creating any object to call it.

### 7. Structure, Union, Enumeration and Class

**Basic**
1. What is a `struct`? What is its default access specifier?
2. What is a `union`? How is it different from a `struct` in memory?
3. What is an `enum`? Give one example.
4. Give one difference between `struct` and `class` in C++.

**Intermediate**
5. Write a `struct Student` with `roll` and `marks`, create 2 objects, take input, and print both.
6. Write a small program using `union Data` with an `int` and a `float` member. Print the size of
   the union using `sizeof`.

**Advanced**
7. Write an `enum Day` for the 7 days of the week. Write a program that takes a number (0–6) from
   the user and prints the matching day name.

### 8. Default arguments

**Basic**
1. What is a default argument?
2. Rule: in which direction (left-to-right or right-to-left) must default values be assigned?

**Intermediate**
3. Write a function `interest(float p, float rate = 5.0, int years = 1)` and call it three ways:
   with 1 argument, 2 arguments, and 3 arguments.
4. Is `void f(int a = 1, int b);` a valid function declaration? Explain.

**Advanced**
5. Write a function `area(float l, float b = 0)` that returns `l*l` (square) if `b` is not given,
   and `l*b` (rectangle) if it is given. Test both cases.

### 9. Inline functions

**Basic**
1. What is an inline function? Which keyword is used?
2. Give one advantage and one disadvantage of inline functions.

**Intermediate**
3. Write an inline function `square(int x)` and use it inside `main()`.
4. Why does the compiler usually refuse to inline a function that has a loop or is recursive?

**Advanced**
5. Write an inline function `cube(int x)` and a normal (non-inline) function `factorial(int n)`
   in the same program. Explain in 2 lines why `factorial` is not a good inline candidate.

### 10. Manipulator functions

**Basic**
1. What is a manipulator? Name two manipulators you have used.
2. Which header file do `setw` and `setprecision` need?

**Intermediate**
3. Write a program that prints a number with exactly 2 digits after the decimal point using
   `setprecision`.
4. Write a program that prints three names in a neat column using `setw`.

**Advanced**
5. Write a program that prints a bill (item name and price) for 3 items, using `setw` to align
   the item names and prices in two neat columns.

### 11. Function overloading and scope rules

**Basic**
1. What is function overloading?
2. Can two overloaded functions differ only in return type? Why or why not?
3. What is scope resolution operator `::` used for?

**Intermediate**
4. Write an overloaded function `add()` that works for two `int`s, two `float`s, and three `int`s.
5. A global variable `x` and a local variable `x` have the same name. How do you access the
   global `x` inside the function?

**Advanced**
6. Write a program with an overloaded function `volume()` for a cube (1 argument), a rectangular
   box (3 arguments) and a cylinder (2 arguments, radius and height).

### 12. Friend function and friend class

**Basic**
1. What is a friend function?
2. Is a friend function a member of the class? Where is it declared and where is it defined?
3. What is a friend class?

**Intermediate**
4. Write a class `Box` with a private data member `volume`. Write a friend function
   `printVolume()` that accesses and prints it.
5. Give one situation where a friend function is genuinely useful (e.g. operating on two classes).

**Advanced**
6. Write two classes `Rectangle` and `Circle`. Write one friend function `compareArea()` that
   takes an object of each class and prints which one has the bigger area.

---

## Unit 2

### 13. Pointers — basics, void pointer, pointer arithmetic

**Basic**
1. What is a pointer? How do you declare a pointer to an `int`?
2. What do `&` and `*` mean when used with pointers?
3. What is a `void` pointer? Can it be dereferenced directly?

**Intermediate**
4. Write a program that stores the address of an `int` variable in a pointer and prints both the
   value and the address.
5. If `p` is an `int*` pointing to an array, what does `p++` do — move by 1 byte or by
   `sizeof(int)` bytes?

**Advanced**
6. Write a program that uses pointer arithmetic (`*(p+i)`) to print all elements of an `int`
   array, instead of using array indexing `a[i]`.

### 14. Pointer to pointer, dangling pointer, wild pointer, null pointer

**Basic**
1. What is a pointer to a pointer? How do you declare one (`int **pp`)?
2. What is a dangling pointer?
3. What is a wild pointer? How is it different from a dangling pointer?
4. What is a null pointer? How do you assign it in modern C++?

**Intermediate**
5. Write a small program that declares `int x = 10, *p = &x, **pp = &p;` and prints `x` using
   both `*p` and `**pp`.
6. Write an example (in comments/pseudocode is fine) of code that creates a dangling pointer using
   `new` and `delete`.

**Advanced**
7. Explain with a short program why checking `if (p != nullptr)` before using a pointer is good
   practice.

### 15. Classes containing pointers, pointer to objects, `this` pointer

**Basic**
1. What does it mean for a class to "contain a pointer" as a data member?
2. What is the `this` pointer? What does it point to?
3. How do you access a member through a pointer to an object — `.` or `->`?

**Intermediate**
4. Write a class `Point` (x, y). Create an object, then a pointer to that object, and call
   `show()` through the pointer using `->`.
5. Write a `setX(int x)` function that uses `this->x = x;` to tell apart the parameter and the
   data member which have the same name.

**Advanced**
6. Write a class `Node` that has an `int data` and a pointer to another `Node` (`Node* next`).
   Create two `Node` objects and link the first one's `next` to the second one.

### 16. Array of objects, multidimensional arrays (in `main` and inside a class)

**Basic**
1. How do you declare an array of 5 objects of a class `Student`?
2. How do you declare a 2-D array of size 3×3 of `int` in `main()`?

**Intermediate**
3. Write a program with an array of 3 `Student` objects (name, marks); take input for all and
   print the topper.
4. Write a program that declares a `3x3` 2-D array inside `main()`, fills it with numbers, and
   prints it like a matrix.

**Advanced**
5. Write a class `Matrix` that stores a `3x3` 2-D array **as a data member**, with a function to
   take input and a function to print the matrix.

### 17. The Standard C++ `string` class

**Basic**
1. Which header file is needed to use the C++ `string` class?
2. Give two advantages of `string` over a C-style character array (`char[]`).
3. How do you find the length of a `string` object?

**Intermediate**
4. Write a program that takes a full name using `string` and `getline()`, and prints its length.
5. Name any four member functions of the `string` class (other than `length()`).

**Advanced**
6. Write a program that takes a sentence as a `string` and counts how many times the letter `'a'`
   appears in it.

### 18. Member functions and modifiers of the `string` class

**Basic**
1. What does `s.length()` (or `s.size()`) return?
2. What does `s.substr(pos, len)` do?
3. What does `s.find("text")` return if the text is not found?

**Intermediate**
4. Write a program using `append()` to join two strings.
5. Write a program using `insert()` and `erase()` on a `string`.

**Advanced**
6. Write a program that takes a sentence, and using `string` member functions, converts it to
   uppercase and prints the reversed string too.

### 19. Difference between pointer and reference variables

**Basic**
1. What is a reference variable? How do you declare one?
2. Give two differences between a pointer and a reference.
3. Can a reference be `nullptr`? Can a pointer?

**Intermediate**
4. Write a `swap()` function using reference parameters (`int &a, int &b`) and one using pointer
   parameters (`int *a, int *b`). Compare how they are called in `main()`.

**Advanced**
5. Explain, with a short example, why a reference must be initialized at the time of declaration
   but a pointer does not have to be.

### 20. Pointer to a data member

**Basic**
1. What is a "pointer to data member" in C++?
2. How is a pointer to a data member declared — give the general syntax
   `Type ClassName::*ptr`.

**Intermediate**
3. Write a class `Item` with a public `int price`. Declare a pointer to this data member and use
   it, through an object, to read and change `price`.

**Advanced**
4. Explain in 2–3 lines why a pointer to a data member is different from a normal pointer — what
   extra information (the class) does it need to make sense?

---

## Unit 3

### 21. Opening and closing files, modes of file

**Basic**
1. Which header file is needed for file handling? Name the three file stream classes it gives.
2. What are the two ways to open a file?
3. Why should a file be closed with `close()`?

**Intermediate**
4. Write a program that opens a file `test.txt` for reading and prints "File not found" if it
   could not be opened.
5. What is the difference between `ios::out` and `ios::app`? What happens to old data in each?

**Advanced**
6. Write a program that writes 2 lines to `log.txt` using `ios::out`, then opens it again in
   `ios::app` mode, adds 1 more line, and finally reads and prints all 3 lines.

### 22. File stream functions, reading and writing files

**Basic**
1. What is the difference between reading with `fin >> s` and `getline(fin, s)`?
2. What do `get()` and `put()` do?
3. What does `eof()` return?

**Intermediate**
4. Write a program that writes 5 numbers to a file, then reads them back and prints their sum.
5. Write a program that counts the number of characters in a file using `get()`.

**Advanced**
6. Write a program that copies the contents of one text file into another file, line by line.

### 23. Sequential access and random access

**Basic**
1. What is the difference between sequential access and random access?
2. What do `seekg()`, `seekp()`, `tellg()` and `tellp()` do?
3. What do `ios::beg`, `ios::cur` and `ios::end` mean?

**Intermediate**
4. Write a program that finds the size of a file using `seekg()` and `tellg()`.
5. A file has `ABCDEFGHIJ`. Which character is read after `seekg(-2, ios::end)`?

**Advanced**
6. Write a program that opens a file with `fstream` in `ios::in | ios::out` mode, replaces the
   5th character with `'*'` using `seekp()`, and prints the whole file again.

### 24. Binary file operations

**Basic**
1. What is a binary file? How is it different from a text file?
2. Which mode is used to open a file in binary form?
3. Write the general syntax of `write()` and `read()`.

**Intermediate**
4. Why is the address typecast to `(char*)` in `write()` and `read()`?
5. Write a program that writes an array of 5 `int`s to a binary file and reads them back.

**Advanced**
6. Write a program that writes 10 numbers to a binary file and then reads **only the 7th number**
   using `seekg()`, without reading the first 6.

### 25. Classes, structures and file operations

**Basic**
1. How do you write one whole structure variable to a binary file in one statement?
2. Why should text inside a record be stored as a `char` array and not a `string`?

**Intermediate**
3. Write a `struct Student` (roll, name, marks). Write 3 records to a binary file and read them all
   back using a `while (fin.read(...))` loop.
4. How can you find the number of records in a binary file?

**Advanced**
5. Write a class `Account` (account number, name, balance) with functions to write objects to a
   file and to search an account by its number from the file and print its details.

### 26. Manager functions, default constructor, constructor with default arguments

**Basic**
1. What are manager functions? Name them.
2. What is a constructor? Write any three of its features.
3. What is a default constructor? When does the compiler create one by itself?

**Intermediate**
4. Write a class `Box` with a constructor with default arguments `Box(int l = 1, int w = 1)`.
   Create objects with 0, 1 and 2 values.
5. Why do `A()` and `A(int x = 0)` together in one class cause an error for `A obj;`?

**Advanced**
6. Write a class `Time` with a constructor that has default arguments for hours, minutes and
   seconds (all 0). Create 3 objects using different numbers of values and print each time.

### 27. Parameterized constructor

**Basic**
1. What is a parameterized constructor?
2. Write the implicit and explicit ways of calling a parameterized constructor.

**Intermediate**
3. Write a class `Rectangle` with a parameterized constructor and a function `area()`.
4. If a class has only a parameterized constructor, why does `Rectangle r;` give an error?

**Advanced**
5. Write a class `Complex` with overloaded constructors (no arguments, one argument, two
   arguments) and a function to add two `Complex` objects.

### 28. Copy constructor

**Basic**
1. What is a copy constructor? Write its general syntax.
2. Write any three situations in which the copy constructor is called.

**Intermediate**
3. Why must the parameter of a copy constructor be a reference?
4. What is the difference between a shallow copy and a deep copy?

**Advanced**
5. Write a class with an `int*` data member and a copy constructor that does a **deep copy**.
   Show that changing the copy does not change the original object.

### 29. Destructors

**Basic**
1. What is a destructor? How is it named?
2. Can a destructor take arguments? Can it be overloaded?

**Intermediate**
3. Write a program to show that objects are destroyed in the reverse order of their creation.
4. When is the destructor of an object created with `new` called?

**Advanced**
5. Write a class `FileLogger` that opens a file in its constructor, has a function to write a
   message, and closes the file in its destructor.

### 30. Initializer lists

**Basic**
1. What is an initializer list? Write its syntax.
2. Which data members must be initialized using an initializer list?

**Intermediate**
3. Write a class `Point` that uses an initializer list to set `x` and `y`.
4. In which order are members initialized — the order in the list or the order of declaration?

**Advanced**
5. Write a class `Student` with a `const int roll` and a reference member `int &marks`, and
   initialize both using an initializer list.

---

# Answers

## Unit 1

1. Procedural: step-by-step functions acting on data (e.g. C). OOP: data and functions bundled
   into objects (e.g. C++, Java). OOP features: encapsulation, abstraction, inheritance,
   polymorphism. Difference: procedural has no data hiding and code reuse is hard (no
   inheritance); OOP has both.
2. Class = blueprint/template. Object = actual variable of that class type, occupying memory.
   Encapsulation = wrapping data + functions together, hiding data using `private`. Abstraction =
   showing only necessary details, hiding internal working. Inheritance = a class acquiring
   properties of another class. Polymorphism = same function name behaving differently
   (overloading/overriding). `private` in a class demonstrates **encapsulation**.
3. `<iostream>`. `cin >>` reads input from keyboard into a variable. `cout <<` prints output to
   the screen. `endl` moves the cursor to a new line (also flushes the output buffer).
4. Data member = a variable inside a class. Member function = a function inside a class. Object
   is created as `ClassName obj;`. Default access specifier of a class is `private`
   (for `struct` it is `public`).
5. Inline member function is written with its body inside the class. Non-inline (outer) is
   declared inside the class but defined outside using `ReturnType ClassName::function(){ }`.
   Writing a function inside the class only *requests* inlining — the compiler decides.
6. Static data member is shared by all objects of the class (one copy for the whole class).
   Static member function can be called using the class name, without any object, and it can only
   access other static members directly (no `this` pointer). It must also be defined once outside
   the class: `int ClassName::staticVar = 0;`.
7. `struct`: default access `public`. `union`: all members share the same memory, so its size is
   the size of its biggest member, and only one member holds a valid value at a time. `enum`: a
   set of named integer constants, e.g. `enum Day {SUN, MON, TUE};`. Struct vs class: default
   access is `public` in struct, `private` in class (otherwise they work almost the same in C++).
8. Default argument = a value already given in the function definition, used if the caller does
   not supply that argument. Rule: default values are assigned **right to left**, so
   `void f(int a = 1, int b);` is **invalid** (a non-default parameter cannot come after a default
   one).
9. Inline function: written with the `inline` keyword; the compiler copies its code at the call
   site instead of making a function call. Advantage: saves function-call overhead (faster for
   small functions). Disadvantage: increases program size if used for big functions. Compiler
   refuses loops/recursion because the code cannot be usefully "copied in place".
10. Manipulator: a function-like tool that changes how output is formatted, e.g. `setw`,
    `setprecision`, `endl`. `setw` and `setprecision` need `<iomanip>`.
11. Function overloading = same function name, different parameter list, in the same scope.
    Return type alone cannot distinguish two overloaded functions — the compiler must be able to
    tell them apart just from the call, and return type is not visible at the call. `::` is the
    scope resolution operator — used to define a member function outside the class and to access a
    global variable when a local one has the same name (`::x`).
12. Friend function: a non-member function given permission to access the class's private data,
    declared inside the class with the `friend` keyword but defined outside like a normal
    function. Friend class: a whole class given the same permission. Not a member, so it is not
    called with `.` or `->`, and it has no `this` pointer.

## Unit 2

13. Pointer: a variable that stores the address of another variable, declared as `int *p;`.
    `&` = address-of operator, `*` = dereference operator (gets the value at an address). `void*`
    = a generic pointer that can hold the address of any type, but it must be typecast before
    dereferencing. Pointer arithmetic on `p++` moves by `sizeof(datatype)` bytes, not 1 byte.
14. Pointer to pointer: a pointer that stores the address of another pointer, `int **pp;`.
    Dangling pointer: points to memory that has already been freed/deleted. Wild pointer: a
    pointer that is declared but never initialized, so it points to a random/garbage address.
    Null pointer: a pointer that points to nothing, assigned in modern C++ using `nullptr`.
15. A class "contains a pointer" when one of its data members is a pointer type. `this` is a
    hidden pointer available inside every member function, pointing to the object that called the
    function. Through a pointer to an object you access members using `->` (`.` is used through
    the object itself, not a pointer to it).
16. Array of objects: `Student s[5];`. 2-D array in `main()`: `int a[3][3];`.
17. `<string>` header. Advantages of `string` over `char[]`: no fixed size limit (it grows
    automatically), and it has built-in member functions (`length()`, `substr()`, `find()`, etc.)
    instead of separate C library functions. Length is found using `s.length()` or `s.size()`.
18. `length()`/`size()` return the number of characters in the string. `substr(pos, len)` returns
    a part of the string starting at `pos` for `len` characters. `find()` returns the special
    value `string::npos` if the text is not found.
19. Reference: an alias (another name) for an existing variable, declared as `int &ref = x;`.
    Differences: a reference must be initialized when declared and cannot be changed to refer to
    another variable later; a pointer can be declared without initializing and can be reassigned.
    A reference can never be `nullptr`; a pointer can be `nullptr`.
20. Pointer to a data member: a pointer that stores the *offset/location* of a member inside a
    class, not a fixed memory address — it only makes sense combined with an actual object.
    Declared as `Type ClassName::*ptr = &ClassName::member;`. It needs the class name because the
    same member exists at a different address in every object; the pointer only tells you *which*
    member, an object tells you *whose*.

## Unit 3

21. Header `<fstream>`. Classes: `ofstream` (write), `ifstream` (read), `fstream` (both). Two ways
    to open: using the constructor `ofstream f("a.txt");` or using `f.open("a.txt");`. `close()`
    saves all data to the disk and frees the file. Check opening with `if (!f)` or
    `f.is_open()`. `ios::out` erases old data and writes from the start; `ios::app` keeps old data
    and always writes at the end.
22. `fin >> s` reads only one word (stops at a space/new line); `getline(fin, s)` reads a full line
    with spaces. `get(ch)` reads one character (spaces too), `put(ch)` writes one character.
    `eof()` returns true (1) when the end of the file has been reached. Safe reading loop:
    `while (getline(fin, line))` or `while (fin.get(ch))`.
23. Sequential access reads the file in order from start to end; random access jumps directly to
    any position. `seekg()`/`seekp()` move the get (read) / put (write) pointer; `tellg()`/`tellp()`
    tell their current position. `ios::beg` = from the beginning, `ios::cur` = from the current
    position, `ios::end` = from the end. File size: `seekg(0, ios::end);` then `tellg()`. For
    `ABCDEFGHIJ`, `seekg(-2, ios::end)` reads `I`.
24. A binary file stores data as raw bytes exactly as in memory (a text file stores readable
    characters). Open with `ios::binary`. Syntax: `fout.write((char*)&x, sizeof(x));` and
    `fin.read((char*)&x, sizeof(x));`. The `(char*)` cast is needed because these functions work
    on bytes and take a `char*`. Item `n` (from 0) is at byte `n * sizeof(item)`, so
    `seekg(6 * sizeof(int))` jumps to the 7th `int`.
25. Whole struct/object: `fout.write((char*)&s, sizeof(s));`. Use a `char` array for text, because
    a `string` stores only a pointer to its letters, so its raw bytes do not contain the actual
    text. Read all records with `while (fin.read((char*)&s, sizeof(s)))`. Number of records =
    file size ÷ `sizeof(record)`.
26. Manager functions = functions that manage an object's life: constructors (default,
    parameterized, copy) and the destructor. Constructor: same name as the class, no return type,
    called automatically when an object is created, can be overloaded. Default constructor = one
    that can be called with no arguments; the compiler makes one only if the class has **no**
    constructor at all. `A()` and `A(int x = 0)` together make `A obj;` **ambiguous** (both can be
    called with no value), so it is a compile error.
27. Parameterized constructor = a constructor that takes arguments, so each object can start with
    different values. Implicit call: `Rectangle r(4, 5);` Explicit call:
    `Rectangle r = Rectangle(4, 5);`. If only a parameterized constructor is written, the compiler
    does not make a default constructor, so `Rectangle r;` has no matching constructor → error.
28. Copy constructor creates a new object as a copy of an existing one:
    `ClassName(const ClassName &obj)`. Called when: `B b(a);`, `B c = a;`, passing an object by value, returning an
    object by value. The parameter must be a reference, otherwise passing it by value would call
    the copy constructor again and again (infinite recursion). Shallow copy copies pointer
    addresses (both objects share the same memory); deep copy gives the copy its own new memory
    with the same value.
29. Destructor: special member function `~ClassName()`, called automatically when an object is
    destroyed, used for clean-up (free memory, close files). It takes no arguments, has no return
    type, and cannot be overloaded (only one per class). Local objects are destroyed in the
    reverse order of creation. For an object made with `new`, the destructor runs only when
    `delete` is used.
30. Initializer list: written after `:` in a constructor, e.g. `Point(int a, int b) : x(a), y(b) { }`.
    Must be used for `const` members, reference members, and member objects with no default
    constructor. Members are always initialized in the order they are **declared in the class**,
    not the order written in the list.
