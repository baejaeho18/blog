---
layout: post
title: "[OODP] 1. Dealing with Data(2)"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

## Data Types
* Fundamental types
    - Integers
    - Floating-point numbers
* Compound types
    - Build on the basic types
    - Arrays, strings, pointers, structures

<!--more-->

### Integer Types
> Numbers with no fractional part, e.g., 2, 98, -5286, 0

![integer-types](/assets/img/2024-02-26/integer-types.png) <br>
c++은 불필요한 memory space의 낭비를 막기 위해 여러가지 type이 존재한다. 이때, system마다 가장 효과적으로 다룰 수 있는 크기인 **natural data size**가 다르기 때문에, 각 type의 크기가 표준으로 고정되어 있지는 않다. <br>
Integer type의 표준은 **int**이고, 음수를 표현할 일 없으면 unsigned을, 보다 넓은 범위를 다루고 싶다면 long이나 long long을, 보다 좁은 범위를 다룬다면 short나 심지어 char를 사용하면 된다.
만약 변수 type의 가능한 범위를 넘어서는 값을 할당한다면 overflow/underflow가 발생한다.

### Floating-Point Numbers
> Floating-point types represent numbers with fractional parts<br>
E notation : 3.45E6 == +3.45e+6 == 3.45 * 10^6

C++에는 3가지 floating-point type이 존재한다.
![floating-types](/assets/img/2024-02-28/floating-types.png)
floating-point constant는 default로 double로 인식된다.
float로 하고 싶다면 Suffix f(or F)를 붙이고, long double로 하고 싶다면 Suffix l(or L)을 붙이면 된다. 이때, 소문자 l을 숫자 1로 착각할 여지를 없애고자 대문자 L을 사용하도록 권고한다.
```c++
1.234f      // float
2.45E20F    // float
2.345324E28 // double
2.2L        // long double

float var = 2.34;   // warning: as it tries to assign a double constant to a float variable
float var2 = 2.34f; // To avoid warning, use the suffix
```

### Operators
* C++ Arithmetic Operators
Addition(+), Subtraction(-), Multiplication(*), Division(/), Modulus(%)

* Expressions and Assignment Operators
> Expression: any value or any valid combination of values and operators consitute an expression

```c++
mids = (cook = 4) + 6;
x = y = 4;
```

* Increment/Decrement Operators
```C++
y = ++z; // z += 1, y = z
y = z--; // temp = z, z -= 1, y = temp

x = 2 * x++ * (3 - ++x);    // ambiguous!
```
- Never ever use them twice in one equation
- C++ doesn't define the correct behaviour, so it depends on compiler

* Bitwise Operators
Operate on the bits of integer values
- shift(<<, >>), negation(~), AND(&), OR(|), XOR(^)
```c++
unsigned char a = 13;
unsigned char b = 22;

unsigned char sl = a << 3;  // 
unsigned char sr = a >> 3;  // 
unsigned char neg = ~a;     // 231?
unsigned char and = a & b;  // 4
unsigned char or = a | b;   // 31
unsigned char xor = a ^ b;  // 27
```

* Type Conversions
> C++ provides automatic type conversion

컴파일러에 의해 발생하므로 data loss가 발생할 수 있음.

* Type Casting Operators
> 2 forms of syntax : (typename)value, typename(value)

개발자가 의도적으로 Type을 지정

## Questions?


<!-- Links -->
