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
### Array
> a data form that can hold several values, all of one type

```c++
int cards[4] = {3, 6, 8, 10};
int hand[4];
hand[4] = {5,6,7,9};
hand = {5,6,7,9};
hand = cards;

float hotelTips[5] = {5.0f, 2.5f};
unsigned int counts[10] = {};

short things[] = {1,3,5,6};
```
- Format: typeName arrayName[arraySize];
- arraySize: integer constant, cannot be a variable <br>
    arraySize에 벗어나는 index를 참고하면 runtime error가 발생한다. index는 0부터 시작한다.
- Initialization Rules for Arrays
초기화는 array를 정의할 때만 가능하다. 또한 다른 array를 그대로 할당하는 것도 불가능하다.
초기화 시, 정해진 크기보다 적은 값만을 할당할 수 있다. 컴파일러는 미할당된 값들에 0을 넣어준다.
또한 size를 명확히 정해주지 않아도 된다. 컴파일러에 의해 자동으로 결정된다.

### Strings
> A series of characters stored in consecutive bytes of memory

- C-style string: stores a string in an array of **char**
    - string의 끝을 뜻하는 Null-character('\0')을 반드시 넣어줘야함.
    - C++에서는 string literals 사이에 whitespace(spaces, tabs, and newlines)만 존재한다면 자동으로 합쳐준다.

- string class library



## Questions?
**Q1.** Array에서 size를 const로 선언한 값으로 정할 수 있는가? <br>
**A1.** 물론이다.

**Q2.** 
**A2.**


<!-- Links -->
