---
layout: post
title: "[OODP] 2. Compound Types(2)"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

## Compound Types
- Built on basic types.
- Arrays, strings, pointers, structures
<!--more-->

### Strings
> A series of characters stored in consecutive bytes of memory

- C-style string: stores a string in an array of **char**
    - string의 끝을 뜻하는 Null-character('\0')을 반드시 넣어줘야함.
    - C++에서는 string literals 사이에 whitespace(spaces, tabs, and newlines)만 존재한다면 자동으로 합쳐준다.

- string class library

### Structures
> Allow developer to store all the related information of different user-definable types in a single place

```c++
// structure declaration
struct inflatable
{
    char name[20];
    float volume;
    double price;
};

struct inflatable goose;    // keyword struct required in C
inflatable vincent;         // keyword struct not required in C++

struct numbers
{
    float v1;
    double v2;
} a, b;         // can directly declare variables here, too

struct
{
    string name;
    int age;
} ds, jy;       // also can omit type name
```

Structure의 각 member들은 membership operator(.)를 통해 접근 가능하다.
Structure의 초기화는 assignment operator(=)를 사용해 이루어진다.
Structure의 배열을 생성하는 것도 가능하다.  

### Enumberations
> An alternative to **const** for creating symbolic constants. Also lets you define new types but in a fairly restricted fashion

```C++
// Syntax:
enum spectrum {red, orange, yellow, green, blue, violet, indigo, ultraviolet};

spectrum band;
band = blue;    // valid
band = 2000;    // invalid, 2000 not an enumerator
band++;         // invalid
band = orange + red;    // invalid
```

열거형은 enumeration이라는 새로운 type을 만들어준다. spectrum에 0-7의 symbolic constant integer가 할당된다. 순서대로 정수가 할당되는 것이 아니라 '='를 활용해 원하는 정수를 명시적으로 할당할 수 있다.

```c++
enum bits { one = 1, two = 2, four = 4, eight = 8};
int v = two;        // two converted to integer 2
cout << v << endl;  // 2
```

### Pointers
> Variable that holds the address of a value in Linear memory model

Linear memory model은 **flat memory model**이라고 불리기도 한다.

프로그램 기준에서 memory는 continuous memory addresses를 가진 것처럼 보이기 때문이다. 이것은 실제 physical addresses와는 다르다.

![memory-appearance](/assets/img/2024-03-06/memory-appearance.png)

모든 variable은 특정한 메모리 위치에 할당된다. 예를 들어, 4-byte integer는 1000~1003에 할당된다.

![memory-variable](/assets/img/2024-03-06/memory-variable.png)

이떄 저장되는 방식에는 2가지가 있다. 
Big endian은 큰 숫자가 먼저 온다. Little endian은 큰 숫자가 나중에 온다.

각 변수의 address는 address operator(&)를 사용해 얻을 수 있다.

```c++
// 1000~1003번지
int variable = 0x12345678;
cout << &variable << endl;  // 1000
```

값의 위치를 저장하는 변수인 Pointer의 선언은 다음과 같다.
다만, 보통 type보다는 변수명에 붙여 쓰는 것은 아래 ptr2는 포인터지만, e는 char 변수이기 때문이다.

```c++
// typename * pointer_name;
int val;
int *ptr = &val;    // pointer to integer initialized to &val
char *ptr2, e;      // while ptr2 is a pointer to char, e is a char variable;
```


- Dereferencing Operator(*) :
**\*pointer**는 pointer에 저장된 위치에 담김 값을 기리킨다.

```c++
*ptr = 100;     // equivalent to 'val = 100;'
cout << *ptr << endl;   // 100
cout << val << endl;    // 100
val = 500;
cout << *ptr << endl;   // 500
cout << val << endl;    // 500
```

## Questions?
**Q1.** Array는 assignment operator(=)를 사용해서 복사할 수 없지만, Structure는 '='를 사용해서 복사할 수 있다. 그렇다면 Structure 안에 있는 Array도 '='를 사용해서 그 Structure를 복사할 때 복사가 될까? 
**A1.** Yes. 어떤 operation을 통해 되는지 구현해보고 싶네.

**Q2.** 왜 Array는 Structure과 달리 assignment operator(=)를 사용할 수 없게 설계되었을까? 어떤 사상에 의해서일까?
**A2.** 

**Q3.** Enumerator에 일부만 정수를 할당한다면 나머지는 어떻게 할당될까? 만약 앞에서 자동으로 할당된 정수와 중복되는 값을 나중에 할당한다면 어떻게 될까?
**A3.** 

**Q4.** Pointer에 저장된 값(ptr)는 특정 변수의 주소(&var)이고, Pointer가 역참조 값(*ptr)은 변수의 값(var)이라면, 왜 초기화할 떄 'int *ptr = &val;'라고 쓰는가? 그런데 왜 '역참조'라는 명칭을 쓰는 건가?



<!-- Links -->
