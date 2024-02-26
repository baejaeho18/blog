---
layout: post
title: "[OODP] 0. About C++(2)"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

## Function Header

> **int main(void)** is very explicit style of function header.

C++ compiler adds the startup code which calls the main function. In effect, the function header of main describes the interface between **main( )** and the operating system.
The function header informs the function's return type and argument list or parameter list.

## The C++ Preprocessor

A program that processes a source file before the main compilation. Preprocessor directives start with **'#'**. Typical preprocessor action is adding or replacing text in source code before compilation.
<!--more-->
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
In the above code, preprocessor 
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
- **iostream** : A header file of the c++ standard library. Contains declarations for the identifier **'cout'** and the operator **'<<'**. <br>
Standard library header files do not have the extension.
    * ex) C++ : iostream, iomanip, fstream, vector, list, deque, memory, algorithm, ... <br>
        C : cstdio(stdio.h), cmath(math.h), cstdlib(stdlibh), ...
- **cout** : A predefined object for the standard output.
    * object is an instance of a particular class
    * automatically recognizes the data type of its input. 반면, printf() in C는 data type을 지정해줘야한다.
- **<<** : An insertion operator to pass the string on the right to the object on the lieft.
- **endl** : A manipulator(기계장치) that represents a new line.
    * Defined in the iostream header file.
    * Part of the std namespace.
    - Do same thing with '\n' in C.
- **std** : namespace directive to use cin, cout, endl.

### Declaration Statements and Variables
> A variable is a memory storage to store information.

(파이썬과는 달리) C++에서는 모든 variable들은 반드시 사용되기 전에 선언되어야 한다.

```C++
int carrots = 25;
cin >> carrots;
cout << carrots;
```
- **cin** allows you to enter a value while the program is running.

## Function Form
![calling-function](/assets/img/2024-02-21/calling-function.png)


## Question?
**Q1.** 이전 챕터에서 우리는 C++ 소스코드가 Compiler를 통해 object-code로 변환이 되고, 이것이 Linker를 통해 startup code와 library code가 덧붙여짐으로써 executable-file이 된다는 사실을 배웠다.
그런데 이번 챕터에서 preprocessor라는 개념을 배우며, main compilation이 이뤄지기 전에 preprocessor가 동작한다는 사실을 알았다. 그리고 preprocessor의 #include는 해당 라이브러리 혹은 사용자작성 파일을 불러온다는 것을 알았다. 이것이 Linker가 하는 일이 아닌가?
이 두가지 사실의 모순이 있지 않은지 혼란스럽다.
**A.** 