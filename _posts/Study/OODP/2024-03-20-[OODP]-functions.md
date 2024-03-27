---
layout: post
title: "[OODP] 5. Functions: C++ Programming Modules"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

C++에서 function을 사용하려면 세가지 조건을 만족해야 한다.
- Provide a function **definition** : describe the actions the function performs
- Provide a function **prototype** : interface which specifies the return type, name and arguments
- **Call** the function
<!--more-->
실제로 C++ 표준 라이브러리들은 C++ Compiler를 설치했다면, 이미 컴파일된 object 파일의 형태로 저장되어 있을 것이다.
import하는 헤더파일에 prototype이, a(ubuntu)나 lib(msvc)를 확장자로 하는 object file에 definition이 저장되어 있다.
```bash
$: ls /usr/lib/gcc/x86_64-linux-gnu/7
cc1 crtoffloadtable.o libbacktrace.a libgomp.so libmpx.so libsupc++.a
cc1plus crtprec32.o libcc1.so libgomp.spec libmpx.spec libtsan.a
collect2 crtprec64.o libcilkrts.a libitm.a libmpxwrappers.a libtsan.so
crtbegin.o crtprec80.o libcilkrts.so libitm.so libmpxwrappers.so libubsan.a
...
```

## Function ProtoType
### Function Arguents
- Passing by value(call by value) : argument로부터 callee의 변수값을 복사해 사용한다.

``` c++
double cube(double x) {
    x = x * x * x;
    return x;
}
```

- Passing by reference(call by reference) : callee가 argument와 동일한 변수를 사용한다.

``` c++
// Mimicking call by reference using pointers
void multiply2(int *p) {
    *p *= 2;
}
```

pointer를 call by value로 봐야하는지 call by reference로 봐야하는지는 아직까지는 의견이 분분하다(학부생 수준의 토의에서다).
나는 call by value로 봐야한다 편이지만, ~~확실히 맞는지도 모르겠고 유희거리에 가까우니 여기까지만 적겠다.~~ ~~여백이 부족하니 적지 않겠다~~
포인터에 조금 더 알아보고 싶은 분은 [포인터]를 참고하셔도 좋을 것 같다.



## Questions?
**Q1.** 왜 포인터를 call by reference로 볼 수 없는거야? 그렇다면 진짜 call by reference는 어떤 것이야?<br>
**A1.** 포인터 자체가 주소를 저장하는 변수이다. 따라서 엄밀히 말하면 'call by reference(참조)'라기 보다는 'call by address(주소)'라고 할 수 있다. 포인터를 통한 간접 참조(indirect reference)라고도 부를 수 있겠다.

**Q2.** 함수의 return type에는 어떤 것이 올 수 있나요? <br>
**A2.** array를 제외한 모든 type이 올 수 있다. integers, floating-point numbers, pointer and even structures and objects! 그러나 흥미롭게도, structure이나 object 내의 array는 반환되지만 array 자체는 반환될 수 없다. <br>
**+** why? 반환된 배열을 해제할 적절한 시기나 방법을 알 수가 없음.

<!-- Links -->
[포인터]: https://handhp1.tistory.com/47