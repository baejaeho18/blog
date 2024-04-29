---
layout: post
title: "[OODP] 11. Reusing Code in C++"
category: study
tags: oodp
---

# Reusing techniques
## Classes with Member Object (containment)
다른 class의 객체들을 class member로 사용할 수 있다.
이를 **containment**, **composition** 혹은 **layering**이라고 부른다.
예를 들어 Student class에서는 string 객체(name)와 valarray 객체(scores) 등을 사용한다.

### valarray template class
> Header file: #include \<valarray\>

numeric값들의 배열을 다르는 template class이다.
합산, 최댓값, 최솟값 등의 산술연산을 지원한다.
vector나 array 클래스들과는 완전히 다르다.

```c++
class Student {
private:
    typedef std::valarray<double> ArrayDb;
    std::string name; // contained object
    ArrayDb scores; // contained object
    // private method for scores output
    std::ostream& arr_out(std::ostream& os) const;
public:
    Student() : name("Null Student"), scores() {}
    explicit Student(const std::string& s) : name(s), scores() {}
    explicit Student(int n) : name ("Nully"), scores(n) {}
    Student(const std::string& s, int n) : name(s), scores(n) {}
    Student(const std::string& s, const ArrayDb& a) : name(s), scores(a) {}
    Student(const char* str, const double* pd, int n) : name(str), scores(pd, n) {}
    ~Student() {}
    double Average() const;
    const std::string& Name() const;
    double& operator[](int i);
    double operator[](int i) const;
    // friends
    // input
    friend std::istream& operator>>(std::istream& is, Student& stu); // 1 word
    friend std::istream& getline(std::istream& is, Student& stu); // 1 line
    // output
    friend std::ostream& operator<<(std::ostream& os, const Student& stu);
};
```

## Private and Protected Inheritance
### Private Inheritance
Public inheritance(is-a relationship)은 base class의 public method들을 derived class의 public method로 삼아, **interface**를 상속받는다.
그러나 private inheritance(has-a relationship)은 base class의 public method들을 derived class의 **private** method로 삼는다. 
이는 containment와 유사한 면이 있다.
![private-inheritance](/assets/img/2024-04-29/private-inheritance.png)

```c++
class Student : private std::string, private std::valarray<double>{
private:
    typedef std::valarray<double> ArrayDb;
    // private method for scores output
    std::ostream& arr_out(std::ostream& os) const;
public:
    Student() : std::string("Null Student"), ArrayDb() {}
    explicit Student(const std::string& s) : std::string(s), ArrayDb() {}
    explicit Student(int n) : std::string("Nully"), ArrayDb(n) {}
    Student(const std::string& s, int n) : std::string(s), ArrayDb(n) {}
    Student(const std::string& s, const ArrayDb& a) : std::string(s), ArrayDb(a) {}
    Student(const char* str, const double* pd, int n)
    : std:: string(str), ArrayDb(pd, n) {}
    ~Student() {}
    double Average() const;
    double& operator[](int i);
    double operator[](int i) const;
    const std::string& Name() const;
    // friends
    // input
    friend std::istream& operator>>(std::istream& is, Student& stu);
    friend std::istream& getline(sted::istream& is, Student& stu);
    // output
    friend std::ostream& operator<<(std::ostream& os, const Student& stu);
};
```
위 코드처럼 **private** keyword를 사용해 상속받는다. 
본 예시처럼 여러 개의 base class로부터 상속받는 것을 **multiple inheritance**라고 부른다.

일반적으로 private inheritance보다는 containment가 훨씬 잘 쓰이는 것이 맞다. 
private inheritance가 유용한 상황은, base class의 protected member를 사용하거나 overriding하고 싶을 때이다.

### Protected Inheritance
이는 private inheritance와 유사하게 has-a relationship을 지원한다.
**protected** 키워드로 상속받는데, base class의 public과 protected member들이 derived class의 protected member가 된다. 정리하자면 다음과 같다.

### Redefining Access with using
지금까지 base class의 public member들을 private나 protected member로 상속 받는 방법을 알아보았다.
그러나 특정한 base-class method를 derived class에서 publicly 사용하고 싶을 수 있다.

사용할 base-class method를 호출하는 wrapping method 정의하는 방법과, public section에서 using을 사용하여 재정의하는 방법이 있다.

```c++
double Student::sum() const // public Student wrapping method
{
    // use privately-inherited method
    return std::valarray<double>::sum(); 
}
class Student : private std::string, private std::valarray<double>
{
    // ...
public:
    using std::valarray<double>::sum;
    // ...
};
```

## Multiple Inheritance


## virtual base classes


## Questions?
**Q1.**    <br>
**A1.** 

**Q2.**      <br>
**A2.** 

<!-- Links -->
