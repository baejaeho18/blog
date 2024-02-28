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

* The char Type : Characters and Small Integers<br>
char type은 1 Byte, 즉 8-bits 크기의 변수이다. 따라서 2^8개의 정수(-128~127)를 표현할 수 있다. 예컨데, ASCII로 알파벳 'M'은 숫자 77로 저장된다. 변수를 호출하면, 저장된 숫자 77은 type에 맞춰져 'M'으로 반환된다. 그러나 실제로 저장되는 것은 1-byte integer이기 때문에, integer operation을 적용하라 수 있다.
```C++
char ch = 'M';  // assign ASCII code for M to ch
int i = ch; // store same code in an int
cout << ch << i << ch + 1 << endl;
// output
// M 77 N
```

* The bool Type
> Bool represents a boolean value(true or false).

Bool 타입이 소개되기 전까지, zero/nonzero number가 false/true로 사용되었다. 이는 아직까지도 이어진다.
```C++
bool is_ready = true;

int ans = true; // ans assigned 1
int promise = false;    // promise assigned 0

// Both in C and C++, nonzero numbers are interpreted as true
if ( 32 ) {
    cout << "True" << endl;
}
else {
    cout << "False" << endl;
}
// output
// True

bool start = -100;  // start assigned true
bool stop = 0;  // stop assigned false
```

* The sizeof Operator
data type들의 size는 system에 따라 다르다. 특정한 data type의 크기를 확인할 때 sizeof을 사용한다.
```C++
// sizeof operator yields size of type or of variable
// sizeof(type_name)
// sizeof(variable_name)
sizeof(int)
sizeof(n_short)
sizeof(n_long)
sizeof(n_llong)
```

* #define Statement
소스코드 안에 숫자들이 많아질수록 의미를 파악하기가 어렵다. 코드 안의 숫자가 무엇을 의미하는지 고민해야하기 때문이다. 이때 **#define** 문을 사용해서 symbolic constants를 정의할 수 있다.
```C++
#define NUM_WHEELS_PER_CAR  4
#define PI                  3.141592

int area = PI * radius * radius;
```

#define 문은 preprocessor directive이다. 마치 editor의 '전체 바꾸기(ctrl+h)'와 같은 역할을 한다. 코드 상의 위치와 관계없이 동작하지만, 일반적으로 파일의 시작에 둔다.

정의한 define 문이 상수가 아닌 연산식일 경우, 의도하지 않은 동작을 방지하기 위해 '( )'로 묶을 것을 권고한다.
```C++
#define NUM_LEGS_PER_CAT    2+2
#define NUM_LEGS_PER_DOG    (2+2)
```

* The const Qualifier
> const type name = value;
그러나 **#define**문은 과거에 symbolic constants를 정의하던 방식이다. const는 symbolic constants를 정의하는 새로운, 더 나은 방법이다.

const는 #define에 비해 여러가지 장점이 있다. const는 type을 명시할 수 있고, 적용 범위를 조절할 수 있다. 또한, #define 처럼 미리 상수를 정의해두는 것이 아니라, runtime 도중에 값을 할당할 수 있다. 또한 arrays, structures, classes와 같은 정교한elaborate 타입들로도 사용될 수 있다.
```C++
#define ONE = 1     // Traditional C style
                    // No explicitly specified type
                    // Uppercase for all letters
                    // Can use ONE outside of this block
const long Two = 2; // New to C++
                    // Uppercase for the 1st letter
                    // Allows to limit the scope of a const
const int Some_const

Some_const = i * 2; // create constants in the runtime

const Position origin = {0,0};
```

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

* C++ Arithmetic Operators
Addition(+), Subtraction(-), Multiplication(*), Division(/), Modulus(%)




## Questions?


<!-- Links -->
