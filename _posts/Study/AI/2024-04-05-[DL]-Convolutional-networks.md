---
layout: post
title: "[DL] 3. Convolutional Networks"
category: study
tags: ai
---

> [Deep Learning]을 정리하겠다.

# 9. Convolutional Networks

합성곱망(convolutional networks; LeCun, 1989) 또는 합성곱 신경망(convolutional neural network, CNN)은 격자 형태(grid-like topology)로 배열된 데이터를 처리하는 데 특화된 신경망이다. 어떤 CNN 구조가 어떤 상황에 좋은지보다, 어떻게 CNN이 구성되는지 위주로 정리하겠다.

## 9.1 The Convolution Operation
두 함수를 합성곱 (f*g)(x)할 때, 첫 인수(f)를 입력이라고 부르고, 둘째 인수를 kernel이라고 부른다. 출력 결과를 feature map이라고도 부른다.
합성곱은 단순한 덧셈 혹은 곱셈 하나가 아니라, 확률곱의 합산처럼 생각하면 조금 이해하기 편하다.
![two_random_convol](/assets/img/2024-04-08/two_random_convol.png)

예를 들어, $$(1,2,3)*(4,5,6) = (4, 1*5+2*4, 1*6+2*5+3*4, 2*6+3*5, 3*6) = (4, 13, 28, 27, 18)$$ 이 되는 것이다.

```python
np.convolve((1,2,3), (4,5,6))   # array([4, 13, 28, 27, 18])
```

위의 배열합성곱은 정확히 동일하게 다항식의 곱에서 찾아볼 수 있다.
![polynomial_multiplication](/assets/img/2024-04-08/polynomial_multiplication.png)

즉, 두 배열을 계수로 하는 두 다항식의 곱에서 계수를 추출한 것과 동일하다.

위의 합성곱 개념을 딥러닝에서 활용할 때, kernel에는 확률밀도함수를 넣는다. 
kernel을 이동평균으로 해석하면, 원본 데이터을 smoothing한 효과가 난다. 이는 시계열 데이터나, 시각 데이터에 적용될 수 있다.

## 9.2 Motivation
합성곱 신경망이 유용한 까닭은 다음 세가지 이유로 설명할 수 있다.
1) sparse interaction : 본래 각 계층에서 필요한 연산의 크기는 (input\*output)이다. 그러나 작은 kernel만으로 원하는 feature을 추출할 수 있을 떄, 필요한 연산의 크기는 (kernel\*output)뿐이다. 물론 해당 계층에서는 직접적으로 연결되지 않은 노드를 학습할 수 없지만, 보다 심층에서는 간접적으로 영향을 받을 수 있다. 이를 보장하기 위해 간격(stride)을 주거나 pooling 구조로 합성곱망을 구성한다.
2) parameter sharing : 모든 입력에 동일한 kernel이 사용된다. 계산비용과 메모리 비용 모두 획기적으로 감소한다.
3) equivariant representations : 입력이 다소 변하더라도 동일한 출력을 보장하는 개념이다. 예컨데, CNN은 이미지의 위치를 이동시켜도 원하는 feature을 동일하게 잡아낸다. 단, 회전한 경우에는 불가능하다.

## 9.3 Pooling
pooling은 합성곱의 결과로 도출된 활성화 값을 이웃 출력들의 요약통계량(summary statistics)로 대체한다. 일반적으로 max, average, $$L^2&& Norm, weighted average 등이 쓰인다.
pooling을 통해 입력의 작은 변화에 대해 특징이 불변(invariant)하도록 할 수 있다. 
더불어 계산비용을 낮추고, 과적합을 방지해 일반화 성능을 향상시키는 효과가 있다.

## 9.4 Convolution and Pooling as an Infinitely Strong Prior
Infinitely Strong Prior(무한히 강한 사전확률분포)란 일부 매개변수에 0을 할당하여 절대로 영향을 끼치지 못하게 강요하는 분포이다. 확률밀도가 얼마나 조밀한지 곧, 분산과 반리례하는 척도가 strong과 weak이다.
합성곱 신경망과 pooling은 고정된 kernel과만 상호작용하기 때문에 무한히 강한 사전분포라고 볼 수 있다. 

## 9.5 Variants of the Basic Convolution Function
## 9.6 Structured Outputs
## 9.7 Data Types
## 9.8 Efficient Convolution Algorithms
## 9.9 Random or Unsupervised Features
## 9.10 The Neuroscientific Basis for Convolutional Networks
## 9.11 Convolutional Networks and the History of Deep Learning

## Questions
**Q1.**   <br>
**A1.** 

**Q2.**  <br> 
**A2.** 

**Q3.**   <br>
**A3.**




<!-- Links -->
[Deep Learning]: https://github.com/baejaeho18/MyLibrary/blob/main/Machine%20Learning/deeplearningbook.pdf