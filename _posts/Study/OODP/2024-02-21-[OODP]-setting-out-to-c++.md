---
layout: post
title: "[OODP] 1. Setting out to C++"
category: study
tags: OODP
---

> POSTECH OODP Lecture at 24SS

## Function Header

> **int main(void)** is very explicit style of function header.

C++ compiler adds the startup code which calls the main function. In effect, the function header of main describes the interface between **main( )** and the operating system.
The function header informs the function return type and argument list or parameter list.

## The C++ Preprocessor

A program that processes a source file before the main compilation. Preprocessor directives start with **#**. Typical preprocessor action is adding or replacing text in source code before compilation.
```C++
// a.cc
int func()
{
    return 1;
}
// b.cc
#include "a.cc"
#define Zero 0
int main()
{
    return Zero;
}

// Preprocessor output
int func()
{
    return 1;
}
int main()
{
    return 0;
}
```
Preprocessor
- removes comments
- adds the content of "a.cc" into "b.cc"
- replaces macro constants defined by '#define' with what they actually are.

```C++
#include <iostream> // a preprocessor directive

int main()
{
    using namespace std; // make definitions visible
    cout << "Come up and C++ me some time." << endl;
    return 0;
}
```
- **iostream** : A header file of the c++ standard library. Contains declarations for the identifier **cout** and the operator **<<**. <br>
Standard library header files do not have the extension.
    ex) C++ : iostream, iomanip, fstream, vector, list, deque, memory, algorithm, ...
        C : cstdio(stdio.h), cmath(math.h), cstdlib(stdlibh), ...
- **cout** : a predefined object for the standard output.
    object is an instance of a particular class
- **<<** : an insertion operator to pass the string on the right to the object on the lieft.
- **endl** : a manipulator(기계장치) that represents a new line.
    Defined in the iostream header file.
    Part of the std namespace.
    Do same thing with '\n' in C.
- **std** : namespace directive to use cin, cout, endl.

## Declaration Statements and Variables
A variable is a memory storage to store information.
(파이썬과는 달리)C++에서는 모든 variable들은 반드시 사용되기 전에 선언되어야 한다.

```C++
int carrots = 25;
```
Type(int)
name(carrots)
symbol(=) : assignment operator
```C++
cin >> carrots;
cout << carrots;
```
- **cin** allows you to enter a value while the program is running.

## Function Form