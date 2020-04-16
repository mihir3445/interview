<div align="center">
📖 Github
&emsp;&emsp; | &emsp;&emsp;
<a href="https://interview.huihut.com">📚 Docsify</a>
</div> 
<br>

<b><details><summary>💡 关于</summary></b>

📚 This warehouse is a summary of basic knowledge for job seekers and beginners in C / C ++ technology direction, including language, library, data structure, algorithm, system, network, link loading library and other knowledge and interview experience, recruitment, internal promotion And other information.

💡 Side directory support methods: [📚 Docsify documentation] (https://interview.huihut.com), [Github + TOC navigation] (https://github.com/jawil/GayHub) ([TOC preview.png] (https://raw.githubusercontent.com/huihut/interview/master/images/TOC preview.png))

📄 Save as PDF: Use the Chrome browser to open the <a href="https://interview.huihut.com"> 📚 Docsify document </a> page, shrink the left directory-right click-print-select the target printer is Save as PDF-Save ([Print Preview.png] (https://raw.githubusercontent.com/huihut/interview/master/images/Print Preview.png))

🙏 If there are any errors or improvements in the contents of the warehouse, issues or pr are welcome. Suggestions or discussions can be submitted at [# 12] (https://github.com/huihut/interview/issues/12). Due to my limited level, the knowledge points in the warehouse are from my original, reading notes, books, blog posts, etc. Non-original has been marked with the source, if there is any omission, please issue an issue. This warehouse follows the [CC BY-NC-SA 4.0 (signed-non-commercial use-shared in the same way)] (LICENSE) agreement, please indicate the source for the reprint, and may not be used for commercial purposes.

</ details>


## 📑 Directory

* [➕ C / C ++] (#-cc)
* [⭐️ Effective] (# ️-effective)
* [📦 STL] (#-stl)
* [〽️ Data Structure] (# ️-Data Structure)
* [⚡️ Algorithm] (# ️-Algorithm)
* [❓ Problems] (#-problems)
* [💻 Operating System] (# -operating system)
* [☁️ Computer Network] (# ️-Computer Network)
* [🌩 Network Programming] (# -Network Programming)
* [💾 Database] (#-Database)
* [📏 Design Mode] (# -Design Mode)
* [⚙️ Link loading library] (# ️-Link loading library)
* [📚 Books] (#-书)
* [🔱 C / C ++ development direction] (# -cc-development direction)
* [💯 Review brush questions website] (# -review brush questions website)
* [📝 Interview Question Experience] (# -Interview Question Experience)
* [📆 Recruitment Time Post] (# -Recruitment Time Post)
* [👍 内 推] (#-内 推)
* [👬 Contributor] (# -Contributor)
* [🍭 Support Sponsor] (# -Support Sponsor)
* [📜 License] (#-license)

## ➕ C / C ++

### const

#### Role

1. Modify the variable, indicating that the variable cannot be changed;
2. Modified pointers are divided into pointers to const and pointers that are constants (const pointers)
3. Modified references, references to const (reference to const), used for formal parameter types, which avoids copying, and avoids modification of values ​​by functions;
4. Modify the member function, indicating that the member variable cannot be modified in the member function.

#### const pointers and references

* Pointer
    * Pointer to const (pointer to const)
    * It is a constant pointer (const pointer)
* Quote
    * Reference to const (reference to const)
    * There is no const reference, because the reference itself is a const pointer

> (It can be imagined for the sake of memory) The value modified by const (behind const) cannot be changed, as shown in the following example using `p2`,` p3`

#### Use

const use

```cpp
// class
class A
{
private:
    const int a; // constant object member, can only be assigned in the initialization list

public:
    // Constructor
    A (): a (0) {};
    A (int x): a (x) {}; // initialization list

    // const can be used to distinguish overloaded functions
    int getValue (); // Ordinary member function
    int getValue () const; // Constant member function, must not modify the value of any data member in the class
};

void function ()
{
    // object
    A b; // Ordinary objects, you can call all member functions and update constant member variables
    const A a; // Constant object, can only call constant member function
    const A * p = & a; // Pointer variable, pointing to constant object
    const A & q = a; // reference to constant object

    // pointer
    char greeting [] = "Hello";
    char * p1 = greeting; // pointer variable, pointing to character array variable
    const char * p2 = greeting; // Pointer variable, pointing to the character array constant (const followed by char, indicating that the character pointed to (char) cannot be changed)
    char * const p3 = greeting; // itself is a constant pointer to a character array variable (const is followed by p3, indicating that the p3 pointer itself cannot be changed)
    const char * const p4 = greeting; // Pointer to a constant itself, pointing to a character array constant
}

// function
void function1 (const int Var); // The passed parameters are immutable in the function
void function2 (const char * Var); // The content pointed by the parameter pointer is a constant
void function3 (char * const Var); // parameter pointer is constant
void function4 (const int & Var); // The reference parameter is constant in the function

// Function return value
const int function5 (); // returns a constant
const int * function6 (); // Return a pointer variable pointing to a constant, use: const int * p = function6 ();
int * const function7 (); // returns a constant pointer to a variable, use: int * const p = function7 ();
```

### static

#### Role

1. Modify the ordinary variable, modify the storage area and life cycle of the variable, so that the variable is stored in the static area, the space is allocated before the main function runs, if there is an initial value, initialize it with the initial value, if there is no initial value, the system uses the default Value to initialize it.
2. Modify the ordinary function, indicating that the scope of the function can only be used in the file that defines the function. When developing a project with multiple people, in order to prevent the function from being renamed in the namespace of others, the function can be positioned as static.
3. Modify the member variable. Modify the member variable so that all objects only save one variable, and the member can be accessed without generating an object.
4. Decorate the member function. Decorate the member function so that the function can be accessed without generating an object, but non-static members cannot be accessed within the static function.

### this pointer

1. The `this` pointer is a special pointer implicit in each non-static member function. It points to the object that called the member function.
2. When calling a member function on an object, the compiler first assigns the address of the object to the `this` pointer, and then calls the member function. Each time the member function accesses a data member, the` this` pointer is used implicitly.
3. When a member function is called, an implicit parameter is automatically passed to it, which is a pointer to the object where the member function is located.
4. The `this` pointer is implicitly declared as:` ClassName * const this`, which means that the `this` pointer cannot be assigned; in the` const` member function of the `ClassName` class, the type of` this` pointer It is: `const ClassName * const`, which means that the object pointed to by` this` pointer cannot be modified (that is, the data member of this object cannot be assigned)
5. `this` is not a regular variable, but an rvalue, so you cannot get the address of` this` (cannot be `& this`).
6. In the following scenarios, it is often necessary to explicitly reference the `this` pointer:
    1. Chained references for implementing objects;
    2. In order to avoid assignment operations on the same object;
    3. When implementing some data structures, such as `list`.

### inline function

#### Features

* Equivalent to writing the content in the inline function where the inline function is called;
* Equivalent to directly executing the function body without executing the step of entering the function;
* Equivalent to macros, but more type checking than macros, and really have functional characteristics;
* Compilers generally do not inline inline functions that include complex operations such as loops, recursion, and switches;
* Functions defined in class declarations, except for virtual functions, are automatically implicitly treated as inline functions.

#### Use

inline use

```cpp
// Statement 1 (add inline, recommended)
inline int functionName (int first, int second, ...);

// Statement 2 (without inline)
int functionName (int first, int second, ...);

// definition
inline int functionName (int first, int second, ...) {/ **** /};

// Defined within the class, implicitly inline
class A {
    int doA () {return 0;} // implicit inlining
}

// Out-of-class definition, need to be explicitly inline
class A {
    int doA ();
}
inline int A :: doA () {return 0;} // requires explicit inlining
```

#### Compiler processing steps for inline functions

1. Copy the inline function body to the inline function call point;
2. Allocate memory space for the local variables in the used inline function;
3. Map the input parameters and return values ​​of the inline function into the local variable space of the calling method;
4. If the inline function has multiple return points, turn it into a branch at the end of the inline function code block (using GOTO).

#### Pros and cons

advantage

1. Inline functions, like macro functions, will expand the code at the called site, eliminating the need for parameter push stacking, stack frame development and recycling, and result return, thereby increasing the speed of the program.
2. Compared with macro functions, inline functions will perform security checks or automatic type conversion when the code is expanded (same as ordinary functions), but macro definitions will not.
3. The member functions declared at the same time in the class are automatically converted into inline functions, so inline functions can access the member variables of the class, but macro definitions cannot.
4. Inline functions can be debugged at runtime, but macro definitions are not.

Disadvantages

1. Code expansion. Inlining comes at the cost of code expansion (copying) and eliminates the overhead caused by function calls. If the time to execute the code in the function body is greater than the cost of the function call, then the gain in efficiency will be very little. On the other hand, every call to an inline function must copy code, which will increase the total code size of the program and consume more memory space.
2. The inline function cannot be upgraded with the function library upgrade. Inline function changes need to be recompiled, unlike non-inline which can be linked directly.
3. Whether it is inline or not, the programmer cannot control it. Inlining functions is only a recommendation to the compiler. Whether to inline the function is up to the compiler.

#### Can a virtual function be an inline function?

> [Are "inline virtual" member functions ever actually "inlined"?] (Http://www.cs.technion.ac.il/users/yechiel/c++-faq/inline-virtuals.html)

* A virtual function can be an inline function. Inline can modify a virtual function, but it cannot be inlined when the virtual function exhibits polymorphism.
* Inlining is recommended by the compiler when the compiler is inline, and the polymorphism of the virtual function is at runtime. The compiler cannot know which code is called at runtime. Therefore, when the virtual function is polymorphic (runtime), it cannot be inlined. .
* The only time when `inline virtual` can be inlined is: the compiler knows which class the object is called (eg` Base :: who () `), only if the compiler has a real object and not a pointer or reference to the object Only happens.

Virtual function inline use

```cpp
#include <iostream>
using namespace std;
class Base
{
public:
inline virtual void who ()
{
cout << "I am Base \ n";
}
virtual ~ Base () {}
};
class Derived: public Base
{
public:
inline void who () // implicit inlining when not writing inline
{
cout << "I am Derived \ n";
}
};

int main ()
{
// The virtual function who () here is called by the specific object (b) of the class (Base), which can be determined during compilation, so it can be inlined, but whether it is ultimately inlined depends on compilation Device.
Base b;
b.who ();

// The virtual function here is called by a pointer, showing polymorphism, which needs to be determined during runtime, so it cannot be inline.
Base * ptr = new Derived ();
ptr-> who ();

// Because Base has a virtual destructor (virtual ~ Base () {}), when deleting, it will first call the Derived destructor and then the Base destructor to prevent memory leakage.
delete ptr;
ptr = nullptr;

system ("pause");
return 0;
}
```
### volatile

```cpp
volatile int i = 10;
```

* The volatile keyword is a type modifier. The type variable declared with it means that it can be changed by certain factors unknown to the compiler (operating system, hardware, other threads, etc.). So using volatile tells the compiler not to optimize such objects.
* Variables declared by the volatile keyword must be fetched from memory each time they are accessed (variables that are not modified by volatile may be fetched from CPU registers due to compiler optimization)
* const can be volatile (such as read-only status register)
* Pointer can be volatile

### assert ()

Assertions are macros, not functions. The prototype of the assert macro is defined in `<assert.h>` (C), `<cassert>` (C ++), and its function is to terminate program execution if its condition returns an error. You can turn off assert by defining `NDEBUG`, but at the beginning of the source code, before` include <assert.h> `.

assert () uses

```cpp
#define NDEBUG // With this line, assert is not available
#include <assert.h>

assert (p! = NULL); // assert is not available
```

### sizeof ()

* sizeof array, get the size of the entire array.
* sizeof pointer, get the size of the pointer itself.

### #pragma pack (n)

Set structure, union and class member variables to be aligned in n bytes

#pragma pack (n) use

```cpp
#pragma pack (push) // Save alignment state
#pragma pack (4) // set to 4 byte alignment

struct test
{
    char m1;
    double m4;
    int m3;
};

#pragma pack (pop) // Restore alignment state
```

### Bit field

```cpp
Bit mode: 2; // mode takes 2 bits
```

Classes can define their (non-static) data members as bit-fields, which contain a certain number of binary bits in a bit-field. When a program needs to transfer binary data to other programs or hardware devices, the bit field is usually used.

* The layout of the bit field in the memory is related to the machine
* The type of the bit field must be an integer or enumerated type, the behavior of the bit field in the signed type will depend on the specific implementation
* The address operator (&) cannot be applied to the bit field, any pointer cannot point to the bit field of the class

### extern "C"

* The function or variable restricted by extern is of type extern
* Variables and functions modified by `extern" C "` are compiled and linked in C language

The role of `extern" C "` is to allow the C ++ compiler to treat the code declared by `extern" C "` as C language code, which can avoid the problem that C ++ code cannot be linked with symbols in the C language library due to symbol modification .

extern "C" use

`` `cpp
#ifdef __cplusplus
extern "C" {
#endif

void * memset (void *, int, size_t);

#ifdef __cplusplus
}
#endif
`` `

### struct and typedef struct

#### C

`` `c
// c
typedef struct Student {
    int age;
} S;
`` `

Equivalent to

`` `c
// c
struct Student {
    int age;
};

typedef struct Student S;
`` `

In this case, `S` is equivalent to` struct Student`, but the two identifier namespaces are different.

You can also define `void Student () {}` that does not conflict with `struct Student`.

#### C ++

Due to the change in the rules (search rules) for locating symbols by the compiler, it is different from the C language.

1. If `struct Student {...};` is defined in the class identifier space, when `Student me;` is used, the compiler will search the global identifier table. If `Student` is not found, it is within the class identifier search for.

That is, you can use `Student` or` struct Student`, as follows:

```cpp
// cpp
struct Student {
    int age;
};

void f (Student me); // Correct, "struct" keyword can be omitted
```

2. If a function with the same name as `Student` is defined,` Student` only represents the function, not the structure, as follows:

```cpp
typedef struct Student {
    int age;
} S;

void Student () {} // Correct, after definition "Student" only represents this function

// void S () {} // Error, the symbol "S" has been defined as an alias of "struct Student"

int main () {
    Student ();
    struct Student me; // or "S me";
    return 0;
}
```

### C ++ struct and class

In general, struct is more suitable as an implementation of a data structure, and class is more suitable as an implementation of an object.

#### the difference

* The most essential difference is the default access control
    1. Default inherited access rights. The struct is public and the class is private.
    2. struct as the realization body of the data structure, its default data access control is public, and class as the realization body of the object, its default member variable access control is private.

### union union

Union is a special class that saves space. A union can have multiple data members, but only one data member can have a value at any time. When a member is assigned, other members become undefined. The joint has the following characteristics:

* The default access control character is public
* May contain constructor, destructor
* Cannot contain members of reference type
* Cannot inherit from other classes and cannot be used as base class
* Cannot contain virtual functions
* Anonymous union can directly access union members in the scope of definition
* Anonymous union cannot contain protected members or private members
* Global anonymous union must be static

union use

`` `cpp
#include <iostream>

union UnionTest {
    UnionTest (): i (10) {};
    int i;
    double d;
};

static union {
    int i;
    double d;
};

int main () {
    UnionTest u;

    union {
        int i;
        double d;
    };

    std :: cout << u.i << std :: endl; // output UnionTest 10

    :: i = 20;
    std :: cout << :: i << std :: endl; // output the global static anonymous union 20

    i = 30;
    std :: cout << i << std :: endl; // output local anonymous union 30

    return 0;
}
`` `

### C implements C ++ classes

C implements the object-oriented features of C ++ (encapsulation, inheritance, polymorphism)

* Encapsulation: Use function pointers to encapsulate attributes and methods into structures
* Inheritance: structure nesting
* Polymorphism: the function pointers of the parent and child methods are different

> [Can you write object-oriented code in C? [Closed]] (https://stackoverflow.com/a/351745)

### explicit (explicit) keywords

* Explicit modification of the constructor can prevent implicit conversion and copy initialization
* When explicit conversion function is modified, implicit conversion can be prevented, except [Conversion by Context] (https://zh.cppreference.com/w/cpp/language/implicit_conversion)

explicit use

```cpp
struct A
{
A (int) {}
operator bool () const {return true;}
};

struct B
{
explicit B (int) {}
explicit operator bool () const {return true;}
};

void doA (A a) {}

void doB (B b) {}

int main ()
{
A a1 (1); // OK: direct initialization
A a2 = 1; // OK: copy initialization
A a3 {1}; // OK: direct list initialization
A a4 = {1}; // OK: initialization of the copy list
A a5 = (A) 1; // OK: Allow explicit conversion of static_cast
doA (1); // OK: Allow implicit conversion from int to A
if (a1); // OK: implicit conversion from A to bool using conversion function A :: operator bool ()
bool a6 (a1); // OK: implicit conversion from A to bool using conversion function A :: operator bool ()
bool a7 = a1; // OK: implicit conversion from A to bool using conversion function A :: operator bool ()
bool a8 = static_cast <bool> (a1); // OK: direct initialization of static_cast

B b1 (1); // OK: direct initialization
B b2 = 1; // Error: Objects whose constructor is explicitly modified cannot be copied and initialized
B b3 {1}; // OK: direct list initialization
B b4 = {1}; // Error: Objects whose constructors are explicitly decorated cannot be copied list initialization
B b5 = (B) 1; // OK: Allow explicit conversion of static_cast
doB (1); // Error: The object whose constructor is explicitly modified cannot be implicitly converted from int to B
if (b1); // OK: the object modified by the explicit conversion function B :: operator bool () can be converted from B to bool in context
bool b6 (b1); // OK: the conversion function B :: operator bool () is explicitly modified to be contextually convertible from B to bool
bool b7 = b1; // Error: the object modified by the explicit conversion function B :: operator bool () cannot be implicitly converted
bool b8 = static_cast <bool> (b1); // OK: static_cast for direct initialization

return 0;
}
```

### friend friend class and friend function

* Can access private members
* Destruction of encapsulation
* Friends are not transferable
* Unidirectional relationship
* The form and number of Friends Statement are not limited

### using

#### using statement

A `using statement` statement introduces only one member of the namespace at a time. It allows us to know exactly which name is referenced in the program. Such as:

`` `cpp
using namespace_name :: name;
`` `

#### Using statement of constructor

In C ++ 11, derived classes can reuse the constructors defined by their direct base classes.

`` `cpp
class Derived: Base {
public:
    using Base :: Base;
    / * ... * /
};
`` `

As described in the using statement above, for each constructor of the base class, the compiler generates a derived class constructor corresponding to it (the parameter list is exactly the same). Generate the following type constructor:

`` `cpp
Derived (parms): Base (args) {}
`` `

#### using instructions

The `using directive` makes all names in a particular namespace visible, so we do n’t need to add any prefix qualifiers to them. Such as:

`` `cpp
using namespace_name name;
`` `

#### Minimize the use of `using instructions` to pollute namespaces

> In general, using the using command is safer than using the compiling command because it ** only imports the specified name **. If the name conflicts with the local name, the compiler will ** issue an instruction **. The using compilation command imports all names, including names that may not be needed. If there is a conflict with the local name, the local name will override the namespace version, and the compiler will not issue a warning In addition, the openness of the namespace means that the names of the namespace may be scattered in multiple places, which makes it difficult to know exactly which names are added.

using

Use as few instructions as possible

`` `cpp
using namespace std;
`` `

Should use more `using statement`

`` `cpp
int x;
std :: cin >> x;
std :: cout << x << std :: endl;
`` `

or

`` `cpp
using std :: cin;
using std :: cout;
using std :: endl;
int x;
cin >> x;
cout << x << endl;
`` `

### :: Range resolution operator

#### Category

1. Global scope character (`:: name`): used before the type name (class, class member, member function, variable, etc.), indicating that the scope is the global namespace
2. Class scope character (`class :: name`): used to indicate that the scope of the specified type is specific to a certain class
3. Namespace scope character (`namespace :: name`): used to indicate that the scope of the specified type is specific to a certain namespace

:: Use

`` `cpp
int count = 11; // global (: :) count

class A {
public:
static int count; // class A count (A :: count)
};
int A :: count = 21;

void fun ()
{
int count = 31; // initialize the local count to 31
count = 32; // Set the local count value to 32
}

int main () {
:: count = 12; // Test 1: Set the global count value to 12

A :: count = 22; // Test 2: Set the count of class A to 22

fun (); // Test 3

return 0;
}
`` `

### enum enumeration type

#### Scoped enumerated types

`` `cpp
enum class open_modes {input, output, append};
`` `

#### Unlimited scope enumerated type

`` `cpp
enum color {red, yellow, green};
enum {floatPrec = 6, doublePrec = 10};
`` `

### decltype

The decltype keyword is used to check the declared type or expression type and value classification of an entity. grammar:

`` `cpp
decltype (expression)
`` `

decltype use

`` `cpp
// Tail return allows us to declare the return type after the parameter list
template <typename It>
auto fcn (It beg, It end)-> decltype (* beg)
{
    // Processing sequence
    return * beg; // return a reference to an element in the sequence
}
// In order to use template parameter members, typename must be used
template <typename It>
auto fcn2 (It beg, It end)-> typename remove_reference <decltype (* beg)> :: type
{
    // Processing sequence
    return * beg; // returns a copy of an element in the sequence
}
`` `

### Quote

#### lvalue reference

Conventional references generally indicate the identity of an object.

#### rvalue reference

An rvalue reference is a reference that must be bound to an rvalue (a temporary object, an object to be destroyed), and generally represents the value of the object.

The rvalue reference can realize Move Sementics and Perfect Forwarding. Its main purpose has two aspects:

* Eliminate unnecessary copying of objects when two objects interact, saving computing storage resources and improving efficiency.
* Ability to define generic functions more concisely and clearly.

#### Reference folding

* `X & &`, `X & &&`, `X && &` can be folded into `X &`
* `X && &&` can be folded into `X &&`

### Macro

* The macro definition can achieve a function similar to a function, but it is not a function after all, and the "parameter" in parentheses in the macro definition is not a real parameter. The "parameter" is a one-to-one replacement when the macro is expanded .

### Member initialization list

benefit

* More efficient: one less process of calling the default constructor.
* In some cases, the initialization list must be used:
  1. Constant members, because constants can only be initialized and cannot be assigned, they must be placed in the initialization list
  2. Reference type, the reference must be initialized at the time of definition, and cannot be reassigned, so it must also be written in the initialization list
  3. There is no default constructor class type, because the use of an initialization list eliminates the need to call the default constructor to initialize

### initializer_list list initialization

Initialize an object with a curly brace initializer list, where the corresponding constructor accepts a `std :: initializer_list` parameter.

initializer_list use

`` `cpp
#include <iostream>
#include <vector>
#include <initializer_list>
 
template <class T>
struct S {
    std :: vector <T> v;
    S (std :: initializer_list <T> l): v (l) {
         std :: cout << "constructed with a" << l.size () << "-element list \ n";
    }
    void append (std :: initializer_list <T> l) {
        v.insert (v.end (), l.begin (), l.end ());
    }
    std :: pair <const T *, std :: size_t> c_arr () const {
        return {& v [0], v.size ()}; // Copy list initialization in return statement
                                   // This does not use std :: initializer_list
    }
};
 
template <typename T>
void templated_fn (T) {}
 
int main ()
{
    S <int> s = {1, 2, 3, 4, 5}; // copy initialization
    s.append ({6, 7, 8}); // List initialization in function call
 
    std :: cout << "The vector size is now" << s.c_arr (). second << "ints: \ n";
 
    for (auto n: s.v)
        std :: cout << n << '';
    std :: cout << '\ n';
 
    std :: cout << "Range-for over brace-init-list: \ n";
 
    for (int x: {-1, -2, -3}) // auto rules make this range for work
        std :: cout << x << '';
    std :: cout << '\ n';
 
    auto al = {10, 11, 12}; // special rules for auto
 
    std :: cout << "The list bound to auto has size () =" << al.size () << '\ n';
 
// templated_fn ({1, 2, 3}); // compilation error! "{1, 2, 3}" is not an expression,
                             // It has no type, so T cannot be derived
    templated_fn <std :: initializer_list <int >> ({1, 2, 3}); // OK
    templated_fn <std :: vector <int >> ({1, 2, 3}); // also OK
}
`` `

### Object Oriented

Object-oriented programming (OOP) is a paradigm of programming with object concepts, and it is also an abstract policy for program development.

! [Object Oriented Features] (https://raw.githubusercontent.com/huihut/interview/master/images/Basic Object Oriented Features.png)

Three characteristics of object-oriented-encapsulation, inheritance, polymorphism

### Package

Encapsulate objective things into abstract classes, and the class can operate its own data and methods only by trusted classes or objects, and hide information from untrusted ones. Keywords: public, protected, private. Do not write the default is private.

* `public` members: can be accessed by any entity
* `protected` members: only allowed to be accessed by subclasses and member functions of this class
* `private` members: only allowed to be accessed by member functions, friend classes or friend functions of this class

### Inheritance

* Base class (parent class); derived class (child class)

### polymorphism

* Multi-state, that is, multiple states (forms). In simple terms, we can define polymorphism as the ability to display messages in multiple forms.
* Polymorphism is based on encapsulation and inheritance.
* C ++ polymorphic classification and implementation:
     1. Overload polymorphism (Ad-hoc Polymorphism, compile time): function overloading, operator overloading
     2. Subtype Polymorphism (Runtime): virtual function
     3. Parameter polymorphism (Parametric Polymorphism, compile time): class template, function template
     4. Forced polymorphism (Coercion Polymorphism, compile time / run time): basic type conversion, custom type conversion

> [The Four Polymorphisms in C++](https://catonmat.net/cpp-polymorphism)

#### Static polymorphism (compilation / early binding)

Function overloading

`` `cpp
class A
{
public:
    void do (int a);
    void do (int a, int b);
};
`` `

#### Dynamic polymorphism (runtime / late binding)

* Virtual function: Use virtual to modify member functions to make them virtual functions

**note:**

* Ordinary functions (non-class member functions) cannot be virtual functions
* Static functions (static) cannot be virtual functions
* The constructor cannot be a virtual function (because when calling the constructor, the virtual table pointer is not in the memory space of the object, the virtual table pointer must be formed after the constructor call is completed)
* The inline function cannot be a virtual function when expressing polymorphism. For explanation, see: [Can a virtual function (virtual) be an inline function (inline)? ] (https://github.com/huihut/interview#%E8%99%9A%E5%87%BD%E6%95%B0virtual%E5%8F%AF%E4%BB%A5%E6%98%AF % E5% 86% 85% E8% 81% 94% E5% 87% BD% E6% 95% B0inline% E5% 90% 97)

Dynamic polymorphism usage

`` `cpp
class Shape // shape class
{
public:
    virtual double calcArea ()
    {
        ...
    }
    virtual ~ Shape ();
};
class Circle: public Shape // circle class
{
public:
    virtual double calcArea ();
    ...
};
class Rect: public Shape // rectangle class
{
public:
    virtual double calcArea ();
    ...
};
int main ()
{
    Shape * shape1 = new Circle (4.0);
    Shape * shape2 = new Rect (5.0, 6.0);
    shape1-> calcArea (); // Call the method in the circle class
    shape2-> calcArea (); // Call the method in the rectangle class
    delete shape1;
    shape1 = nullptr;
    delete shape2;
    shape2 = nullptr;
    return 0;
}
`` `

### Virtual destructor

The virtual destructor is to resolve the pointer of the base class to the derived class object, and use the pointer of the base class to delete the derived class object.

Use of virtual destructor

`` `cpp
class Shape
{
public:
    Shape (); // Constructor cannot be a virtual function
    virtual double calcArea ();
    virtual ~ Shape (); // Virtual destructor
};
class Circle: public Shape // circle class
{
public:
    virtual double calcArea ();
    ...
};
int main ()
{
    Shape * shape1 = new Circle (4.0);
    shape1-> calcArea ();
    delete shape1; // Because Shape has a virtual destructor, when delete releases the memory, first call the subclass destructor and then call the base class destructor to prevent memory leaks.
    shape1 = NULL;
    return 0;
}
`` `

### Pure virtual function

A pure virtual function is a special virtual function. In the base class, you cannot give a meaningful implementation of the virtual function, but declare it as a pure virtual function, and its implementation is left to the derived class of the base class.

`` `cpp
virtual int A () = 0;
`` `

### Virtual function, pure virtual function

* If a virtual function is declared in the class, this function is implemented, even if it is empty, its role is to allow this function to be overridden in its subclasses, so that the compiler can use Late binding to achieve polymorphism. A pure virtual function is just an interface, it is just a function declaration, and it has to be implemented in a subclass.
* Virtual functions may not be rewritten in subclasses; but pure virtual functions must be implemented in subclasses before they can be instantiated.
* The virtual function class is used for "implementation inheritance", inheriting the interface also inherits the implementation of the parent class. Pure virtual functions are concerned with the unity of the interface, and the implementation is done by subclasses.
* Classes with pure virtual functions are called abstract classes. Such classes cannot directly generate objects, but can only be used after they are inherited and their virtual functions are rewritten. After the abstract class is inherited, the subclass can continue to be an abstract class or an ordinary class.
* Virtual base class is the base class in virtual inheritance, see virtual inheritance below for details.

> [Difference and connection between virtual functions and pure virtual functions in CSDN. C ++] (https://blog.csdn.net/u012260238/article/details/53610462)

### Virtual function pointer, virtual function table

* Virtual function pointer: In an object containing a virtual function class, it points to the virtual function table and is determined at runtime.
* Virtual function table: In the program read-only data section (`.rodata section`, see: [Target File Storage Structure] (#% E7% 9B% AE% E6% A0% 87% E6% 96% 87% E4% BB % B6% E5% AD% 98% E5% 82% A8% E7% BB% 93% E6% 9E% 84)), store the virtual function pointer, if the derived class implements a virtual function of the base class, then in the virtual The virtual function pointer covering the original base class in the table is created according to the class declaration at compile time.

> [Virtual function (table) implementation mechanism in C ++ and its simulation implementation in C language] (https://blog.twofei.com/496/)

### Virtual inheritance

Virtual inheritance is used to solve the problem of diamond inheritance under multiple inheritance conditions (wasting storage space and ambiguous).

The underlying implementation principle is related to the compiler, and is generally implemented through ** virtual base class pointer ** and ** virtual base class table **, and each virtual inherited subclass has a virtual base class pointer (occupies a pointer storage space , 4 bytes) and virtual base class table (does not occupy the storage space of class objects) (It should be emphasized that the virtual base class will still have a copy in the subclass, but there is only a maximum of one copy, not in the subclass Inside); When a subclass of virtual inheritance is inherited as a parent class, the virtual base class pointer will also be inherited.

In fact, vbptr refers to the virtual base table pointer (virtual base table pointer), the pointer points to a virtual base table (virtual table), the virtual table records the offset address of the virtual base class and this class; Offset the address, so that the members of the virtual base class are found, and virtual inheritance does not need to maintain two identical copies of the common base class (virtual base class) like ordinary multiple inheritance, saving storage space.

### Virtual inheritance, virtual function

* Similarities: both use virtual pointers (both occupy the storage space of the class) and virtual tables (neither occupy the storage space of the class)
* the difference:
    * Virtual inheritance
        * The virtual base class still exists in the inherited class and only takes up storage space
        * The virtual base class table stores the offset of the virtual base class relative to the directly inherited class
    * Virtual function
        * Virtual functions do not occupy storage space
        * The virtual function table stores the virtual function address

### Template classes, member templates, virtual functions

* Virtual functions can be used in template classes
* The member template of a class (whether it is an ordinary class or a class template) (which is a member function of the template) cannot be a virtual function

### Abstract class, interface class, aggregate class

* Abstract class: class containing pure virtual functions
* Interface class: an abstract class containing only pure virtual functions
* Aggregation class: users can directly access its members, and has a special form of initialization syntax. Meet the following characteristics:
    * All members are public
    * No constructor is defined
    * No class initialization
    * No base class, no virtual function

### Memory allocation and management

#### malloc, calloc, realloc, alloca

1. malloc: apply for a specified number of bytes of memory. The initial value in the applied memory is uncertain.
2. calloc: For objects of specified length, allocate memory that can hold the specified number of them. Every bit of the applied memory is initialized to 0.
3. realloc: Change the length of previously allocated memory (increase or decrease). When increasing the length, the content of the previously allocated area may need to be moved to another sufficiently large area, and the initial value in the newly added area is uncertain.
4. alloca: apply for memory on the stack. When the program is pushed out of the stack, it will automatically release the memory. However, it should be noted that alloca is not portable, and it is difficult to implement on machines without traditional stacks. alloca should not be used in programs that must be widely ported. C99 supports variable-length arrays (VLA), which can be used instead of alloca.

#### malloc, free

Used to allocate and free memory

malloc, free use

Apply for memory and confirm whether the application is successful

`` `cpp
char * str = (char *) malloc (100);
assert (str! = nullptr);
`` `

Pointer becomes empty after freeing memory

`` `cpp
free (p);
p = nullptr;
`` `

#### new, delete

1. new / new []: accomplish two things, first call malloc to allocate memory at the bottom, and then call the constructor (create object).
2. delete / delete []: Two things are also done, first call the destructor (clean up resources), and then call free to free up space.
3. new will automatically calculate the number of bytes required when applying for memory, and malloc requires us to enter the number of bytes for the memory space.

new, delete use

Apply for memory and confirm whether the application is successful

`` `cpp
int main ()
{
    T * t = new T (); // Memory allocation first, then constructor
    delete t; // Destructor first, then release memory
    return 0;
}
`` `

#### Position new

Positioning new (placement new) allows us to pass additional address parameters to new to create objects in a pre-specified memory area.

`` `cpp
new (place_address) type
new (place_address) type (initializers)
new (place_address) type [size]
new (place_address) type [size] {braced initializer list}
`` `

* `place_address` is a pointer
* `initializers` provides a (possibly empty) comma-separated list of initial values

### delete this Is it legal?

> [Is it legal (and moral) for a member function to say delete this?] (Https://isocpp.org/wiki/faq/freestore-mgmt#delete-this)

Legal, but:

1. It must be ensured that this object is allocated through `new` (not` new [] `, not placement new, not on the stack, not global, or not a member of other objects)
2. Make sure that the member function that calls `delete this` is the last member function that calls this
3. It must be ensured that this function is not called after `delete this` of the member function
4. It must be ensured that no one uses it after `delete this`

### How to define a class that can only generate objects on the heap (stack)?

> [How to define a class that can only generate objects on the heap (stack)?] (Https://www.nowcoder.com/questionTerminal/0a584aa13f804f3ea72b442a065a7618)

#### Only on the heap

Method: Make the destructor private

Reason: C ++ is a statically bound language. The compiler manages the life cycle of objects on the stack. When the compiler allocates stack space for class objects, it first checks the accessibility of the class's destructor. If the destructor is not accessible, you cannot create an object on the stack.

#### Only on the stack

Method: Reload new and delete as private

Reason: generating objects on the heap, using the new keyword operation, the process is divided into two stages: the first stage, using new to find available memory on the heap, allocated to the object; the second stage, calling the constructor to generate the object. If the new operation is set to private, the first stage cannot be completed, and the object cannot be generated on the heap.

### Smart pointer

#### C ++ Standard Library (STL)

Header file: `#include <memory>`

#### C ++ 98

`` `cpp
std :: auto_ptr <std :: string> ps (new std :: string (str));
`` `

#### C ++ 11

1. shared_ptr
2. unique_ptr
3. weak_ptr
4. auto_ptr (deprecated by C ++ 11)

* Class shared_ptr implements the concept of shared ownership (shared ownership). Multiple smart pointers point to the same object, and the object and its related resources will be released when "the last reference is destroyed". In order to perform the above work in a more complex scenario, the standard library provides auxiliary classes such as weak_ptr, bad_weak_ptr, and enable_shared_from_this.
* Class unique_ptr implements the concept of exclusive ownership or strict ownership, ensuring that only one smart pointer can point to the object at a time. You can transfer ownership. It is particularly useful for avoiding memory leaks (for example, forgetting to delete after new).

##### shared_ptr

Multiple smart pointers can share the same object, and the last one of the objects has the responsibility to destroy the object and clean up all resources related to the object.

* Support custom deleter (custom deleter), can prevent Cross-DLL problem (object is created by new in dynamic link library (DLL), but is destroyed by delete in another DLL), automatically release the mutex lock

##### weak_ptr

weak_ptr allows you to share but does not own an object. Once the last smart pointer that owns the object loses ownership, any weak_ptr will automatically become empty. Therefore, in addition to the default and copy constructors, weak_ptr only provides "accept a shared_ptr" constructor.

* The problem of cycles of references (cycles of references, two objects that have not been used actually point to each other, making it seem to be in the "used" state) can be broken

##### unique_ptr

unique_ptr is a type that was only available in C ++ 11 and is a smart pointer that can help avoid resource leaks when an exception occurs. Using exclusive ownership means that you can ensure that an object and its corresponding resources are owned by only one pointer at a time. Once it is destroyed or programmed empty, or starts to own another object, the previously owned object will be destroyed, and any corresponding resources will be released.

* unique_ptr is used to replace auto_ptr

##### auto_ptr

Deprecated by c ++ 11 due to lack of language features such as "std :: move" semantics for "construction and assignment", and other flaws.

##### Comparison of auto_ptr and unique_ptr

* auto_ptr can assign copy, ownership transfer after copying copy; unqiue_ptr has no copy assignment semantics, but implements `move` semantics;
* auto_ptr objects cannot manage arrays (destructive call `delete`), unique_ptr can manage arrays (destructive call` delete [] `);

### Mandatory type conversion operator

> [MSDN. Cast operator] (https://msdn.microsoft.com/zh-CN/library/5f6c9f8h.aspx)

#### static_cast

* For conversion of non-polymorphic types
* Do not perform runtime type checking (conversion security is not as good as dynamic_cast)
* Usually used to convert numeric data types (such as float-> int)
* You can move the pointer in the entire class hierarchy, it is safe to convert the subclass to the parent class (up conversion), and it is not safe to convert the parent class to the subclass (because the subclass may have fields or methods that are not in the parent class)

> Up conversion is an implicit conversion.

#### dynamic_cast

* For conversion of polymorphic types
* Perform line runtime type checking
* Only applicable to pointers or references
* Conversion of ambiguous pointer will fail (return nullptr), but no exception will be thrown
* You can move the pointer in the entire class hierarchy, including up conversion, down conversion

#### const_cast

* Used to remove const, volatile and __unaligned features (such as converting const int type to int type)

#### reinterpret_cast

* For simple reinterpretation of bits
* Abuse of the reinterpret_cast operator may easily bring risks. Unless the required conversion itself is low-level, one of the other cast operators should be used.
* Allow conversion of any pointer to any other pointer type (such as conversion from `char *` to `int *` or `One_class *` to `Unrelated_class *`, but it is not safe in itself)
* It also allows any integer type to be converted to any pointer type and reverse conversion.
* The reinterpret_cast operator cannot discard const, volatile, or __unaligned features.
* A practical use of reinterpret_cast is in a hash function, that is, by making two different values ​​hardly end with the same index to map values ​​to the index.

#### bad_cast

* Due to the failure to cast to a reference type, the dynamic_cast operator raises a bad_cast exception.

bad_cast use

`` `cpp
try {
    Circle & ref_circle = dynamic_cast <Circle &> (ref_shape);
}
catch (bad_cast b) {
    cout << "Caught:" << b.what ();
}
`` `

### Runtime Type Information (RTTI)

#### dynamic_cast

* For conversion of polymorphic types

#### typeid

* The typeid operator allows the type of the object to be determined at runtime
* type \ _id returns a reference to a type \ _info object
* If you want to obtain the data type of the derived class through the pointer of the base class, the base class must have a virtual function
* Can only get the actual type of the object

#### type_info

* The type_info class describes the type information generated by the compiler in the program. Objects of this class can effectively store pointers to the names of types. The type_info class can also store code values ​​suitable for comparing whether two types are equal or comparing their arrangement order. The coding rules and arrangement order of the types are unspecified and may vary from program to program.
* Header: `typeinfo`

typeid, type_info use

`` `cpp
#include <iostream>
using namespace std;

class Flyable // can fly
{
public:
    virtual void takeoff () = 0; // take off
    virtual void land () = 0; // landing
};
class Bird: public Flyable // bird
{
public:
    void foraging () {...} // foraging
    virtual void takeoff () {...}
    virtual void land () {...}
    virtual ~ Bird () {}
};
class Plane: public Flyable // aircraft
{
public:
    void carry () {...} // transport
    virtual void takeoff () {...}
    virtual void land () {...}
};

class type_info
{
public:
    const char * name () const;
    bool operator == (const type_info & rhs) const;
    bool operator! = (const type_info & rhs) const;
    int before (const type_info & rhs) const;
    virtual ~ type_info ();
private:
    ...
};

void doSomething (Flyable * obj) // do something
{
    obj-> takeoff ();

    cout << typeid (* obj) .name () << endl; // Output incoming object type ("class Bird" or "class Plane")

    if (typeid (* obj) == typeid (Bird)) // determine the object type
    {
        Bird * bird = dynamic_cast <Bird *> (obj); // object conversion
        bird-> foraging ();
    }

    obj-> land ();
}

int main () {
Bird * b = new Bird ();
doSomething (b);
delete b;
b = nullptr;
return 0;
}
`` `

## ⭐️ Effective

### Effective C++

1. Treat C ++ as a language federation (C, Object-Oriented C ++, Template C ++, STL)
2. It is better to replace the preprocessor with a compiler (try to replace `# define` with` const`, `enum`, and` inline`)
3. Use const whenever possible
4. Make sure the object has been initialized before use (assignment during construction (copy constructor) is more efficient than assignment after default construction (copy assignment))
5. Understand which functions C ++ silently writes and calls (the compiler secretly creates default constructor, copy constructor, copy assignment operator, destructor for class)
6. If you do not want to use the function automatically generated by the compiler, you should explicitly reject it (declare the member function you do not want to use as private and not implement it)
7. Declare a virtual destructor for the polymorphic base class (if class has any virtual functions, it should have a virtual destructor)
8. Don't let exceptions escape the destructor (destructors should swallow non-propagating exceptions, or end the program, rather than spit out exceptions; if you want to handle exceptions, they should be handled in non-destructive ordinary functions)
9. Never call virtual functions during construction and destruction (because such calls never fall to derived class)
10. Let `operator =` return a `reference to * this` (for chain assignment)
11. Handle "self assignment" in `operator =`
12. When assigning objects, make sure to copy "all member variables in the object" and "all base class components" (call the base class copy constructor)
13. Manage resources with objects (resources are obtained in the constructor and released in the destructor. It is recommended to use smart pointers. The resource acquisition time is the initialization time (Resource Acquisition Is Initialization, RAII))
14. Be careful about copying behavior in resource management classes (the common RAII class copying behavior is: suppress copying, reference counting, deep copying, and transfer bottom resource ownership (similar to auto_ptr))
15. Provide access to raw resources in the resource management class (access to raw resources may go through explicit conversion or implicit conversion. Generally speaking, conversion is safer, and implicit conversion is more convenient for customers)
16. Use the same form when using new and delete in pairs (using `[]` in `new` then delete []`, and `[]` not used in `new` then delete`)
17. Store (place) the newed object in a smart pointer in a separate statement (if you don't do this, it may lead to undetectable resource leaks due to compiler optimization)
18. Make the interface easy to use correctly, not easy to be misused (methods to promote normal use: consistency of the interface, compatible behavior of built-in types; methods to prevent misuse: create new types, restrict operations on types, and constrain object values , Eliminate customer resource management responsibilities)
19. Design class is just like design type, you need to consider object creation, destruction, initialization, assignment, value transfer, legal value, inheritance relationship, conversion, generalization and so on.
20. Rather replace pass-by-value with pass-by-reference-to-const (the former is usually more efficient and avoids the slicing problem), but it does not apply to built-in types, STL iterators, and function objects.
21. When you must return an object, do not deliberately return its reference (never return pointer or reference to a local stack object, or return reference to a heap-allocated object, or return pointer or reference to a local static object which may be required at the same time Multiple such objects.)
22. Declare member variables as private (for encapsulation, consistency, precise control of their reading and writing, etc.)
23. It is better to replace member function with non-member and non-friend (it can increase packaging, packaging flexibility and expandability)
24. If all parameters (including the metaphor parameter pointed by this pointer) require type conversion, please use the non-member function for this
25. Consider writing a swap function that does not throw exceptions
26. Delay the occurrence time of variable definitions as much as possible (can increase program clarity and improve program efficiency)
27. Do as little transformation as possible (old style: `(T) expression`,` T (expression) `; new style:` const_cast <T> (expression) `,` dynamic_cast <T> (expression) `,` reinterpret_cast <T > (expression) `,` static_cast <T> (expression) `;; avoid transformation as much as possible, focus on efficiency and avoid dynamic_casts, design as much as possible without transformation, encapsulate the transformation into a function, and prefer a new transformation)
28. Avoid using handles (including references, pointers, iterators) to point inside the object (to increase encapsulation, make const member functions behave more like const, and reduce "dangling handles" (such as dangling pointers, etc.)) possibility)
29. It ’s worth the effort to “exception safety” (Exception-safe functions) will not leak resources or allow any data structure to be corrupted even if an exception occurs, divided into three possible guarantees: basic, strong Type, do not throw abnormal type)
30. Thoroughly understand the inlining of inlining (inlining is compile-time behavior in most C ++ programs; whether the inline function is really inline depends on the compiler; most compilers refuse to be too complicated (such as with loops or recursion) ) Function inlining, and all calls to virtual functions (unless they are the most bland) will also make inlining fail; the code inflation caused by inline may bring efficiency losses; inline functions cannot be upgraded with the upgrade of the library)
31. Minimize compilation dependencies between files (if you can use object references or object pointers to complete the task, do not use objects; if possible, try to replace class declarative with class declarative; provide different for declarative and declarative Header file)
32. Make sure your public inherits the is-a (is a) relationship (everything that applies to base classes must be applicable to derived classes, because each derived class object is also a base class object )
33. Avoid obscuring inherited names (you can use using declarative or forwarding functions to make the obscured names goodbye)
34. Distinguish between interface inheritance and implementation inheritance (under public inheritance, derived classes always inherit the base class interface; pure virtual functions only specify interface inheritance; non-pure impure virtual functions specify interface inheritance and default implementation inheritance; non -virtual function specifies interface inheritance and mandatory implementation inheritance)
35. Consider other options than the virtual function (such as the non-virtual interface (NVI) method of the Template Method design pattern, replace the virtual function with a "function pointer member variable", and replace the virtual function with a tr1 :: function` member variable, Replace the virtual function in the inheritance system with a virtual function in another inheritance system)
36. Never redefine inherited non-virtual functions
37. Never redefine the inherited default parameter value, because the default parameter value is statically bound, but the virtual function is dynamically bound
38. Through compound molding has-a (there is one) or "implemented according to something" (in the application domain (application domain), compound means has-a (there is one); in the implementation domain), compound means With is-implemented-in-terms-of (based on something)
39. Use private inheritance wisely and prudently (private inheritance means is-implemented-in-terms-of (implemented according to something), use compound as much as possible, when the derived class needs to access members of the protected base class, or needs to (The private function is used when the virtual function is defined from the inheritance, or when the empty base is optimized.)
40. Use multiple inheritance wisely and carefully (multiple inheritance is more complicated than single inheritance, may lead to new ambiguity, and the need for virtual inheritance, but it does have legitimate uses, such as "public inheritance of an interface class" and "private inheritance" A class that assists in implementation; virtual inheritance can solve the ambiguity of diamond inheritance under multiple inheritance, but it will increase the cost of size, speed, complexity of initialization and assignment, etc.)
41. Understand implicit interfaces and compile-time polymorphism (both classes and templates support interfaces and polymorphism); the interface of the class is explicit with the signature as the center, and polymorphism is through virtual Functions occur at runtime; the interface of template is implicit based on valid expressions, and polymorphism occurs through template instantiation and function overloading resolution (function overloading resolution) at compile time)
42. Understand the dual meaning of typename (declaring the template type parameter is that the prefix keywords class and typename have the same meaning; please use the keyword typename to identify the nested subordinate type name, but not in the base class lists (base class lists) or members Use it as the base class modifier in the member initialization list)
43. Learn to deal with the name in the templated base class (you can refer to the name of the member in the base class templates through `this->` in the derived class templates, or by a clearly written "base class qualification modifier" )
44. Extract code irrelevant to parameters away from templates (code expansion due to non-type template parameters) can often be eliminated by replacing template parameters with function parameters or class member variables; due to type parameters The resulting code inflation can often be achieved by sharing implementation codes with implementation types with identical binary representations)
45. Use member function templates to accept all compatible types (please use member function templates to generate functions that "accept all compatible types"; declare member templates for "generalized copy construction" or "generalized assignment operation" Need to declare the normal copy constructor and copy assignment operator)
46. ​​When you need type conversion, please define non-member functions for the template (when we write a class template and the "related to this template" function provided by it supports "implicit type conversion of all parameters", please select those functions Defined as "friend function within class template")
47. Please use traits classes to express type information (traits classes through templates and "templates specialization" to make "type-related information" available at compile time, through overloading technology to achieve if ... else for types at compile time test)
48. Recognize template metaprogramming (template metaprogramming (TMP, template metaprogramming) can move work from runtime to compilation, so early error detection and higher execution efficiency can be achieved; TMP can be used to generate "giving policies" "Custom combination codes based on combinations of policy choices" can also be used to avoid generating codes that are not suitable for certain special types)
49. Understand the behavior of new-handler (set \ _new \ _handler allows customers to specify a function that is called when memory allocation cannot be satisfied; nothrow new is a rather limited tool because it is only applicable to memory allocation (operator new) , Subsequent constructor calls may still throw exceptions)
50. Understand the reasonable replacement timing of new and delete (in order to detect operational errors, collect usage statistics of dynamically allocated memory, increase the speed of allocation and return, reduce the space overhead caused by the default memory manager, make up for the default allocator Non-optimal alignment, cluster related objects, and obtain unconventional behavior)
51. When writing new and delete, you need to stick to the routine (operator new should contain an infinite loop and try to allocate memory in it. If it cannot meet the memory requirements, you should call new-handler, it should also be able to handle 0 bytes applications The class-specific version should also handle "larger (wrong) applications than the correct size"; operator delete should do nothing when the null pointer is received, and the class-specific version should also handle "bigger than the correct size (error )Application")
52. Writing placement new also writes placement delete (When you write a placement operator new, make sure to also write the corresponding placement operator delete, otherwise there may be a subtle and intermittent memory leak; when you declare placement new and placement delete, make sure not to cover up their normal versions unconsciously (unintentionally)
53. Don't ignore compiler warnings
54. Familiarize yourself with standard libraries including TR1 (TR1, C ++ Technical Report 1, C ++ 11 standard draft files)
55. Make yourself familiar with Boost (quasi-standard library)

### More Effective c++

1. Carefully distinguish between pointers and references (when you know that you need to point to something, and will never change to point to other things, or when you implement an operator and its grammatical requirements cannot be met by pointers, you should choose references; At any other time, please use pointers)
2. It is best to use C ++ transformation operators (`static_cast`,` const_cast`, `dynamic_cast`,` reinterpret_cast`)
3. Never deal with arrays in polymorphically (polymorphism and pointer arithmetic cannot be mixed; array objects almost always involve arithmetic operations on pointers, so do n’t mix arrays and polymorphism)
4. The default constructor is not necessary (to avoid the fields in the object being initialized meaninglessly)
5. Be alert to customized "type conversion functions" (single-argument constructors can avoid the misuse of compilers by simple methods (explicit keywords) or proxy classes); implicit type conversion operators can be changed to explicit Member function to avoid unexpected behavior)
6. Distinguish between the prefix and postfix forms of increment / decrement operator (pre-accumulation is taken out and returned, a reference is returned; post-accumulation is taken out and accumulated, and a const object is returned; when processing user-defined types, Should use pre-increment as much as possible; post-implementation should be based on its pre-sibling)
7. Never overload the `&&`, `||` and `,` operators (`&&` and `||` overloads will replace "sudden semantics" with "function call semantics"; `, `'S overloading cannot guarantee that the expression on the left must be evaluated earlier than the expression on the right)
8. Understand new and delete of different meanings (`new operator`,` operator new`, `placement new`,` operator new [] `;` delete operator`, `operator delete`,` destructor`, `operator delete [] `)
9. Use destructors to avoid leaking resources (releasing resources during destructors can avoid resource leaks when abnormal)
10. Prevent resource leaks in the constructors (since C ++ only destructs the constructed objects, so the constructor can use try ... catch or auto_ptr (and similar classes) to handle resource leaks)
11. Prohibit exceptions from flowing out of the destructors (reasons: one, to avoid the termination function being called during the stack-unwinding mechanism of the exception propagation process; second, to help ensure that the destructors complete all the things they should complete)
12. Understand the difference between "throwing an exception" and "passing a parameter" or "calling a virtual function" (first, exception objects will always be copied (except by pointer), if even captured by by value It is copied twice, and the object passed to the function parameter does not necessarily have to be copied; second, objects that are "thrown into exceptions" have fewer type conversion actions than objects "passed to the function"; Third, the catch clause is checked and compared by the compiler in the "order in which it appears in the source code", and the first one that matches successfully is executed, and a virtual function is called, which is selected to execute the "best with the object type" "Match" function)
13. Capture exceptions by by reference (to avoid the problem of object deletion and exception object cutting, retain the ability to capture standard exceptions, and restrict the number of times that exception objects need to be copied)
14. Use exception specifications wisely (exception specifications provide an excellent explanation of "what exceptions the function wants to throw"; there are also some disadvantages, including that the compiler only checks them locally and it is easy to inadvertently violate, and may Impede the higher-level exception handler to handle unexpected exceptions)
15. Understand the cost of exception handling (roughly, if you use try statement blocks, the code will expand by about 5% -10%, and the execution speed will also drop by this number; so please limit your use of try statement blocks and exception specifications Must-use locations, and exceptions are thrown only in the case of real exceptions)
16. Remember the 80-20 rule (the overall performance of the software is almost always determined by a small part of its constituent elements (code), and a program profiler can be used to identify the code that consumes resources)
17. Consider using lazy evaluation (slow evaluation) (can be applied to: Reference Counting) to avoid unnecessary object copying, distinguish operator [] read and write actions to do different things, Lazy Fetching (slow mode) Take out) to avoid unnecessary database reading actions, Lazy Expression Evaluation (expression slow evaluation) to avoid unnecessary numerical calculation actions)
18. Amortize the expected computational cost (over-eager evaluation can improve program efficiency when you have to support certain operations and its structure is almost always required, or its results are often required multiple times) )

### Google C ++ Style Guide

* English: [Google C ++ Style Guide] (https://google.github.io/styleguide/cppguide.html)
* Chinese: [C ++ Style Guide] (https://zh-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/contents/)

### Other

* [FAQ of Bjarne Stroustrup] (http://www.stroustrup.com/bs_faq.html)
* [Bjarne Stroustrup's C ++ style and tips FAQ] (http://www.stroustrup.com/bs_faq2.html)

## 📦 STL

### STL index

[STL Method Meaning Index] (https://github.com/huihut/interview/tree/master/STL)

### STL container

Container | Underlying data structure | Time complexity | Orderless | Non-repeatable | Other
--- | --- | --- | --- | --- | ---
[array] (https://github.com/huihut/interview/tree/master/STL#array) | array | random read change O (1) | unordered | repeatable | support random access
[vector] (https://github.com/huihut/interview/tree/master/STL#vector) | array | random read modification, tail insertion, tail deletion O (1) <br/> head insertion, head Delete O (n) | Unordered | Repeatable | Support random access
[deque] (https://github.com/huihut/interview/tree/master/STL#deque) | Double-ended queue | Head-to-tail insertion, head-to-tail deletion O (1) | Unordered | Repeatable | One central control + Multiple buffers, support fast addition and deletion at the beginning and end, support random access
[forward_list] (https://github.com/huihut/interview/tree/master/STL#forward_list) | Single linked list | insert, delete O (1) | unordered | repeatable | random access is not supported
[list] (https://github.com/huihut/interview/tree/master/STL#list) | Doubly linked list | Insert, delete O (1) | Unordered | Repeatable | Random access is not supported
[stack] (https://github.com/huihut/interview/tree/master/STL#stack) | deque / list | top insert, top delete O (1) | unordered | repeatable | deque or list closed head Open end, the reason for not using vector should be limited capacity size, time-consuming expansion
[queue] (https://github.com/huihut/interview/tree/master/STL#queue) | deque / list | tail insertion, head deletion O (1) | unordered | repeatable | deque or list closed The head end is open, the reason for not using the vector should be that the capacity is limited, and the expansion takes time
[priority_queue] (https://github.com/huihut/interview/tree/master/STL#priority_queue) | vector + max-heap | Insert, delete O (log <sub> 2 </ sub> n) | Ordered | Repeatable | vector container + heap processing rules
[set] (https://github.com/huihut/interview/tree/master/STL#set) | Red Black Tree | Insert, Delete, Find O (log <sub> 2 </ sub> n) | Ordered | Not repeatable |
[multiset] (https://github.com/huihut/interview/tree/master/STL#multiset) | Red Black Tree | Insert, Delete, Find O (log <sub> 2 </ sub> n) | Ordered | Repeatable |
[map] (https://github.com/huihut/interview/tree/master/STL#map) | Red Black Tree | Insert, Delete, Find O (log <sub> 2 </ sub> n) | Ordered | Not repeatable |
[multimap] (https://github.com/huihut/interview/tree/master/STL#multimap) | Red Black Tree | Insert, Delete, Find O (log <sub> 2 </ sub> n) | Ordered | Repeatable |
[unordered_set] (https://github.com/huihut/interview/tree/master/STL#unordered_set) | Hash Table | Insert, Delete, Find O (1) Worst O (n) | Unordered | Not Repeatable |
[unordered_multiset] (https://github.com/huihut/interview/tree/master/STL#unordered_multiset) | Hash table | insert, delete, find O (1) worst O (n) | unordered | repeatable |
[unordered_map] (https://github.com/huihut/interview/tree/master/STL#unordered_map) | Hash Table | Insert, Delete, Find O (1) Worst O (n) | Unordered | Not Repeatable |
[unordered_multimap] (https://github.com/huihut/interview/tree/master/STL#unordered_multimap) | Hash Table | Insert, Delete, Find O (1) Worst O (n) | Unordered | Repeatable |

### STL algorithm

Algorithm | Underlying Algorithm | Time Complexity | Non-Repeatable
--- | --- | --- | ---
[find] (http://www.cplusplus.com/reference/algorithm/find/) | Sequential search | O (n) | Repeatable
[sort] (https://github.com/gcc-mirror/gcc/blob/master/libstdc++-v3/include/bits/stl_algo.h#L4808) | [introspective sorting] (https: //en.wikipedia .org / wiki / Introsort) | O (n * log <sub> 2 </ sub> n) | Repeatable

## 〽️ Data structure

### Sequential structure

#### Sequence Stack (Sequence Stack)

[SqStack.cpp] (DataStructure / SqStack.cpp)

Sequential stack data structure and pictures

`` `cpp
typedef struct {
ElemType * elem;
int top;
int size;
int increment;
} SqStack;
`` `

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/SqStack.png)

#### Queue (Sequence Queue)

Queue data structure

`` `cpp
typedef struct {
ElemType * elem;
int front;
int rear;
int maxSize;
} SqQueue;
`` `

##### Acyclic queue

Acyclic queue picture

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/SqQueue.png)

`SqQueue.rear ++`

##### Circular queue

Circular queue picture

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/SqLoopStack.png)

`SqQueue.rear = (SqQueue.rear + 1)% SqQueue.maxSize`

#### Sequence List (Sequence List)

[SqList.cpp] (DataStructure / SqList.cpp)

Sequence table data structure and pictures

`` `cpp
typedef struct {
ElemType * elem;
int length;
int size;
int increment;
} SqList;
`` `

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/SqList.png)


### Chain structure

[LinkList.cpp] (DataStructure / LinkList.cpp)

[LinkList_with_head.cpp] (DataStructure / LinkList_with_head.cpp)

Chained data structure

`` `cpp
typedef struct LNode {
    ElemType data;
    struct LNode * next;
} LNode, * LinkList;
`` `

#### Link Queue

Chain queue picture

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/LinkQueue.png)

#### Chain representation of linear table

##### Link List

Singly linked list pictures

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/LinkList.png)

##### Doubly linked list (Du-Link-List)

Picture of doubly linked list

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/DuLinkList.png)

##### Cir-Link-List

Picture of a circular list

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/CirLinkList.png)

### Hash table

[HashTable.cpp] (DataStructure / HashTable.cpp)

#### Concept

Hash function: `H (key): K-> D, key ∈ K`

#### Construction method

* Direct addressing method
* Divided remainder method
* Digital analysis method
* Folding method
* Square method

#### Conflict handling method

* Chain address method: use the same link to link with the same key
* Open addressing method
    * Linear detection method: the same key-> put it in the next position of key, `Hi = (H (key) + i)% m`
    * Secondary detection method: the same key-> put in `Di = 1 ^ 2, -1 ^ 2, ..., ± (k) ^ 2, (k <= m / 2)`
    * Random detection method: `H = (H (key) + pseudo-random number)% m`

#### Linear probing hash table data structure

Hash table data structure and picture of linear detection

`` `cpp
typedef char KeyType;

typedef struct {
KeyType key;
} RcdType;

typedef struct {
RcdType * rcd;
int size;
int count;
bool * tag;
} HashTable;
`` `

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/HashTable.png)

### Recursion

#### Concept

The function calls itself directly or indirectly

#### Recursion and divide and conquer

* Divide and conquer
    * Breakdown of the problem
    * Decomposition of problem scale
* Search in half (recursive)
* Merge sort (recursive)
* Quick sort (recursive)

#### Recursion and iteration

* Iteration: repeatedly use old values ​​of variables to derive new values
* Search in half (iteration)
* Merge sort (iteration)

#### Generalized table

##### Head and tail linked list storage representation

Storage representation and picture of head and tail linked list of generalized table

`` `cpp
// Head and tail linked list storage representation of generalized table
typedef enum {ATOM, LIST} ElemTag;
// ATOM == 0: atom, LIST == 1: child table
typedef struct GLNode {
    ElemTag tag;
    // Common part, used to distinguish between atomic nodes and table nodes
    union {
        // Joint part of atomic node and table node
        AtomType atom;
        // atom is the range of atomic nodes, AtomType is defined by the user
        struct {
            struct GLNode * hp, * tp;
        } ptr;
        // ptr is the pointer field of the table node, prt.hp and ptr.tp point to the head and tail of the table respectively
    } a;
} * GList, GLNode;
`` `

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/GeneralizedList1.png)

##### Extended linear linked list storage representation

Extended linear linked list storage representation and pictures

`` `cpp
// Extended linear linked list storage representation of generalized tables
typedef enum {ATOM, LIST} ElemTag;
// ATOM == 0: atom, LIST == 1: child table
typedef struct GLNode1 {
    ElemTag tag;
    // Common part, used to distinguish between atomic nodes and table nodes
    union {
        // Joint part of atomic node and table node
        AtomType atom; // Value range of atomic node
        struct GLNode1 * hp; // Header pointer of table node
    } a;
    struct GLNode1 * tp;
    // Equivalent to next in a linear list, pointing to the next element node
} * GList1, GLNode1;
`` `

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/GeneralizedList2.png)

### Binary tree

[BinaryTree.cpp] (DataStructure / BinaryTree.cpp)

#### Nature

1. Non-empty binary tree at level i has at most 2 <sup> (i-1) </ sup> nodes (i> = 1)
2. Binary tree of depth k has at most 2 <sup> k </ sup>-1 node (k> = 1)
3. The number of nodes with degree 0 is n <sub> 0 </ sub>, and the number of nodes with degree 2 is n <sub> 2 </ sub>, then n <sub> 0 </ sub> = n <sub > 2 </ sub> + 1
4. The depth of a complete binary tree with n nodes k = ⌊ log <sub> 2 </ sub> (n) ⌋ + 1
5. For the node numbered i (1 <= i <= n) in the complete binary tree with n nodes
    1. If i = 1, the root, otherwise the parent is ⌊ i / 2 ⌋
    2. If 2i> n, the i node has no left child, otherwise the child number is 2i
    3. If 2i + 1> n, the i node has no right child, otherwise the child number is 2i + 1

#### Storage structure

Binary tree data structure

`` `cpp
typedef struct BiTNode
{
    TElemType data;
    struct BiTNode * lchild, * rchild;
} BiTNode, * BiTree;
`` `

##### Sequential storage

Binary tree sequential storage of pictures

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/SqBinaryTree.png)

##### Chain storage

Binary tree chain storage pictures

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/LinkBinaryTree.png)

#### Traversal method

* First traversal
* In-order traversal
* Subsequent traversal
* Level traversal

#### Category

* Full binary tree
* Complete binary tree (heap)
    * Large top pile: root> = left && root> = right
    * Small top heap: root <= left && root <= right
* Binary search tree (binary sorting tree): left <root <right
* Balanced binary tree (AVL tree): | Left subtree tree height-Right subtree tree height | <= 1
* The smallest unbalanced tree: the subtree where the balanced binary tree inserts a new node to cause the unbalance: adjustment:
    * LL type: the left child of the root rotates right
    * RR type: the right child of the root is left-handed
    * LR type: the left child of the root turns left and then right
    * RL type: the left child of the right child, right-handed first, then left-handed

### Other trees and forests

#### Tree storage structure

* Parental notation
* Parent and child notation
* Child brother notation

#### And check set

A set of disjoint subsets S = {S1, S2, ..., Sn}

#### Balanced binary tree (AVL tree)

##### Nature

* | Left subtree tree height-Right subtree tree height | <= 1
* The balanced binary tree must be a binary search tree, otherwise it is not necessarily
* The formula of the node of the least binary balanced tree: `F (n) = F (n-1) + F (n-2) + 1` (1 is the root node, F (n-1) is the left subtree Number of nodes, F (n-2) is the number of nodes in the right subtree)

Balanced binary tree picture

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/Self-balancingBinarySearchTree.png)

##### Minimum imbalance tree

Subtree in which a balanced binary tree inserts a new node causing imbalance

Adjustment:

* LL type: the left child of the root rotates right
* RR type: the right child of the root is left-handed
* LR type: the left child of the root turns left and then right
* RL type: the left child of the right child, right-handed first, then left-handed

#### Red Black Tree

[RedBlackTree.cpp] (DataStructure / RedBlackTree.cpp)

##### What are the characteristics of the red-black tree?

1. The node is red or black.
2. The root is black.
3. All leaves are black (leaves are NIL nodes).
4. Each red node must have two black child nodes. (There cannot be two consecutive red nodes on all paths from each leaf to the root.) (The parent node of the newly added node must be the same)
5. All simple paths from any node to each of its leaves contain the same number of black nodes. (The new node must be red)

##### Adjustment

1. discoloration
2. Left
3. Turn right

##### Application

* Associative array: such as map, set in STL

##### The difference between red-black tree, B tree, B + tree?

* The depth of the red-black tree is relatively large, while the depth of the B tree and B + tree is relatively small
* B + tree saves all data in leaf nodes, and connects them together in the form of linked list.

#### B-tree (B-tree), B + tree (B + -tree)

B tree, B + tree pictures

! [B tree (B-tree), B + tree (B + -tree)] (https://i.stack.imgur.com/l6UyF.png)

##### Features

* Generalized binary search tree
* "Dumpy", internal (non-leaf) nodes can have a variable number of child nodes (the number range is predefined)

##### Application

* Most file systems and database systems use B-tree and B + -tree as the index structure

##### the difference

* Only the leaf nodes in the B + tree will have a pointer to the record (ROWID), while the B tree has all the nodes, and the index items that appear in the internal nodes will no longer appear in the leaf nodes.
* All leaf nodes in the B + tree are connected by pointers, but the B tree does not.

##### Advantages of B-tree

The data of the internal nodes can be obtained directly, without having to locate according to the leaf nodes.

##### Advantages of B + tree

* Non-leaf nodes will not bring ROWID, so that a block can accommodate more index items, one can reduce the height of the tree. Second, an internal node can locate more leaf nodes.
* The leaf nodes are connected by pointers, the range scan will be very simple, and for the B-tree, the leaf nodes and internal nodes need to move back and forth.

> The difference between B tree and B + tree comes from: [differences-between-b-trees-and-b-trees] (https://stackoverflow.com/questions/870218/differences-between-b-trees-and-b-trees ), [The difference between B tree and B + tree] (https://www.cnblogs.com/ivictor/p/5849061.html)

#### Octree

Octree pictures

! [] (https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Octree2.png/400px-Octree2.png)

An octree, or octree, is a tree-like data structure used to describe three-dimensional space (divide space). Each node of the octree represents a volume element of a cube, and each node has eight child nodes. The volume elements represented by these eight child nodes add up to the volume of the parent node. Generally, the center point serves as the bifurcation center of the node.

##### Purpose

* 3D computer graphics
* Nearest neighbor search

## ⚡️ Algorithm

### Sort

Sorting Algorithm | Average Time Complexity | Worst Time Complexity | Space Complexity | Data Object Stability
--- | --- | --- | --- | ---
[Bubbling Sort] (Algorithm / BubbleSort.h) | O (n <sup> 2 </ sup>) | O (n <sup> 2 </ sup>) | O (1) | Stable
[Select Sort] (Algorithm / SelectionSort.h) | O (n <sup> 2 </ sup>) | O (n <sup> 2 </ sup>) | O (1) | The array is unstable and the linked list is stable
[Insert Sort] (Algorithm / InsertSort.h) | O (n <sup> 2 </ sup>) | O (n <sup> 2 </ sup>) | O (1) | Stable
[Quick Sort] (Algorithm / QuickSort.h) | O (n * log <sub> 2 </ sub> n) | O (n <sup> 2 </ sup>) | O (log <sub> 2 </ sub> n) | unstable
[Heap Sort] (Algorithm / HeapSort.cpp) | O (n * log <sub> 2 </ sub> n) | O (n * log <sub> 2 </ sub> n) | O (1) | No stable
[Merge Sort] (Algorithm / MergeSort.h) | O (n * log <sub> 2 </ sub> n) | O (n * log <sub> 2 </ sub> n) | O (n) | Stable
[Hill Sort] (Algorithm / ShellSort.h) | O (n * log <sup> 2 </ sup> n) | O (n <sup> 2 </ sup>) | O (1) | Unstable
[Count Sort] (Algorithm / CountSort.cpp) | O (n + m) | O (n + m) | O (n + m) | Stable
[Bucket Sorting] (Algorithm / BucketSort.cpp) | O (n) | O (n) | O (m) | Stable
[Base Sorting] (Algorithm / RadixSort.h) | O (k * n) | O (n <sup> 2 </ sup>) | | Stable

> * Are arranged from small to large
> * k: represents the number of "digits" in the value
> * n: represents the data size
> * m: represents the maximum value minus the minimum value of the data
> * From: [wikipedia. Sorting algorithm] (https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)

### Find

Search Algorithm | Average Time Complexity | Space Complexity | Search Condition
--- | --- | --- | ---
[Sequential Search] (Algorithm / SequentialSearch.h) | O (n) | O (1) | Unordered or Ordered
[Binary search (half search)] (Algorithm / BinarySearch.h) | O (log <sub> 2 </ sub> n) | O (1) | Ordered
[Interpolation search] (Algorithm / InsertionSearch.h) | O (log <sub> 2 </ sub> (log <sub> 2 </ sub> n)) | O (1) | Ordered
[Fibonacci Search] (Algorithm / FibonacciSearch.cpp) | O (log <sub> 2 </ sub> n) | O (1) | Ordered
[Hash Search] (DataStructure / HashTable.cpp) | O (1) | O (n) | Unordered or Ordered
[Binary Search Tree (Binary Search Tree Search)] (Algorithm / BSTSearch.h) | O (log <sub> 2 </ sub> n) | |
[红黑 树] (DataStructure / RedBlackTree.cpp) | O (log <sub> 2 </ sub> n) | |
2-3 tree | O (log <sub> 2 </ sub> n-log <sub> 3 </ sub> n) | |
B tree / B + tree | O (log <sub> 2 </ sub> n) | |

### Graph search algorithm

Graph search algorithm | data structure | traversal time complexity | space complexity
--- | --- | --- | ---
[BFS breadth first search] (https://en.wikipedia.org/wiki/%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C% E7% B4% A2) | Adjacency matrix <br/> Adjacency list | O (\ | v \ | <sup> 2 </ sup>) <br/> O (\ | v \ | + \ | E \ |) | O (\ | v \ | <sup> 2 </ sup>) <br/> O (\ | v \ | + \ | E \ |)
[DFS Depth First Search] (https://zh.wikipedia.org/wiki/%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C% E7% B4% A2) | Adjacency matrix <br/> Adjacency list | O (\ | v \ | <sup> 2 </ sup>) <br/> O (\ | v \ | + \ | E \ |) | O (\ | v \ | <sup> 2 </ sup>) <br/> O (\ | v \ | + \ | E \ |)

### Other algorithms

Algorithm | Idea | Application
--- | --- | ---
[Divide and Conquer] (https://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95) | divide a complex problem into two or more The same or similar sub-problems, until the last sub-problem can be simply solved directly, the solution of the original problem is the combination of the sub-problems | [round robin schedule problem] (https://github.com/huihut/interview/tree/ master / Problems / RoundRobinProblem), sorting algorithm (quick sorting, merge sorting)
[Dynamic Planning] (https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)|By decomposing the original problem into relative A simple subproblem method for solving complex problems, suitable for problems with overlapping subproblems and optimal substructure properties | [Backpack problem] (https://github.com/huihut/interview/tree/master/Problems/ KnapsackProblem), Fibonacci sequence
[Greedy method] (https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E6%B3%95)|A choice in each step is taken in the current state The best or optimal (that is, the most favorable) choice, which hopes to result in the best or optimal algorithm | travel salesman problem (shortest path problem), minimum spanning tree, Huffman coding

## ❓ Problems

### Single Problem

* [Chessboard Coverage Problem] (Problems / ChessboardCoverageProblem)
* [Knapsack Problem] (Problems / KnapsackProblem)
* [Neumann Neighbor Problem (Problems / NeumannNeighborProblem)]
* [Round Robin Problem (Round Robin Problem)] (Problems / RoundRobinProblem)
* [Tubing Problem (Problems / TubingProblem)]

### Leetcode Problems

* [Github. Haoel / leetcode] (https://github.com/haoel/leetcode)
* [Github. Pezy / LeetCode] (https://github.com/pezy/LeetCode)

### Sword Finger Offer

* [Github. Zhedahht / CodingInterviewChinese2] (https://github.com/zhedahht/CodingInterviewChinese2)
* [Github. Gatieme / CodingInterviews] (https://github.com/gatieme/CodingInterviews)

### Cracking the Coding Interview Programmer Interview Gold Code

* [Github. Careercup / ctci] (https://github.com/careercup/ctci)
* [Niu Ke. Programmer Interview Gold Code] (https://www.nowcoder.com/ta/cracking-the-coding-interview)

### Niuke.com

* [Nuke. Online Programming Topics] (https://www.nowcoder.com/activity/oj)

## 💻 Operating system

### Processes and threads

For threaded systems:
* Process is an independent unit of resource allocation
* Thread is an independent unit of resource scheduling

For threadless systems:
* Process is an independent unit for resource scheduling and allocation

#### Communication methods between processes and their advantages and disadvantages

* Pipeline (PIPE)
    * Famous pipes: a half-duplex communication method that allows communication between unrelated processes
        * Advantages: can achieve communication between processes of arbitrary relationship
        * Disadvantages:
            1. Long-term storage in the system, improper use is prone to errors
            2. Limited buffer
    * Anonymous pipes: a half-duplex communication method, which can only be used between processes that are related (parent-child process)
        * Advantages: simple and convenient
        * Disadvantages:
            1. Limited to one-way communication
            2. Can only be created between its processes and its related processes
            3. Limited buffer
* Semaphore: a counter that can be used to control multiple threads' access to shared resources
    * Pros: Can synchronize processes
    * Disadvantages: limited semaphore
* Signal (Signal): a more complex communication method, used to notify the receiving process that an event has occurred
* Message Queue (Message Queue): is a linked list of messages, stored in the kernel and identified by the message queue identifier
    * Advantages: Can achieve communication between any process, and achieve synchronization between message sending and receiving through system call functions, without considering synchronization issues, convenient
    * Disadvantages: copying information requires additional CPU time, not suitable for large amounts of information or frequent operations
* Shared memory (Shared Memory): Map a section of memory that can be accessed by other processes. This shared memory is created by one process, but multiple processes can access it
    * Advantages: no need to copy, fast, large amount of information
    * Disadvantages:
        1. Communication is achieved by directly attaching the shared space buffer to the virtual address space of the process, so the synchronization of read and write operations between processes
        2. Use the memory buffer to directly exchange information. The entity of the memory exists in the computer and can only be shared by many processes in the same computer system, which is not convenient for network communication.
* Socket (Socket): can be used for process communication between different computers
    * Advantages:
        1. The transmission data is byte level, the transmission data can be customized, the data volume is small and the efficiency is high
        2. Short data transmission time and high performance
        3. Suitable for real-time information interaction between client and server
        4. Can be encrypted, strong data security
    * Disadvantages: need to analyze the transmitted data and convert it into application-level data.

#### Communication method between threads

* Lock mechanism: including mutex / mutex, reader-writer lock, spin lock, condition variable
    * Mutexes / quantities (mutex): Provides an exclusive way to prevent data structures from being modified concurrently.
    * Reader-writer lock: allows multiple threads to read shared data at the same time, and write operations are mutually exclusive.
    * Spin locks (spin locks) are similar to mutex locks, all to protect shared resources. The mutex lock is when the resource is occupied and the applicant goes to sleep; while the spin lock cyclically detects whether the holder has released the lock.
    * Condition variable (condition): You can block the process atomically until a certain condition is true. The test of the condition is carried out under the protection of the mutex. Condition variables are always used with mutex locks.
* Semaphore mechanism (Semaphore)
    * Unnamed thread semaphore
    * Name thread semaphore
* Signal mechanism (Signal): similar to signal processing between processes
* Barrier (barrier): The barrier allows each thread to wait until all cooperating threads have reached a certain point, and then continue execution from that point.

The purpose of communication between threads is mainly used for thread synchronization, so threads do not have a communication mechanism for data exchange like process communication

> The communication method between processes and the advantages and disadvantages come from: [summary of process thread interview questions] (http://blog.csdn.net/wujiafei_njgcxy/article/details/77098977)

#### Private and shared resources between processes

* Private: address space, heap, global variables, stack, registers
* Sharing: code segment, public data, process directory, process ID

#### Private and shared resources between threads

* Private: thread stack, registers, program counter
* Sharing: heap, address space, global variables, static variables

#### Comparison, advantages, disadvantages and choices between multi-process and multi-thread

##### Compared

Contrast dimension | multi-process | multi-thread | summary
--- | --- | --- | ---
Data sharing and synchronization | Data sharing is complex and requires IPC; data is separate and synchronization is simple | because sharing process data, data sharing is simple, but also because of this reason, synchronization is complicated | each has its own advantages
Memory, CPU | Occupying more memory, complex switching, low CPU utilization | Less memory occupation, simple switching, high CPU utilization | Thread dominance
Create, destroy, switch | Create, destroy, switch is complicated, slow | Create, destroy, switch, simple, fast | thread dominant
Programming, debugging | Simple programming, simple debugging | Complex programming, complicated debugging | The process is dominant
Reliability | The process will not affect each other | The hang of a thread will cause the entire process to hang | The process is dominant
Distributed | Adapted to multi-core, multi-machine distributed; if one machine is not enough, it is relatively simple to expand to multiple machines | Adapted to multi-core distributed | process dominant

##### Pros and cons

Pros and cons | Multiprocess | Multithreading
--- | --- | ---
Advantages | Simple programming and debugging, high reliability | Fast creation, destruction and switching speed, small memory and resource occupation
Disadvantages | Slow creation, destruction, switching speed, large memory and resource occupation | Complex programming and debugging, and poor reliability

##### choice

* Need to frequently create priority threads for destruction
* Prioritize the use of threads that require a lot of calculations
* Threads for strong correlation processing and processes for weak correlation processing

### File system

* Windows: FCB table + FAT + bitmap
* Unix: inode + mixed index + group link

### Host endianness and network endianness

#### Host byte order (CPU byte order)

##### Concept

The host byte order is also called CPU byte order, which is not determined by the operating system, but by the CPU instruction set architecture. There are two types of host byte order:

* Big endian (Big Endian): high-order bytes are stored in the low-order address, low-order bytes are stored in the high-order address
* Little endian (Little Endian): high-order bytes are stored in the high-order address, low-order bytes are stored in the low-order address

##### Storage method

The 32-bit integer `0x12345678` is stored starting from the address whose starting position is` 0x00`, then:

Memory address | 0x00 | 0x01 | 0x02 | 0x03
--- | --- | --- | --- | ---
Big endian | 12 | 34 | 56 | 78
Little endian | 78 | 56 | 34 | 12

Big endian little endian pictures

! [大端 序] (https://raw.githubusercontent.com/huihut/interview/master/images/CPU-Big-Endian.svg.png)
! [Little Endian Order] (https://raw.githubusercontent.com/huihut/interview/master/images/CPU-Little-Endian.svg.png)

##### Judging big endian little endian

Judge big endian little endian

You can judge whether your CPU byte order is big-endian or little-endian like this:

`` `cpp
#include <iostream>
using namespace std;

int main ()
{
int i = 0x12345678;

if (* ((char *) & i) == 0x12)
cout << "big end" << endl;
else
cout << "little end" << endl;

return 0;
}
`` `

##### Byte order of processors of various architectures

* x86 (Intel, AMD), MOS Technology 6502, Z80, VAX, PDP-11 and other processors are little-endian;
* Motorola 6800, Motorola 68000, PowerPC 970, System / 370, SPARC (except V9) and other processors are big-endian;
* The byte order of ARM (default little endian), PowerPC (except PowerPC 970), DEC Alpha, SPARC V9, MIPS, PA-RISC and IA64 is configurable.

#### Network byte order

The network byte order is a data representation format specified in TCP / IP, which has nothing to do with the specific CPU type, operating system, etc., so as to ensure that the data can be correctly interpreted when transferred between different hosts.

The network byte order adopts: Big Endian (Big Endian) arrangement.

### Page replacement algorithm

During the address mapping process, if the page to be accessed is found in the page that is not in memory, a page fault interrupt is generated. When a page fault interrupt occurs, if there is no free page in the operating system memory, the operating system must select a page in the memory to move it out of memory to make room for the page that will be paged in. The rule used to choose which page to eliminate is called the page replacement algorithm.

#### Category

* Global replacement: replacement in the entire memory space
* Partial replacement: replacement in this process

#### Algorithm

Global:
* Working set algorithm
* Page missing rate replacement algorithm

Local:
* Best replacement algorithm (OPT)
* First-in first-out replacement algorithm (FIFO)
* The most recent unused (LRU) algorithm
* Clock (Clock) replacement algorithm

## ☁️ Computer network

> Some knowledge points in this section come from "Computer Network (7th Edition)"

Computer network architecture:

! [Computer Network Architecture] (https://raw.githubusercontent.com/huihut/interview/master/images/Computer Network Architecture.png)

### The role and agreement of each layer

Layering | Role | Agreement
--- | --- | ---
Physical layer | Transmission of bits through the medium to determine the mechanical and electrical specifications (Bit Bit) | RJ45, CLOCK, IEEE802.3 (repeater, hub)
Data link layer | Assembling bits into frames and point-to-point transfer (Frame Frame) | PPP, FR, HDLC, VLAN, MAC (bridge, switch)
Network layer | Responsible for the transmission of data packets from source to sink and Internet interconnection (Packet Packet) | IP, ICMP, ARP, RARP, OSPF, IPX, RIP, IGRP (router)
Transport layer | Provide end-to-end reliable message delivery and error recovery (segment) | TCP, UDP, SPX
Session Layer | Establish, manage and terminate sessions (Session Protocol Data Unit SPDU) | NFS, SQL, NETBIOS, RPC
Presentation layer | Translate, encrypt and compress data (indicating protocol data unit PPDU) | JPEG, MPEG, ASII
Application layer | Means to allow access to the OSI environment (application protocol data unit APDU) | FTP, DNS, Telnet, SMTP, HTTP, WWW, NFS


### Physical layer

* Unit of data transmission: bit
* Data transmission system: source system (source point, sender)-> transmission system-> destination system (receiver, end point)

aisle:
* Unidirectional channel (simplex channel): only one direction communication, no reverse direction interaction, such as broadcasting
* Two-way alternating communication (half-duplex communication): Both parties can send messages, but they cannot send or receive at the same time
* Two-way simultaneous communication (full-duplex communication): both sides of the communication can send and receive information at the same time

Channel multiplexing technology:
* Frequency division multiplexing (FDM, Frequency Division Multiplexing): different users are in different frequency bands, and the users used occupy different bandwidth resources at the same time
* Time Division Multiplexing (TDM, Time Division Multiplexing): different users in different time slices in the same time period, all users occupy the same frequency bandwidth at different times
* Wavelength Division Multiplexing (WDM, Wavelength Division Multiplexing): optical frequency division multiplexing
* Code Division Multiplexing (CDM): Different users use different codes and can use the same frequency band to communicate at the same time

### data link layer

Main channels:
* Point-to-point channel
* Broadcast channel

#### Point-to-point channel

* Data unit: frame

Three basic questions:
* Encapsulation and framing: Encapsulate the IP datagram of the network layer into a frame, `SOH-data part-EOT`
* Transparent transmission: No matter what character in the data part, it can be transmitted; it can be solved by byte filling method (the escape character is added before the conflict character)
* Error detection: reduce the bit error rate (BER, Bit Error Rate), widely used cyclic redundancy check (CRC, Cyclic Redundancy Check)

Point-to-Point Protocol:
* Point-to-Point Protocol (Point-to-Point Protocol): the protocol used when the user's computer communicates with the ISP

#### Broadcast channel

Broadcast communication:
* Hardware address (physical address, MAC address)
* Unicast (unicast) frame (one-to-one): the MAC address of the received frame is the same as the hardware address of the station
* Broadcast (broadcast) frames (one pair of all): frames sent to all sites on the local area network
* Multicast (multicast) frames (one-to-many): frames sent to some sites on the local area network

### Network layer

* IP (Internet Protocol, Internet Protocol) is a protocol designed for computer networks to communicate with each other.
* ARP (Address Resolution Protocol)
* ICMP (Internet Control Message Protocol, Internet Control Message Protocol)
* IGMP (Internet Group Management Protocol, Internet Group Management Protocol)

#### IP Internet Protocol

IP address classification:
* `IP address :: = {<network number>, <host number>}`

IP address category | Network number | Network range | Host number | IP address range
--- | --- | --- | --- | ---
Class A | 8bit, the first bit is fixed at 0 | 0-127 | 24bit | 1.0.0.0-127.255.255.255
Class B | 16bit, the first two are fixed at 10 | 128.0-191.255 | 16bit | 128.0.0.0-191.255.255.255
Type C | 24bit, the first three bits are fixed at 110 | 192.0.0-223.255.255 | 8bit | 192.0.0.0-223.255.255.255
Class D | The first four digits are fixed at 1110, the latter are multicast addresses
Class E | The first five digits are fixed at 11110, the latter are reserved for future use

IP datagram format:

! [IP datagram format] (https://raw.githubusercontent.com/huihut/interview/master/images/IP datagram format.png)
#### ICMP Internet Control Message Protocol

ICMP message format:

! [ICMP message format] (https://raw.githubusercontent.com/huihut/interview/master/images/ICMP message format.png)

application:
* PING (Packet InterNet Groper) detects the connectivity between two hosts
* TTL (Time To Live, time to live) This field specifies the maximum number of network segments that IP packets are allowed to pass before being discarded by the router

#### Internal Gateway Protocol

* RIP (Routing Information Protocol, routing information protocol)
* OSPF (Open Sortest Path First, open shortest path first)

#### External Gateway Protocol

* BGP (Border Gateway Protocol, border gateway protocol)

#### IP Multicast

* IGMP (Internet Group Management Protocol, Internet Group Management Protocol)
* Multicast routing protocol

#### VPN and NAT

* VPN (Virtual Private Network, virtual private network)
* NAT (Network Address Translation)

#### What does the routing table contain?

1. Network ID (Network ID, Network number): It is the network ID of the target address.
2. Subnet mask: used to judge the network to which the IP belongs
3. Next hop address / interface (Next hop / interface): It is the address of the next stop of the data on the journey to the destination address. The interface points to next hop (that is, the next route). The route in an autonomous system (AS, Autonomous system) should contain all subnets in the area, and the default gateway (Network id: `0.0.0.0`, Netmask:` 0.0.0.0`) points to the exit of the autonomous system.

Depending on the application and implementation, the routing table may contain the following additional information:

1. Cost (Cost): is the cost required to pass the path in the data transmission process.
2. Quality of service for routing
3. List of outgoing / incoming connections to be filtered in routing

### Transport layer

protocol:

* TCP (Transmission Control Protocol, transmission control protocol)
* UDP (User Datagram Protocol, user datagram protocol)

port:

Applications | FTP | TELNET | SMTP | DNS | TFTP | HTTP | HTTPS |
--- | --- | --- | --- | --- | --- | --- | --- | ---
Port number | 21 | 23 | 25 | 53 | 69 | 80 | 443 | 161

#### TCP

* TCP (Transmission Control Protocol, Transmission Control Protocol) is a connection-oriented, reliable, and byte-based transport layer communication protocol whose transmission unit is the message segment.

feature:
* Connection-oriented
* Only point-to-point (one-to-one) communication
* Reliable interaction
* Full duplex communication
* Byte-oriented

How TCP guarantees reliable transmission:
* Confirmation and timeout retransmission
* Reasonable data segmentation and sorting
* flow control
* Congestion control
* Data validation

TCP message structure

! [TCP message] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP message.png)

TCP header

! [TCP header] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP header.png)

TCP: Status Control Code (Code, Control Flag), which occupies 6 bits and has the following meanings:
* URG: urgent bit (urgent). When `URG = 1, it indicates that the urgent pointer field is valid, which means the packet is an urgent packet. It tells the system that there is urgent data in this segment, which should be transmitted as soon as possible (equivalent to high-priority data), and the Urgent Pointer field in the above figure will also be enabled.
* ACK: Acknowledge bit. The acknowledgment number field is only valid when `ACK = 1’, which means this packet is an acknowledgment packet. When `ACK ＝ 0`, the confirmation number is invalid.
* PSH: (Push function) If it is 1, the representative requests the other party to immediately transmit other corresponding packets in the buffer without having to wait for the buffer to be full.
* RST: Reset bit. When `RST = 1, it indicates that there is a serious error in the TCP connection (such as due to a host crash or other reasons). The connection must be released before the transport connection is re-established.
* SYN: Synchronous bit. When SYN is set to 1, it means that this is a connection request or connection acceptance message. Usually a packet with the SYN flag means "active" to connect to the other party.
* FIN: Final bit (Final), used to release a connection. When `FIN ＝ 1`, it indicates that the data of the sending end of this segment has been sent, and the transport connection is required to be released.

#### UDP

* UDP (User Datagram Protocol, User Datagram Protocol) is a connectionless transport layer protocol in the OSI (Open System Interconnection) reference model, which provides a simple and unreliable transaction-oriented information transmission service, and its transmission unit Is a user datagram.

feature:
* not connected
* Do your best to deliver
* Message oriented
* No congestion control
* Support one-to-one, one-to-many, many-to-one, many-to-many interactive communication
* Low overhead

UDP message structure

! [UDP message] (https://raw.githubusercontent.com/huihut/interview/master/images/UDP message.png)

UDP header

! [UDP Header] (https://raw.githubusercontent.com/huihut/interview/master/images/UDPHeader.png)

> TCP / UDP pictures from: <https://github.com/JerryC8080/understand-tcp-udp>

#### The difference between TCP and UDP

1. TCP is connection-oriented, UDP is connectionless;
2. TCP provides reliable services, that is, the data transmitted through the TCP connection is error-free, not lost, not repeated, and arrives in sequence; UDP does its best to deliver, that is, reliable delivery is not guaranteed
3. The logical communication channel of TCP is a full-duplex reliable channel; UDP is an unreliable channel
5. Each TCP connection can only be point-to-point; UDP supports one-to-one, one-to-many, many-to-one and many-to-many interactive communication
6. TCP is oriented to byte stream (probably sticky packet problem), in fact, TCP treats data as a series of unstructured byte stream; UDP is packet-oriented (no sticky packet problem)
7. UDP has no congestion control, so network congestion will not reduce the sending rate of the source host (useful for real-time applications, such as IP phones, real-time video conferencing, etc.)
8. TCP header overhead is 20 bytes; UDP header overhead is small, only 8 bytes

#### TCP sticky problem

##### the reason

TCP is a transmission service based on byte stream (UDP is based on message), "stream" means that the data transmitted by TCP has no boundaries. So there may be two data packets stuck together.

##### Solve

* Send fixed length packets. If the size of each message is the same, as long as the receiving peer accumulates the received data until the data equals a fixed length value, it will be regarded as a message.
* Baotou plus body length. The packet header is 4 bytes of fixed length, indicating the length of the packet body. The receiving peer first receives the packet header length and receives the packet body according to the packet header length.
* Set boundaries between data packets, such as adding special symbols `\ r \ n` marks. The FTP protocol does just that. But the problem is that if the data body also contains `\ r \ n`, it will be mistaken as the boundary of the message.
* Use more complex application layer protocols.

#### TCP flow control

##### Concept

Flow control is to make the sending rate of the sender not too fast, but to allow the receiver to receive it.

##### Methods

Variable window for flow control

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/Example of using variable windows for flow control.png)

#### TCP congestion control

##### Concept

Congestion control is to prevent excessive data from being injected into the network, so that the routers or links in the network will not be overloaded.

##### Methods

* Slow start (slow-start)
* Congestion avoidance (congestion avoidance)
* Fast retransmit (fast retransmit)
* Fast recovery (fast recovery)

TCP congestion control diagram

! [] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP congestion window cwnd changes during congestion control.png)
! [] (https://raw.githubusercontent.com/huihut/interview/master/images/fast retransmission schematic.png)
! [] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP congestion control flowchart.png)

#### TCP transmission connection management

> Because it is important for TCP to establish a connection with three handshake and to release the connection with four waves, attach a detailed description of this chapter in the book "Computer Network (7th Edition)-Xie Xiren": huihut / interview / master / images / TCP-transport-connection-management.png>

##### TCP three-way handshake to establish a connection

! [UDP message] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP three-way handshake to establish a connection.png)

[Explain the whole process of TCP connection establishment]

1. The client sends a SYN to the server, indicating that the client requests to establish a connection;
2. The server receives the SYN sent by the client and replies with SYN + ACK to the client (agreeing to establish a connection);
3. After receiving the SYN + ACK from the server, the client responds with an ACK to the server (indicating that the client received the consent message sent by the server);
4. The server receives the ACK from the client, the connection is established, and data transmission is possible.

##### Why does TCP have to shake hands three times?

[Answer One] Because the channel is unreliable, and TCP wants to establish a reliable transmission on the unreliable channel, then three communications is the theoretical minimum. (And UDP does not need to establish a reliable transmission, so UDP does not require a three-way handshake.)

> [Google Groups. Why is TCP a three-way handshake to establish a connection? {Technology} {Network Communication}] (https://groups.google.com/forum/#!msg/pongba/kF6O7-MFxM0/5S7zIJ4yqKUJ)

[Answer II] Because both parties need to confirm that the other party has received the serial number sent by themselves, the confirmation process requires at least three communications.

> [Know. Why is TCP a three-way handshake instead of two or four? ] (https://www.zhihu.com/question/24853633/answer/115173386)

[Answer three] In order to prevent the invalid connection request segment from being sent to the server suddenly, an error is generated.

> ["Computer Network (7th Edition) -Xie Xiren"] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP-transport-connection-management.png)

##### TCP four waves to release the connection

! [UDP message] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP four waves to release the connection.png)

[Explain the whole process of TCP release connection]

1. The client sends FIN to the server, indicating that the client does not need to send data to the server (request to release the connection from the client to the server);
2. The server receives the FIN sent by the client and replies ACK to the client (agreeing to release the connection from the client to the server);
3. The client receives the ACK from the server, and the connection from the client to the server is released (but the connection from the server to the client has not been released, and the client can still receive data)
4. The server continues to send the unfinished data to the client;
5. The server sends FIN + ACK to the client, indicating that the server has sent the data (request to release the connection from the server to the client, even if no reply is received from the client, it will be automatically released after a certain period of time)
6. The client receives the FIN + ACK from the server and replies to the client with an ACK (agreeing to release the connection from the server to the client);
7. After receiving the ACK from the client, the server releases the connection from the server to the client.

##### Why does TCP have to wave four times?

[Question 1] Why does TCP wave four times? / Why does TCP need three times to establish a connection and four times to release a connection?

[Answer One] Because TCP is in full-duplex mode, after the client requests to close the connection, the connection from the client to the server is closed (one or two waves), and the server continues to transmit the data that has not been previously transmitted to the client (data transmission) , The connection from the server to the client is closed (waving three or four times). Therefore, when TCP releases the connection, the server's ACK and FIN are sent separately (with data transmission in between), and when the TCP establishes the connection, the server's ACK and SYN are sent together (second handshake), so TCP requires three connections It takes four times to release the connection.

[Question 2] Why can ACK and SYN be sent together when TCP is connected, and ACK and FIN are sent separately when released? (ACK and FIN refer to the second and third wave)

[Answer 2:] When the client requests the release, the server may still have data to transmit to the client, so the server must respond to the client FIN request (the server sends an ACK), and then the data is transmitted. After the transmission is completed, the server then Make a FIN request (the server sends FIN); there is no intermediate data transmission when connecting, so ACK and SYN can be sent together when connecting.

[Question three] Why does the client need TIME-WAIT to wait for 2MSL at the end?

【Answer three】

1. In order to ensure that the last ACK message sent by the client can reach the server. If it fails to arrive, the server will retransmit the FIN + ACK segment overtime, and the client will retransmit the ACK and re-time.
2. Prevent invalid connection request segments from appearing in this connection. When TIME-WAIT lasts 2MSL, all the segments generated during the duration of this connection will disappear from the network, so that the old connection segments will not appear in the next connection.

#### TCP finite state machine

TCP finite state machine picture

! [TCP's finite state machine] (https://raw.githubusercontent.com/huihut/interview/master/images/TCP's finite state machine.png)

### Application layer

#### DNS

* DNS (Domain Name System) is a service of the Internet. It serves as a distributed database that maps domain names and IP addresses to each other, enabling people to access the Internet more conveniently. DNS uses TCP and UDP port 53. Currently, the limit for the length of each domain name is 63 characters, and the total length of the domain name cannot exceed 253 characters.

domain name:
* `Domain name :: = {<third-level domain name>. <Second-level domain name>. <Top-level domain name>}`, for example: `blog.huihut.com`

#### FTP

* FTP (File Transfer Protocol, file transfer protocol) is a set of standard protocols for file transfer on the network, using the client / server model, using TCP datagrams, providing interactive access, bidirectional transmission.
* TFTP (Trivial File Transfer Protocol) is a small and easy-to-implement file transfer protocol. It also uses the client-server approach and uses UDP datagrams. It only supports file transfers but not interactions. User authentication

#### TELNET

* The TELNET protocol is a member of the TCP / IP protocol family and is the standard protocol and main method of the Internet remote login service. It provides users with the ability to complete remote host work on the local computer.

* HTTP (HyperText Transfer Protocol) is a transfer protocol used to transfer hypertext from a WWW (World Wide Web, World Wide Web) server to a local browser.

* SMTP (Simple Mail Transfer Protocol) is a set of rules for transferring mail from the source address to the destination address, which controls the transfer method of the letter. The SMTP protocol belongs to the TCP / IP protocol suite, which helps each computer find the next destination when sending or transferring letters.
* Socket requires at least a pair of port numbers (Socket) to establish a network communication connection. Socket is essentially a programming interface (API), which encapsulates TCP / IP. TCP / IP also provides an interface that programmers can use for network development. This is the Socket programming interface.

#### WWW

* WWW (World Wide Web, World Wide Web, World Wide Web) is a system composed of many hypertext links to each other, accessed via the Internet

##### URL

* URL (Uniform Resource Locator) is a standard resource address (Address) on the Internet

standard format:

* `Protocol type: [// server address [: port number]] [/ resource level UNIX file path] file name [? Query] [# Clip ID]
    
Complete format:

* `Protocol type: [// [Credential information required to access resources @] server address [: port number]] [/ resource level UNIX file path] file name [? Query] [# 段 ID]`

> Among them [access credential information @ ;: port number ;? query; #fragment ID] are all optional items
> For example: `https: // github.com / huihut / interview # cc`

##### HTTP

HTTP (HyperText Transfer Protocol) is an application layer protocol for distributed, collaborative, and hypermedia information systems. HTTP is the foundation of data communication on the World Wide Web.

Request method

Method | Significance
--- | ---
OPTIONS | Request some option information to allow the client to view the server's performance
GET | Request the specified page information and return the entity body
HEAD | Similar to the get request, but there is no specific content in the returned response, used to get the header
POST | Submit data to a specified resource for processing requests (such as submitting a form or uploading a file). The data is contained in the request body. POST requests may result in the creation of new resources and / or modification of existing resources
PUT | The data transmitted from the client to the server replaces the content of the specified document
DELETE | Request the server to delete the specified page
TRACE | Echo the request received by the server, mainly used for testing or diagnosis

Status code (Status-Code)

* 1xx: indicates notification information, such as the request received or being processed
    * 100 Continue: continue, the client should continue its request
    * 101 Switching Protocols. The server switches the protocol according to the client's request. You can only switch to a more advanced protocol, for example, to a new version of HTTP
* 2xx: indicates success, if received or known
    * 200 OK: The request was successful
* 3xx: indicates redirection, further action must be taken to complete the request
    * 301 Moved Permanently: Move permanently. The requested resource has been permanently moved to the new URL, the returned information will include the new URL, and the browser will automatically be directed to the new URL. Any new requests in the future should use the new URL instead
* 4xx: indicates the customer's error, such as wrong syntax in the request or failure to complete
    * 400 Bad Request: The syntax of the client request is wrong, the server cannot understand
    * 401 Unauthorized: request for user authentication
    * 403 Forbidden: The server understands the request from the client, but refuses to execute the request (inadequate authority)
    * 404 Not Found: The server cannot find the resource (web page) according to the client's request. With this code, the website designer can set a personalized page of "The resource you requested cannot be found"
    * 408 Request Timeout: The server waits too long for the request sent by the client, timeout
* 5xx: indicates an error of the server, such as the server fails to complete the request
    * 500 Internal Server Error: Internal server error, unable to complete the request
    * 503 Service Unavailable: Due to overload or system maintenance, the server is temporarily unable to process client requests. The length of the delay can be included in the Retry-After header of the server
    * 504 Gateway Timeout: acting as a gateway or proxy server, not getting requests from remote servers in time
> 更多状态码：[菜鸟教程 . HTTP状态码](http://www.runoob.com/http/http-status-codes.html)

##### Other agreements

* SMTP (Simple Main Transfer Protocol) is a standard for transmitting Email on the Internet and is a relatively simple text-based protocol. One or more recipients of a message are specified on it (in most cases it is confirmed to exist), and then the message text is transmitted. You can easily test an SMTP server through the Telnet program. SMTP uses TCP port 25.
* DHCP (Dynamic Host Configuration Protocol) is a network protocol of a local area network. It uses UDP protocol to work and has two main purposes:
    * For internal network or network service providers to automatically assign IP addresses to users
    * Used by internal network administrators as a means of central management of all computers
* SNMP (Simple Network Management Protocol) constitutes a part of the Internet protocol family defined by the Internet Engineering Task Force (IETF). The protocol can support a network management system to monitor whether the devices connected to the network have any management concerns.

## 🌩 Network programming

### Socket

> [Linux Socket programming (not limited to Linux)] (https://www.cnblogs.com/skynet/archive/2010/12/12/1903949.html)

! [Socket client server communication] (https://raw.githubusercontent.com/huihut/interview/master/images/socket client server communication.jpg)


#### Socket read () and write () functions

`` `cpp
ssize_t read (int fd, void * buf, size_t count);
ssize_t write (int fd, const void * buf, size_t count);
`` `

##### read ()

* The read function is responsible for reading content from fd.
* When the read is successful, read returns the actual number of bytes read.
* If the returned value is 0, it means that the end of the file has been read, and if it is less than 0, an error has occurred.
* If the error is EINTR, the reading is caused by interruption; if it is ECONNREST, there is a problem with the network connection.

##### write ()

* The write function writes the contents of nbytes in buf to the file descriptor fd.
* Returns the number of bytes written when successful. On failure, it returns -1 and sets the errno variable.
* In network programs, there are two possibilities when we write to the socket file descriptor.
* (1) The return value of write is greater than 0, indicating that part or all of the data has been written.
* (2) The returned value is less than 0, and an error has occurred at this time.
* If the error is EINTR, it indicates that an interruption error occurred during writing; if it is EPIPE, it indicates that there is a problem with the network connection (the other party has closed the connection).

#### TCP three-way handshake in socket to establish connection

We know that TCP establishes a connection by performing a "three-way handshake", that is, exchanging three packets. The general process is as follows:

1. The client sends a SYN J to the server
2. The server responds to the client with a SYN K, and confirms SYN J ACK J + 1
3. The client wants the server to send an acknowledgement ACK K + 1

Only the three-way handshake is finished, but what about the three-way handshake in the socket function? Please see the picture below:

! [TCP three-way handshake sent in socket] (http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157467258.png)

It can be seen from the figure:
1. When the client calls connect, a connection request is triggered and a SYN J packet is sent to the server. At this time, connect enters a blocking state;
2. The server listens to the connection request, that is, receives the SYN J packet, calls the accept function to receive the request and sends SYN K and ACK J + 1 to the client, then accept enters the blocking state;
3. After the client receives the SYN K of the server, ACK J + 1, connect returns at this time, and confirms the SYN K;
4. When the server receives ACK K + 1, accept returns, so that the three handshake is completed and the connection is established.

#### TCP four-way handshake in socket to release connection

The above describes the three-way handshake establishment process of TCP in socket and the socket functions involved. Now we introduce the process of releasing the connection by the four-way handshake in the socket, please see the following figure:

! [TCP four-way handshake sent in socket] (http://images.cnblogs.com/cnblogs_com/skynet/201012/201012122157487616.png)

The illustrated process is as follows:

1. An application process first calls close to actively close the connection, then TCP sends a FIN M;
2. After receiving the FIN M, the other end performs a passive close to confirm the FIN. Its reception is also passed to the application process as an end-of-file character, because the reception of FIN means that the application process can no longer receive additional data on the corresponding connection;
3. After a period of time, the application process that received the end-of-file character calls close to close its socket. This causes its TCP to also send a FIN N;
4. The source TCP that received the FIN confirms it.

So there is a FIN and ACK in each direction.

## 💾 Database

> Some knowledge points in this section come from "Introduction to Database System (5th Edition)"

### basic concept

* Data (data): Symbolic records describing things are called data.
* Database (DataBase, DB): It is a collection of large amounts of organized, sharable data stored in the computer for a long time. It has three basic characteristics of permanent storage, organization and sharing.
* Database management system (DataBase Management System, DBMS): It is a layer of data management software between the user and the operating system.
* Database system (DataBase System, DBS): It is a system for storing, managing, processing and maintaining data composed of databases, database management systems (and their application development tools), applications and database administrators (DataBase Administrator DBA)
* Entity (entity): things that exist objectively and can be distinguished from each other are called entities.
* Attribute (attribute): An attribute possessed by an entity is called an attribute.
* Code (key): The attribute set that uniquely identifies an entity is called a code.
* Entity type (entity type): use entity name and its attribute name set to abstract and portray similar entities, called entity type.
* Entity set (entity set): a collection of the same entity type is called an entity set.
* Relationship (relationship): The relationship between entities usually refers to the relationship between different sets of entities.
* Schema (schema): Schema is also called logical schema. It is a description of the logical structure and characteristics of all data in the database. It is a common data view of all users.
* External schema (external schema): External schema is also called subschema or user schema. It is a description of the logical structure and characteristics of local data that database users (including application programmers and end users) can see and use The data view of a database user is a logical representation of data related to an application.
* Internal schema (internal schema): internal schema is also called storage schema (storage schema), a database has only one internal schema. He is a description of the physical structure and storage method of the data, and the way the database is organized within the database.

### Common data models

* Hierarchical model
* Network model (network model)
* Relational model
    * Relationship (relation): a relationship corresponds to a table usually said
    * Tuple (tuple): a row in the table is a tuple
    * Attribute (attribute): a column in the table is an attribute
    * Key (key): a certain attribute group of a tuple can be uniquely determined in the table
    * Domain (domain): a set of values ​​with the same data type
    * Component: an attribute value in the tuple
    * Relationship mode: the description of the relationship, generally expressed as `relationship name (attribute 1, attribute 2, ..., attribute n)`
* Object oriented data model (object oriented data model)
* Object relational data model
* Semi-structured data model (semistructure data model)

### Common SQL operations

<table>
  <tr>
    <th> Object type </ th>
    <th> Object </ th>
    <th> Type of operation </ th>
  </ tr>
  <tr>
    <td rowspan = "4"> Database mode </ td>
    <td> Mode </ td>
    <td> <code> CREATE SCHEMA </ code> </ td>
  </ tr>
  <tr>
    <td> Basic table </ td>
    <td> <code> CREATE SCHEMA </ code>, <code> ALTER TABLE </ code> </ td>
  </ tr>
    <tr>
    <td> View </ td>
    <td> <code> CREATE VIEW </ code> </ td>
  </ tr>
    <tr>
    <td> Index </ td>
    <td> <code> CREATE INDEX </ code> </ td>
  </ tr>
    <tr>
    <td rowspan = "2"> Data </ ​​td>
    <td> Basic tables and views </ td>
    <td> <code> SELECT </ code>, <code> INSERT </ code>, <code> UPDATE </ code>, <code> DELETE </ code>, <code> REFERENCES </ code>, <code > ALL PRIVILEGES </ code> </ td>
  </ tr>
    <tr>
    <td> Attribute column </ td>
    <td> <code> SELECT </ code>, <code> INSERT </ code>, <code> UPDATE </ code>, <code> REFERENCES </ code>, <code> ALL PRIVILEGES </ code> </ td>
  </ tr>
</ table>

> SQL syntax tutorial: [runoob. SQL tutorial] (http://www.runoob.com/sql/sql-tutorial.html)

### Relational Database

* Basic relation operations: query (selection, projection, connection (equivalent connection, natural connection, outer connection (left outer connection, right outer connection)), division, union, difference, intersection, Cartesian product, etc.), insertion, deletion ,modify
* Three types of integrity constraints in the relational model: entity integrity, referential integrity, user-defined integrity

#### Index

* Database index: sequential index, B + tree index, hash index
* [Data structure and algorithm principle behind MySQL index] (http://blog.codinglabs.org/articles/theory-of-mysql-index.html)

### Database integrity

* The integrity of the database refers to the correctness and compatibility of the data.
    * Integrity: In order to prevent the existence of incompatible semantic (incorrect) data in the database.
    * Security: In order to protect the database from malicious destruction and illegal access.
* Trigger: It is a special event-driven process defined by the user in the relational table.

### Relational Data Theory

* Data dependency is a constraint relationship between attributes and attributes within a relationship, and is a correlation between data that is reflected by the equality of values ​​between attributes.
* The most important data dependence: functional dependence, multi-value dependence.

#### Paradigm

* First Normal Form (1NF): The attribute (field) is the smallest unit that cannot be divided.
* Second Normal Form (2NF): 1NF is satisfied, and each non-primary attribute is completely dependent on the primary key (eliminating the partial functional dependence of 1NF non-primary attribute on the code).
* The third normal form (3NF): meet 2NF, any non-primary attribute does not depend on other non-primary attributes (eliminate the transfer function dependence of 2NF non-primary attributes on the code).
* Boyce-Cord Paradigm (BCNF): meet 3NF, any non-primary attribute can not depend on the primary key subset (eliminate the dependency of 3NF primary attribute on the code part and transfer function).
* Fourth Normal Form (4NF): satisfy 3NF, and there can be non-trivial and non-functional multi-value dependencies between attributes (eliminate 3NF non-trivial and non-functional multi-value dependencies).

### Database recovery

* Transaction: It is a sequence of database operations defined by the user. These operations are either done or not done at all, and are an inseparable unit of work.
* ACID characteristics of things: atomicity, consistency, isolation, continuity.
* Recovery implementation technology: establish redundant data-> use redundant data to implement database recovery.
* Common techniques for establishing redundant data: data dump (dynamic mass dump, dynamic incremental dump, static mass dump, static incremental dump), and log file registration.

### Concurrency control

* Transaction is the basic unit of concurrency control.
* Data inconsistencies caused by concurrent operations include: lost modifications, non-repeatable reads, and reading of "dirty" data.
* Main technologies of concurrency control: blockade, timestamp, optimistic control method, multi-version concurrency control, etc.
* Basic blocking types: exclusive lock (X lock / write lock), shared lock (S lock / read lock).
* Livelock deadlock:
    * Livelock: The transaction is always in a waiting state, which can be avoided by the strategy of first come, first served.
    * Deadlock: Things can never end
        * Prevention: one-time blockade method, sequential blockade method;
        * Diagnosis: timeout method, waiting graph method;
        * Cancellation: Undo the transaction with the lowest deadlock cost and release all the locks of this transaction, so that other transactions can continue to run.
* Serializable scheduling: The concurrent execution of multiple transactions is correct if and only if the result is the same as when these transactions are executed serially in a certain order. Criteria for correct scheduling of concurrent transactions in serializability.

## 📏 Design pattern

> Examples of major design patterns: [CSDN column. C ++ design patterns] (https://blog.csdn.net/liang19890820/article/details/66974516) series of blog posts

[Design Pattern Engineering Directory] (DesignPattern)

### Singleton mode

[Singleton pattern example] (DesignPattern / SingletonPattern)

### Abstract factory pattern

[Abstract factory pattern example] (DesignPattern / AbstractFactoryPattern)

### Adapter mode

[Adapter pattern example] (DesignPattern / AdapterPattern)

### Bridge Mode

[Bridge Pattern Example] (DesignPattern / BridgePattern)

### Observer mode

[Observer pattern example] (DesignPattern / ObserverPattern)

### Six principles of design patterns

* Single Responsibility Principle (SRP)
* Liskov Substitution Principle (LSP)
* Dependency inversion principle (DIP, Dependence Inversion Principle)
* Interface Segregation Principle (ISP)
* Law of Demeter (LoD, Law of Demeter)
* Open Close Principle (OCP, Open Close Principle)

## ⚙️ Link loading library

> Part of the knowledge in this section comes from "Self-cultivation of programmers-link loading library"

### Memory, stack, heap

The general application memory space has the following areas:

* Stack: automatically allocated and released by the operating system, storing function parameter values, local variables, etc., used to maintain the context of the function call
* Heap: Generally allocated and released by the programmer. If the programmer does not release it, it may be recovered by the operating system at the end of the program to accommodate the memory area dynamically allocated by the application.
* Executable file image: stores the image of the executable file in memory, and loading by the loader reads or maps the memory of the executable file here
* Reserved area: The reserved area is not a single memory area, but a general term for the memory area that is protected from access in the memory. For example, usually the C language speaks of an invalid pointer as 0 (NULL), so the 0 address is normal Impossible access to data

#### Stack

The stack saves the maintenance information needed for a function call, often called a stack frame (Stack Frame) or activity record (Activate Record), and generally includes the following aspects:

* The return address and parameters of the function
* Temporary variables: including non-static local variables of functions and other temporary variables automatically generated by the compiler
* Save context: including registers that need to remain unchanged before and after function calls

#### Heap

Heap allocation algorithm:

* Free List (Free List)
* Bitmap
* Object pool

#### "Segment fault" or "Illegal operation, the memory address cannot be read / write"

Typical illegal pointer dereference error. This error occurs when the pointer points to a memory address that is not allowed to read or write, but the program attempts to use the pointer to read or write the address.

Common reasons:

* Initialize the pointer to NULL, and then start using the pointer without giving it a reasonable value
* It is useless to initialize the pointer in the stack, the value of the pointer will generally be a random number, and then the pointer will be used directly.

### Compile link

#### The file format of each platform

Platform | Executable files | Object files | Dynamic libraries / Shared objects | Static libraries
--- | --- | --- | --- | ---
Windows | exe | obj | dll | lib
Unix / Linux | ELF, out | o | so | a
Mac | Mach-O | o | dylib, tbd, framework | a, framework

#### Compile and link process

1. Pre-compilation (the pre-compiler processes pre-compiled instructions such as `# include`,` # define`, etc. to generate `.i` or` .ii` files)
2. Compilation (the compiler performs lexical analysis, grammatical analysis, semantic analysis, intermediate code generation, object code generation, optimization, and generates `.s` files)
3. Assembly (the assembler translates the assembly code into machine code and generates `.o` files)
4. Link (connector performs address and space allocation, symbol resolution, relocation, and generates `.out` files)

> The current version of GCC combines pre-compilation and compilation into one step, pre-compiled compiler cc1, assembler as, linker ld

> MSVC compilation environment, compiler cl, linker link, executable file viewer dumpbin

#### target document

The file generated by the compiler after compiling the source code is called the target file. The target file is structurally speaking, it is an executable file format that has been compiled, but it has not been linked, and some symbols or some addresses may not have been adjusted.

> Executable files (.exe for Windows and ELF for Linux), dynamic link libraries (.dll for Windows and .so for Linux), static link libraries (.lib for Windows and Linux) `.A` are stored in executable file format (Windows according to PE-COFF, Linux according to ELF)

##### Target file format

* Windows PE (Portable Executable), or PE-COFF, `.obj` format
* ELF (Executable Linkable Format) for Linux, `.o` format
* OMF (Object Module Format) of Intel / Microsoft
* Unix `a.out` format
* MS-DOS `.COM` format

> Both PE and ELF are variants of COFF (Common File Format)

##### Target file storage structure

Segment | Function
--- | ---
File Header | File header, describing the file attributes of the entire file (including whether the file is executable, whether it is a static link or a dynamic link and entry address, target hardware, target operating system, etc.)
.text section | Code section, machine code compiled by the execution statement
.data section | Data section, initialized global variables and local static variables
.bss section | BSS section (Block Started by Symbol), uninitialized global variables and local static variables (because the default value is 0, so it is only reserved here and does not occupy space)
.rodata section | read-only data section, which stores read-only data, generally read-only variables (such as const modified variables) and string constants in the program
.comment section | Comment section, which stores compiler version information
.note.GNU-stack section | Stack notes section

> Other sections

#### Linked Interface-Symbol

In the link, the merge of the object files is actually a reference to the address between the object files, that is, a reference to the address of the function and variable. We refer to functions and variables collectively as symbols, and function names or variable names are symbol names.

The following symbol table (Symbol Table):

Symbol (Symbol Name) | Symbol Value (Address)
--- | ---
main | 0x100
Add | 0x123
... | ...

### Shared Library for Linux (Shared Library)

The shared library under Linux is a common ELF shared object.

The shared library version update should ensure the compatibility of the binary interface ABI (Application Binary Interface)

#### Naming

`libname.so.x.y.z`

* x: major version number, incompatible between libraries with different major version numbers, need to be recompiled
* y: minor version number, high version number is backward compatible with low version number
* z: release version number, without changing the interface, fully compatible

#### path

Most open source systems, including Linux, follow the FHS (File Hierarchy Standard) standard, which specifies how system files are stored, including various directory structures, organizations, and functions.

* `/ lib`: store the most critical and basic shared libraries of the system, such as dynamic linker, C language runtime library, math library, etc.
* `/ usr / lib`: store key libraries needed for non-system runtime, mainly development libraries
* `/ usr / local / lib`: store libraries that are not very related to the operating system itself, mainly libraries for some third-party applications

> The dynamic linker will look for shared libraries in the directories specified by `/ lib`,` / usr / lib` and specified by the `/ etc / ld.so.conf` configuration file

#### Environment variables

* `LD_LIBRARY_PATH`: temporarily change the shared library search path of an application without affecting other applications
* `LD_PRELOAD`: Specify some pre-loaded shared libraries or even target files
* `LD_DEBUG`: Turn on the debugging function of the dynamic linker

#### so writing of shared library

Use CLion to write shared libraries

Create a shared library named MySharedLib

CMakeLists.txt

`` `cmake
cmake_minimum_required (VERSION 3.10)
project (MySharedLib)

set (CMAKE_CXX_STANDARD 11)

add_library (MySharedLib SHARED library.cpp library.h)
`` `

library.h

`` `cpp
#ifndef MYSHAREDLIB_LIBRARY_H
#define MYSHAREDLIB_LIBRARY_H

// print Hello World!
void hello ();

// Sum using variable template parameters
template <typename T>
T sum (T t)
{
    return t;
}
template <typename T, typename ... Types>
T sum (T first, Types ... rest)
{
    return first + sum <T> (rest ...);
}

#endif
`` `

library.cpp

`` `cpp
#include <iostream>
#include "library.h"

void hello () {
    std :: cout << "Hello, World!" << std :: endl;
}
`` `

#### use of so shared library (called by executable project)

Use CLion to call a shared library

Create an executable project named TestSharedLib

CMakeLists.txt

`` `cmake
cmake_minimum_required (VERSION 3.10)
project (TestSharedLib)

# C ++ 11 compile
set (CMAKE_CXX_STANDARD 11)

# Header file path
set (INC_DIR / home / xx / code / clion / MySharedLib)
# Library file path
set (LIB_DIR / home / xx / code / clion / MySharedLib / cmake-build-debug)

include_directories ($ {INC_DIR})
link_directories ($ {LIB_DIR})
link_libraries (MySharedLib)

add_executable (TestSharedLib main.cpp)

# Link to MySharedLib library
target_link_libraries (TestSharedLib MySharedLib)
`` `

main.cpp

`` `cpp
#include <iostream>
#include "library.h"
using std :: cout;
using std :: endl;

int main () {

    hello ();
    cout << "1 + 2 =" << sum (1,2) << endl;
    cout << "1 + 2 + 3 =" << sum (1,2,3) << endl;

    return 0;
}
`` `

Results of the

`` `
Hello, World!
1 + 2 = 3
1 + 2 + 3 = 6
`` `

### Windows application entry function

* GUI (Graphical User Interface) application, linker option: `/ SUBSYSTEM: WINDOWS`
* CUI (Console User Interface) application, linker option: `/ SUBSYSTEM: CONSOLE`

_tWinMain and _tmain function declaration

`` `cpp
Int WINAPI _tWinMain (
    HINSTANCE hInstanceExe,
    HINSTANCE,
    PTSTR pszCmdLine,
    int nCmdShow);

int _tmain (
    int argc,
    TCHAR * argv [],
    TCHAR * envp []);
`` `

Application type | Entry point function | Startup function embedded in executable file
--- | --- | ---
GUI application for handling ANSI characters (strings) | _tWinMain (WinMain) | WinMainCRTSartup
GUI application for handling Unicode characters (strings) | _tWinMain (wWinMain) | wWinMainCRTSartup
CUI application that handles ANSI characters (strings) | _tmain (Main) | mainCRTSartup
CUI application for handling Unicode characters (strings) | _tmain (wMain) | wmainCRTSartup
Dynamic Link Library (Dynamic-Link Library) | DllMain | _DllMainCRTStartup

### Windows Dynamic-Link Library

> Some knowledge points come from "Windows Core Programming (Fifth Edition)"

#### Usefulness

* Expanded application features
* Simplified project management
* Helps save memory
* Promote the sharing of resources
* Promotes localization
* Helps resolve differences between platforms
* Can be used for special purposes

#### Note

* Creating a DLL is actually creating a function that can be called by an executable module
* When a module provides a memory allocation function (malloc, new), it must also provide another memory release function (free, delete)
* When mixing C and C ++, use extern "C" modifier
* A DLL can export functions, variables (avoid export), C ++ classes (export and import need to be the same as the compiler, otherwise avoid export)
* DLL module: __declspec (dllexport) in cpp file is written before include header file
* Executable module calling DLL: MYLIBAPI should not be defined before __declspec (dllimport) of cpp file

#### Search order for loading Windows programs

1. Directory containing executable files
2. The system directory of Windows can be obtained through GetSystemDirectory
3. 16-bit system directory, which is the System subdirectory in the Windows directory
4. The Windows directory can be obtained through GetWindowsDirectory
5. The current directory of the process
6. The directories listed in the PATH environment variable

#### DLL entry function

DllMain function

`` `cpp
BOOL WINAPI DllMain (HINSTANCE hinstDLL, DWORD fdwReason, LPVOID lpvReserved)
{
    switch (fdwReason)
    {
    case DLL_PROCESS_ATTACH:
        // Called when mapping a DLL to the process address space for the first time
        // The DLL is being mapped into the process' address space.
        break;
    case DLL_THREAD_ATTACH:
        // When the process creates a thread, it is used to tell the DLL to perform thread-related initialization (non-main thread execution)
        // A thread is bing created.
        break;
    case DLL_THREAD_DETACH:
        // The system calls ExitThread before the thread exits, the thread that is about to be terminated performs thread-related cleanup by telling the DLL
        // A thread is exiting cleanly.
        break;
    case DLL_PROCESS_DETACH:
        // Called when a DLL is removed from the process's address space
        // The DLL is being unmapped from the process' address space.
        break;
    }
    return (TRUE); // Used only for DLL_PROCESS_ATTACH
}
`` `

#### 载入卸载库

LoadLibrary、LoadLibraryExA、LoadPackagedLibrary、FreeLibrary、FreeLibraryAndExitThread 函数声明

```cpp
// 载入库
HMODULE WINAPI LoadLibrary(
  _In_ LPCTSTR lpFileName
);
HMODULE LoadLibraryExA(
  LPCSTR lpLibFileName,
  HANDLE hFile,
  DWORD  dwFlags
);
// 若要在通用 Windows 平台（UWP）应用中加载 Win32 DLL，需要调用 LoadPackagedLibrary，而不是 LoadLibrary 或 LoadLibraryEx
HMODULE LoadPackagedLibrary(
  LPCWSTR lpwLibFileName,
  DWORD   Reserved
);

// 卸载库
BOOL WINAPI FreeLibrary(
  _In_ HMODULE hModule
);
// 卸载库和退出线程
VOID WINAPI FreeLibraryAndExitThread(
  _In_ HMODULE hModule,
  _In_ DWORD   dwExitCode
);
```

#### 显示地链接到导出符号

GetProcAddress 函数声明

```cpp
FARPROC GetProcAddress(
  HMODULE hInstDll,
  PCSTR pszSymbolName  // 只能接受 ANSI 字符串，不能是 Unicode
);
```

#### DumpBin.exe 查看 DLL 信息

在 `VS 的开发人员命令提示符` 使用 `DumpBin.exe` 可查看 DLL 库的导出段（导出的变量、函数、类名的符号）、相对虚拟地址（RVA，relative virtual address）。如：
```
DUMPBIN -exports D:\mydll.dll
```

#### LoadLibrary 与 FreeLibrary 流程图

LoadLibrary 与 FreeLibrary 流程图

##### LoadLibrary

![WindowsLoadLibrary](https://raw.githubusercontent.com/huihut/interview/master/images/WindowsLoadLibrary.png)

##### FreeLibrary

![WindowsFreeLibrary](https://raw.githubusercontent.com/huihut/interview/master/images/WindowsFreeLibrary.png)

#### DLL 库的编写（导出一个 DLL 模块）

DLL 库的编写（导出一个 DLL 模块）
DLL 头文件

```cpp
// MyLib.h

#ifdef MYLIBAPI

// MYLIBAPI 应该在全部 DLL 源文件的 include "Mylib.h" 之前被定义
// 全部函数/变量正在被导出

#else

// 这个头文件被一个exe源代码模块包含，意味着全部函数/变量被导入
#define MYLIBAPI extern "C" __declspec(dllimport)

#endif

// 这里定义任何的数据结构和符号

// 定义导出的变量（避免导出变量）
MYLIBAPI int g_nResult;

// 定义导出函数原型
MYLIBAPI int Add(int nLeft, int nRight);
```

DLL 源文件

```cpp
// MyLibFile1.cpp

// 包含标准Windows和C运行时头文件
#include <windows.h>

// DLL源码文件导出的函数和变量
#define MYLIBAPI extern "C" __declspec(dllexport)

// 包含导出的数据结构、符号、函数、变量
#include "MyLib.h"

// 将此DLL源代码文件的代码放在此处
int g_nResult;

int Add(int nLeft, int nRight)
{
    g_nResult = nLeft + nRight;
    return g_nResult;
}
```

#### DLL 库的使用（运行时动态链接 DLL）

DLL 库的使用（运行时动态链接 DLL）

```cpp
// A simple program that uses LoadLibrary and 
// GetProcAddress to access myPuts from Myputs.dll. 
 
#include <windows.h> 
#include <stdio.h> 
 
typedef int (__cdecl *MYPROC)(LPWSTR); 
 
int main( void ) 
{ 
    HINSTANCE hinstLib; 
    MYPROC ProcAdd; 
    BOOL fFreeResult, fRunTimeLinkSuccess = FALSE; 
 
    // Get a handle to the DLL module.
 
    hinstLib = LoadLibrary(TEXT("MyPuts.dll")); 
 
    // If the handle is valid, try to get the function address.
 
    if (hinstLib != NULL) 
    { 
        ProcAdd = (MYPROC) GetProcAddress(hinstLib, "myPuts"); 
 
        // If the function address is valid, call the function.
 
        if (NULL != ProcAdd) 
        {
            fRunTimeLinkSuccess = TRUE;
            (ProcAdd) (L"Message sent to the DLL function\n"); 
        }
        // Free the DLL module.
 
        fFreeResult = FreeLibrary(hinstLib); 
    } 

    // If unable to call the DLL function, use an alternative.
    if (! fRunTimeLinkSuccess) 
        printf("Message printed from executable\n"); 

    return 0;
}
```
### Runtime Library (Runtime Library)

#### Typical program operation steps

1. The operating system creates a process and gives control to the entrance of the program (often an entry function in the runtime)
2. The entry function initializes the runtime library and the running environment of the program (including heap, I / O, threads, global variable construction, etc.).
3. After the entry function is initialized, the main function is called, and the main part of the program is officially started.
4. After the main function is executed, return to the entry function for cleaning (including global variable destructuring, heap destruction, and closing I / O, etc.), and then make a system call to end the process.

> I / O of a program refers to the interaction between the program and the outside world, including files, management procedures, networks, command lines, signals, etc. More broadly, I / O refers to what the operating system understands as a "file".

#### glibc entrance

`_start-> __libc_start_main-> exit-> _exit`

The `main (argc, argv, __environ)` function is executed in `__libc_start_main`.

#### MSVC CRT entrance

`int mainCRTStartup (void)`

Perform the following operations:

1. Initialize the global variables related to the OS version.
2. Initialize the heap.
3. Initialize I / O.
4. Get command line parameters and environment variables.
5. Initialize some data of the C library.
6. Call main and record the return value.
7. Check for errors and return the return value of main.

#### C language runtime (CRT)

Roughly includes the following functions:

* Start and exit: Including entry function and other functions on which entry function depends.
* Standard functions: There are functions realized by the C language standard library specified by the C language standard.
* I / O: encapsulation and implementation of I / O functions.
* Heap: encapsulation and implementation of the heap.
* Language realization: the realization of some special functions in the language
* Debugging: code to realize the debugging function.

#### C language standard library (ANSI C)

contain:

* Standard input and output (stdio.h)
* File operation (stdio.h)
* Character operation (ctype.h)
* String operation (string.h)
* Mathematical functions (math.h)
* Resource management (stdlib.h)
* Format conversion (stdlib.h)
* Time / date (time.h)
* Assertions (assert.h)
* Constants of various types (limits.h & float.h)
* Variable length parameter (stdarg.h)
* Non-local jump (setjmp.h)

## 📚 Books

> [huihut / CS-Books] (https://github.com/huihut/CS-Books): 📚 Computer Science Books Computer Technology Books PDF

### Language

* "C ++ Primer"
* "Effective C ++"
* "More Effective C ++"
* "Deep Exploration of C ++ Object Model"
* "In-depth understanding of C ++ 11"
* "Analysis of STL source code"

### Algorithm

* "Sword Finger Offer"
* "Programming Pearl"
* "Programmer Interview Collection"

### System

* "In-depth understanding of computer systems"
* "Windows Core Programming"
* "Advanced Programming in Unix Environment"

### The internet

* "Unix Network Programming"
* "Detailed Explanation of TCP / IP"

### Other

* "Self-cultivation of programmers"

## 🔱 C / C ++ development direction

> The development direction of C / C ++ is very broad, including but not limited to the following directions. Here are some requirements for recruiting positions in large factories.

### Background / Server

【Background Development】

* Solid programming skills, master C / C ++ / JAVA and other development languages, commonly used algorithms and data structures;
* Familiar with TCP / UDP network protocol and related programming, inter-process communication programming;
* Understand scripting languages ​​such as Python, Shell, Perl;
* Understand MYSQL and SQL language, programming, understand NoSQL, key-value storage principle;
* Comprehensive and solid software knowledge structure, master professional knowledge of operating system, software engineering, design mode, data structure, database system, network security, etc .;
* Understand the knowledge of distributed system design and development, load balancing technology, system disaster tolerance design, high availability system, etc.

### Desktop Client

[PC client development]

* Bachelor degree or above in computer software related major, love programming, solid foundation, understand algorithms and data structure related knowledge;
* Familiar with memory management, file system, process thread scheduling of windows operating system;
* Familiar with MFC / windows interface implementation mechanism, proficient in VC, proficient in C / C ++, proficient in STL, and network programming experience under Windows;
* Proficiency in Windows client development and debugging, experience in Windows application software development is preferred;
* Passionate about innovation and solving challenging problems, with good algorithm foundation and system analysis ability.

### Graphics / Games / VR / AR

[Game client development]

* Bachelor degree or above in computer science / engineering related major, love programming, solid foundation, understand algorithms, data structure, software design related knowledge
* Master at least one programming language commonly used in game development, with C ++ / C # programming experience preferred;
* Experience with game engine (such as Unity, Unreal) is preferred;
* Those who understand certain aspects of game client technology (such as graphics, audio, animation, physics, artificial intelligence, network synchronization) are preferred;
* Passionate about innovating and solving challenging problems, strong learning ability, analysis and problem solving ability, and good sense of teamwork;
* Ability to read English technical documents;
* Love games.

### Test development

【Test Development】

* Bachelor degree or above in computer or related major;
* One to two years of programming experience in C / C ++ / Python or other computer languages;
* Ability to write test plans, test cases, and implement performance and safety tests;
* Have the ability to realize the automation system;
* Ability to locate and investigate product defects, and the ability to debug defects at the code level;
* Proactive work, responsible, with a good teamwork spirit.

### Cybersecurity / Reverse

【safety technology】

* Passionate about the Internet, passionate pursuit of operating system and network security, no limit to professional;
* Familiar with vulnerability mining, network security offensive and defensive technologies, and understand common hacker attacks;
* Master basic development ability, proficient in C / C ++ language;
* Have a good grasp of database, operating system, network principles;
* Experience in software reverse, network security offensive and defensive or security system development is preferred.

### Embedded / Internet of Things

【Embedded Application Development】

* Have a good programming foundation, proficient in C / C ++ language;
* Master the necessary knowledge of software development such as operating system and data structure;
* Possess strong communication and understanding ability and good sense of teamwork;
* Those with Linux / Android system platform development experience are preferred.

### Audio / Video / Streaming Media / SDK

【Audio and video codec】

1. Master degree or above, computer, signal processing, mathematics, information and related majors and directions;
2. The video coding and decoding foundation is solid, and the commonly used HEVC or H264 has a good digital signal processing foundation;
3. Master C / C ++, strong code ability, familiar with an assembly language is preferred;
4. Strong reading ability in English literature;
5. Strong learning ability, teamwork spirit and strong anti-stress ability.

### Computer Vision / Machine Learning

【Computer Vision Research】

* Computer, applied mathematics, pattern recognition, artificial intelligence, automatic control, statistics, operations research, biological information, physics / quantum computing, neuroscience, sociology / psychology, etc., image processing, pattern recognition, machine learning related research Orientation, bachelor degree or above, Ph.D. is preferred;
* Proficient in basic algorithms and applications related to computer vision and image processing;
* Strong algorithm implementation ability, proficient in C / C ++ programming, familiar with Shell / Python / Matlab at least one programming language;
* Papers published in academic conferences or journals such as computer vision, pattern recognition, related international competition awards, and related patents are preferred.

## 💯 Review brush question website

* [cplusplus] (http://www.cplusplus.com/)
* [cppreference] (https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5)
* [runoob] (http://www.runoob.com/cplusplus/cpp-tutorial.html)
* [leetcode] (https://leetcode.com/) | [leetcode-cn] (https://leetcode-cn.com/)
* [lintcode] (https://www.lintcode.com/)
* [nowcoder] (https://www.nowcoder.net/)

## 📝 Interview question experience

* [Niu Ke.. 2020 Autumn Recruitment Noodles Summary! (Post division)] (https://www.nowcoder.com/discuss/205497)
* [Niuke.com] [Preparation for Autumn Tricks] Strategy for 2020 Autumn Tricks] (https://www.nowcoder.com/discuss/197116)
* [Niuke.com 2019 School Recruitment Summary! [Daily Update]] (https://www.nowcoder.com/discuss/90907)
* [Niuke.com 2019 School Recruitment Technology Posts Summary [Technology]] (https://www.nowcoder.com/discuss/146655)
* [Niu Ke.. Summary of 2018 School Recruitment Written Test Questions] (https://www.nowcoder.com/discuss/68802)
* [Niu Ke.. The 2017 Autumn Campus Recruitment Pen Jing Face Special Topic Summary] (https://www.nowcoder.com/discuss/12805)
* [Niu Ke. The most complete collection of 2017 spring tricks in history! ! ] (https://www.nowcoder.com/discuss/25268)
* [Nukke. Interview questions are here] (https://www.nowcoder.com/discuss/57978)
* [Knowing.. On the Internet job search, what well-written and attentive face have you seen? It is best to share your own facial and mental journey. ] (https://www.zhihu.com/question/29693016)
* [Know. What are the most common interview algorithm questions for internet companies? ] (https://www.zhihu.com/question/24964987)
* [CSDN. C ++ Interview Questions Completely Organized] (http://blog.csdn.net/ljzcome/article/details/574158)
* [CSDN. Baidu R & D interview questions (C ++ direction)] (http://blog.csdn.net/Xiongchao99/article/details/74524807?locationNum=6&fps=1)
* [CSDN. C ++ 30 common interview questions] (http://blog.csdn.net/fakine/article/details/51321544)
* [CSDN. Tencent 2016 intern interview experience (already got offer)] (http://blog.csdn.net/onever_say_love/article/details/51223886)
* [cnblogs. C ++ Interview Collection (Questions Asked for Interview)] (https://www.cnblogs.com/Y1Focus/p/6707121.html)
* [cnblogs. C / C ++ written and interview questions summary] (https://www.cnblogs.com/fangyukuan/archive/2010/09/18/1829871.html)
* [cnblogs. Summary of common C ++ interview questions and basic knowledge points (1)] (https://www.cnblogs.com/LUO77/p/5771237.html)
* [segmentfault. Summary of common interview questions in C ++] (https://segmentfault.com/a/1190000003745529)

## 📆 Recruiting time posts

* [Niuke.com 2020 School Recruitment | 2020 IT Enterprise Recruitment Schedule] (https://www.nowcoder.com/school/schedule)

## 👍 Recommend

* [Github. CyC2018 / Job-Recommend] (https://github.com/CyC2018/Job-Recommend): 🔎 Internet internal push information (social recruitment, school recruitment, internship)
* [Github. Amusi / AI-Job-Recommend] (https://github.com/amusi/AI-Job-Recommend): direction of artificial intelligence of domestic companies (including machine learning, deep learning, computer vision and natural language processing) Job recruitment information (including full-time, internship and school recruitment)

## 👬 Contributors

Including Issues and PRs for errata, sorted according to contribution time.

[tamarous] (https://github.com/tamarous), [i0Ek3] (https://github.com/i0Ek3), [sniper00] (https://github.com/sniper00), [blackhorse001] (https : //github.com/blackhorse001), [houbaron] (https://github.com/houbaron), [Qouan] (https://github.com/Qouan), [2329408386] (https://github.com com / 2329408386), [FlyingfishMORE] (https://github.com/FlyingfishMORE), [Ematrix163] (https://github.com/Ematrix163), [ReturnZero23] (https://github.com/ReturnZero23), [kelvinkuo] (https://github.com/kelvinkuo), [henryace] (https://github.com/henryace), [xinghun] (https://github.com/xinghun), [maokelong] (https : //github.com/maokelong), [easyYao] (https://github.com/easyYao), [FengZiYjun] (https://github.com/FengZiYjun), [shangjiaxuan] (https://github.com com / shangjiaxuan), [kwongtailau] (https://github.com/kwongtailau), [asky991] (https://github.com/asky991), [traviszeng] (https://github.com/traviszeng), [kele1997] (https://github.com/kele1997), [hxdnshx] (https://github.com/hxdnshx), [a74731248] (https://github.com/a 74731248), [qvjp] (https://github.com/qvjp), [xindelvcheng] (https://github.com/xindelvcheng), [hbsun2113] (https://github.com/hbsun2113), [linkwk7 ] (https://github.com/linkwk7), [foolishflyfox] (https://github.com/foolishflyfox), [zhjp0] (https://github.com/zhjp0), [Mrtj2016] (https: / /github.com/Mrtj2016)

## 🍭 Support sponsorship

Reward me for a pack of spicy strips ~

! [Huihut-AliPay] (https://huihut-img.oss-cn-shenzhen.aliyuncs.com/Huihut-AliPay-H370.png)! [Huihut-WeChatPay] (https: //huihut-img.oss- cn-shenzhen.aliyuncs.com/Huihut-WeChatPay-H370.png)

## 📜 License

This warehouse follows the CC BY-NC-SA 4.0 (signed-non-commercial use-sharing in the same way) agreement, please indicate the source for reprinting, and may not be used for commercial purposes.

[! [CC BY-NC-SA 4.0] (https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)] (LICENSE)
