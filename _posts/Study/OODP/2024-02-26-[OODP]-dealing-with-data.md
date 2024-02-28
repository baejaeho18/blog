---
layout: post
title: "[OODP] 1. Dealing with Data(1)"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

# Variables
> Programs typically need to store information. To store an item, the program must keep track of 3 fundamental properties

1. 어디에 저장할 것인가
2. 어떤 value를 저장할 것인가.
3. 어떤 type의 정보를 저장할 것인가.

```C++
int barincount = 5;
```
1. braincount는 정보가 저장된 memory location을 가리키는 데 사용된다.
2. braincount는 5라는 value를 뜻한다.
3. integer에 저장된다.

## Names for Variables
> Naming Rules

- Alphabetic characters(a-Z), numeric digits(0-9) and underscore(_).
- 첫 글자는 numeric digit일 수 없다
- 대소문자는 구분된다
- C++ keyword(reserved name)은 사용할 수 없다
- 길이 제한은 없다
- Avoid names beginning with underscore character, e.g., _variable, __Variable.
    - 하나 혹은 두 underscroe(_) 뒤에 붙는 대문자 이름은 compiler에 예약되어 있다
    - 하나의 underscore로 시작하는 이름은 global identifier로 예약되어 있다.
    > Names beginning with two underscore characters or with an underscore character followed by an uppercase letter are reserved for use by the implementation, i.e., compiler. Names beginning with a single underscore character are reserved for use as global identifiers by the implementation.


## Data Types
* Fundamental types
    - Integers
    - Floating-point numbers
* Compound types
    - Build on the basic types
    - Arrays, strings, pointers, structures

### Integer Types
Numbers with no fractional part, e.g., 2, 98, -5286, 0 <br>
![integer-types](/assets/img/2024-02-26/integer-types.png) <br>
16-bit의 short integer type은 -32,768 ~ +32,767의 값을 표현할 수 있다.
    - 2^16 = 65536
여러가지 type이 존재하는 이유는 불필요한 memory space의 낭비를 막기 위해서이다.

C++ 표준이 type마다 고정된 크기를 두지 않은 것은 system마다 **natural data size**가 다르기 때문이다. natural size란 컴퓨터가 가장 효과적으로 다룰 수 있는 크기를 말한다. IBM은 가장 natural한 16-bits를 int로 맞췄다. <br>
Integer type의 표준은 **int**이고, 음수를 표현할 일 없으면 unsigned을, 보다 넓은 범위를 다루고 싶다면 long이나 long long을, 보다 좁은 범위를 다룬다면 short나 심지어 char를 사용하면 된다.
    - char는 ?-bits로 ?~?까지의 정수를 표현할 수 있다.

만약 변수 type의 가능한 범위를 넘어서는 값을 할당한다면 overflow/underflow가 발생한다.
![over-underflow](/assets/img/2024-02-26/over-underflow.png)

* Integer Literals
10진수 뿐만 아니라, 16진수와 8진수로도 표현할 수 있다.
```C++
int chest = 42;     // decimal integer literal (42)
int waist = 0x42;   // hexadecimal integer literal starts with '0x' (66)
int inseam = 042;   // octal integer literal starts with '0' (34)
```
hexadecimal은 0~9, A-F로 표현된다. 0xF(or 0xf, 0XF, 0Xf)는 15, 0xFF는 255(1 byte)이다. 2 digits이 1 byte라는 것이 low-level system programming에서 무척 편리하다.
```C++
cout << dec; // manipulator for changing number base
cout << "chest = " << chest << " (decimal for 42)" << endl;
cout << hex; // manipulator for changing number base
cout << "waist = " << waist << " (hexadecimal for 42)" << endl;
cout << oct; // manipulator for changing number base
cout << "inseam = " << inseam << " (octal for 42)" << endl;
// Output
// chesct = 42 (defimal for 42) 
// waist = 2a (hexadecimal for 42)
// inseam = 52 (octal for 42)
```

* How C++ Decides What Type a Constan Is?

* The char Type: Characters and Small Integers
char type은 1 Byte, 즉 8-bits 크기의 변수이다. 따라서 2^8개의 정수(-128~127)를 표현할 수 있다.




## Questions?
**Q.** 구글 C++ style guide를 보았을 때, member 변수에는 underscore(_)를 사용하도록 권장하던데 상관없을까요?
**A.** class 멤버변수 앞에 underscore를 붙여야한다는 것은 전혀 아니다. 그래야할 이유가 없다. 다만 underscore를 앞에 쓰지 말라는 것은 컴파일러의 예약어와 겹칠 수도 있기 때문이다. 그런데 멤버변수는 별도로 implementation되기 때문에 사용해도 무방하다.
**+** [구글 C++ Convention]를 확인해본 결과 class 멤버변수에 underscore를 붙이는 것을 권장하는 것은 앞이 아니라 뒤였다. 우문에 현답이라 하겠다.

**Q2.** char가 정수까지 표현할 수 있다고 했는데, int로 type을 다시 선언해줘야 출력할 수 있다면 정수를 저정한다고 표현할 수 있나요?

<!-- Links -->
[구글 C++ Convention]: https://torbjorn.tistory.com/257