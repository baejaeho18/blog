---
layout: post
title: "[DL] 2. Optimization for Training Deep Models"
category: study
tags: ai
---

> [Deep Learning]을 정리하겠다.

딥러닝에서의 최적화 문제는 모델의 파라미터를 조정하여 cost function, J(θ)를 최소화하는 것을 말한다.
본 챕터에서는 학습을 위해 쓰이는 최적화가 pure 최적화와 얼마나 다른지, 무슨 난제들이 있는지, 어떤 최적화 전략들이 실제로 쓰이고 있는지 알아보겠다.
<!--more-->
## 8.1 How Learning Differs from Pure Optimization

먼저 학습(learning)의 정의를 짚고 넘어가자.
> A commputer program is said to learn from experience E with respect to some class of tasks T and performance measure P,
if its performance at tasks in T, as measured by P, improves with experience E [Mitchell, 1977]


## 8.2 Challenges in Neural Network Optimization

## 8.3 Basic Algorithms

## 8.4 Parameter Initialization Strategies

## 8.5 Algorithms with Adaptive Learning Rates

## 8.6 Approximate Second-Order Methods

## 8.7 Optimization Strategies and Meta-Algorithms

## Questions
**Q1.** 어떻게 추정기가 모델의 편향과 분산을 조절하는지 잘 모르겠습니다. 추정기의 정규화가 어떻게 이뤄지는지 이해가 잘 가지 않습니다.  <br>
**A1.** Try all equations drive as possible.

**Q2.** input에 noise를 추가한다는 것은 직관적으로 이해가 됩니다. 그런데 noise를 가중치에 적용한다는 것이 왜 성능 향상에 도움이 되는지 잘 이해가 가지 않습니다. 경험적 추론의 결과인가요? <br> 
**A2.** 


<!-- Links -->
[Deep Learning]: https://github.com/baejaeho18/MyLibrary/blob/main/Machine%20Learning/deeplearningbook.pdf
[Mitchell, 1977]: https://www.cin.ufpe.br/~cavmj/Machine%20-%20Learning%20-%20Tom%20Mitchell.pdf