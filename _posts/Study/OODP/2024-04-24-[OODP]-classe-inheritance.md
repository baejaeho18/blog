---
layout: post
title: "[OODP] 10. Class Inheritance(2)"
category: study
tags: oodp
---

> POSTECH OODP Lecture at 24SS

# Class Inheritance

Class 상속은 높은 코드 재사용성을 제공한다.
상속하도록 설계된 base class와 상속 받는 derived class로 구성된다.
<!--more-->
간단한 base class의 예시는 다음과 같다.

```c++
class Student
{
private:
    string name;
    int id;
public:
    Student(const string &name_ = "", int id_ = 0);
    void setName(const string &name_) { name = name_; }
    const string& getName() const { return name; }
    void setId(int id_) { id = id_; }
int getId() const { return id; }
};

Student::Student(const string &name_, int id_)
: name(name_), id(id_)
{ }
```
학생이라는 커다란 분류 아래, 대학원생들을 표현하는 deriving class의 간단한 예시는 다음과 같다.
```c++
class GraduateStudent : public Student
{
private:
    // string name; int id;
    string lab;
public:
    GraduateStudent(const string &name_ = "", int id_ = 0, const string &lab_ = "");
    // void setName(const string &name_) { name = name_; }
    // const string& getName() const { return name; }
    // void setId(int id_) { id = id_; }
    // int getId() const { return id; }
    void setLab(const string &lab_) { lab = lab_; }
    const string& getLab() const { return lab; }
};

GraudateStudent::GraudateStudent(const string &name_, int id_, const string &lab_)
// : name(name_), id(id_), lab(lab_)
: Student(name_, id_), lab(lab_)
{ }
```
주석은 상속 받지 않았을 때 필요한 member들이다.
**: public Student** 구문을 통해 Student의 public member들을 GraduateStudent 자신의 interface처럼 사용할 수 있다. 한편, Student의 private member들은 GraduateStudent가 사용할 수 있지만 GraduateStudent의 member function으로 직접 제어할 수는 없다. name과 id를 = 연산자로 할당하지 않고, initializer list로 초기화하는 이유이다.

![inheritance](/assets/img/2024-04-22/inheritance.png)

상속되지 않는 member들도 존재하는데, Constructor&destructor와 assignment operator들이 그것이다. 이는 derived class가 base class에 비해 data member들이 추가되는 경우가 잦이, 자체적인 constructor가 있는 것이 자연스럽기 때문이다.

## Speicial Relationships Btw. Derived & Base Classes

* derived-class object는 base-class의 public method들을 사용할 수 있다.

* base-class pointer는 derived-class 객체를 explicit typecast 없이 지칭할 수 있다.

* base-class reference는 derived-class 객체를 explicit typecast 없이 참조할 수 있다

* 다른 것은 불가능하다.

이러한 관계를 **is-a** relationship이라고 부른다(GraduateStudent is a Student).


## Questions?
**Q1.**      <br>
**A1.** 

**Q2.**      <br>
**A2.** 


<!-- Links -->
