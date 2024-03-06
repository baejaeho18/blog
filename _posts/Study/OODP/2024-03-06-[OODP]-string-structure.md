---
layout: post
title: "[OODP] 2. Compound Types(1)"
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
} ds, jy;       // also can omit structure name
```




## Questions?
**Q1.** 



<!-- Links -->
