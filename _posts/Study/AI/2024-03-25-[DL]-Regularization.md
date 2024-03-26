---
layout: post
title: "[DL] 2. Regularization for Deep Learning"
category: study
tags: ai
---

> [Deep Learning]을 정리하겠다.

머신러닝에서 중요한 문제는 어떻게 훈련 데이터 뿐만 아니라, 실제 데이터(new input)에 대해서도 잘 동작하도록 할 것인가다. 
training error가 다소 발생하더라도 test error를 잡는 것이 **regularization**의 전략이다.
정규화란, "any modification we make to a learning algorithm that is intended to reduce its generalization error but not its training error."
정규화 전략에는 제약(constraints)를 거는 것과 여러 가설을 결합(ensemble)하는 것이 있다.
constraints를 추가하는 방식에는 파라미터 값에 제약을 걸거나, 사전지식을 부여하거나, 모델을 단순화(simpler)하거나, determined 문제로 변환하는 등이 있다.
이상적인 정규화는 분산(variance)를 크게 감소시키면서 편향(bias)는 적절하게 유지하는 것이다.
regularizing estimator(추정기)는 입력값에 대해 예측을 생성하고, 실제값과의 오차를 최소화하기 위해 파라미터를 조정하는 과정에서 복잡도를 조절한다??
파라미터와 층의 수와 크기가 클수록, 복잡도와 모델의 크기가 크고 과적합(overfitting)의 위험도 올라간다. 적절한 정규화된 큰 모델이 일반적으로 가장 최적화된 모델이다.

## 7.1 Parameter Norm Penalties
딥러닝의 출현 이전에도 선형 모델(로직스틱회귀, 선형회귀)에서도 정규화는 쓰여왔다.
전통적인 방법이 parameter norm penalty(혹은 weight decay)를 적용하여 파라미터가 너무 커지지 않게 제약을 거는 것이다. weight의 절댓값이 너무 크지 않도록 막는 역할을 한다. 단, bias는 건드리지 않는다.
일반적으로 L1 또는 L2 정규화 항을 손실 함수에 추가하여 가중치의 크기를 제한한다.

이때, 각 layer 계층마다 별도의 가중치 감쇠(decay) 계수α를 적용하는 것이 성능적으로 우월하지만 각 계수를 결정하는 비용이 너무 크기 때문에 모든 계층에 동일한 가중치 감쇠를 적용한다.

## 7.2 Norm Penalties as Constrained Optimization
모델의 복잡도를 제어하기 위해 가중치에 제약을 가하는 또다른 정규화 방법에는 제약된 최적화 문제(constrained optimization)가 있다.
이 접근 방식에서 KKT(Karush-Kuhn-Trucker) multipliers는 Largrange function과 유사한 역할을 한다. Largrange function은 제약 조건을 고려해 새로운 목표 함수를 만들어주는 함수로, 제약이 있는 최적화 문제를 해결하는데 사용된다.
KKT 승수는 모델이 최적화 상태에 도달할 때, 각 제약 조건이 얼마나 '중요한지' 나타낸다.
이로써 가중치의 크기를 특정 임계값으로 제한하는 정규화 항을 추가하여 모델을 단순화한다.


## 7.3 Regularization and Under-Constrained Promblems
머신러닝에서 많이 사용되는 선형모델(선형회귀, PCA) 들은 역행렬을 계산해야 한다. 그러나 대상이 Singular(특이) 행렬일 경우, 역행렬이 존재하지 않는다. 어떤 방향으로도 분산이 없거나, 입력 feature의 수(열의 수)가 샘플의 수(행의 수)보다 적은 경우이다.
이런 경우, 역행렬에 작은 상수와 단위행렬의 곱을 더하여 정규화한다.
입력 특성(feature)의 수보다 관측된 데이터 샘플의 수가 적은 underdetermined 문제에 대해 이러한 pseudoinverse(유사 역행렬)로 정규화를 사용하여 여러 해로 인해 과적합되지 않도록 안정화할 수 있다.


## 7.4 Dataset Arguentation
모델의 일반화 성능을 향상시키는 가장 효과적인 방법은 더 많은 데이터로 훈련시키는 것이다. 제한된 데이터 양으로부터 데이터 증강을 통해 학습 데이터셋의 다양성을 높이는 방법이다.
특히 입력 데이터의 다양한 변환에도 동일한 결과를 도출하야하는 분류 작업에 유용하다.
예를 들면, 이미지 회전, 이동, 반전 등의 변형을 통해 학습 데이터셋을 확장하는 것이다.
이러한 접근 방식은 특정한 모델과 도메인에만 유용하다는 것을 유의해야 한다.
예를 들어, 밀도추정작업에 대한 데이터 증강은 이미 문제를 해결하기 전까지는 굉장히 어렵다.

## 7.5 Noise Robustness
앞 챕터와 마찬가지로 데이터를 증강하지만, 오히려 잡음(noise)를 추가하는 전략이다.
이는 noise 주입이 마치 weight norm penalty와 같이 작용한다는 것에 근거를 둔다.
특히, 이미 잡음이 있는 데이터에서 숨겨지 모델 안정성 개선.
예를 들면, 데이터에 노이즈를 추가하여 모델이 노이즈에 강건하게 학습하도록 함.

## 7.6 Semi-Supervised Learning
레이블이 있는 데이터뿐만 아니라 레이블이 없는 데이터를 활용하여 모델을 학습시키는 방법.
예를 들면, 생성 모델을 사용하여 레이블 없는 데이터를 생성하여 모델을 학습시키는 방법.

## 7.7 Multi-Task Learning
여러 작업을 동시에 학습하여 모델의 일반화 성능을 향상시키는 방법.
예를 들면, 하나의 네트워크가 여러 작업을 수행하도록 설계하여 공통된 특징을 학습하는 방법.


## 7.8 Early Stopping
검증 세트의 성능이 더 이상 향상되지 않을 때 학습을 중단하는 방법.
예를 들면, 학습 과정 중에 주기적으로 검증 세트의 성능을 모니터링하고, 성능이 더 이상 향상되지 않으면 학습을 중단.

## 7.9 Parameter Tying and Parameter Sharing
가중치를 공유하여 모델의 파라미터 수를 줄이는 방법.
예를 들면, 다수의 네트워크 계층에서 가중치를 공유하여 모델 파라미터를 공유.


## 7.10 Sparse Representations
희소 표현을 통해 모델을 정규화하는 방법.
예를 들면, L1 정규화를 사용하여 모델의 가중치를 희소하게 만듦


## 7.11 Bagging and Other Ensemble Methods
앙상블 학습을 통해 모델의 일반화 성능을 향상시키는 방법.
예를 들면, 다수의 모델을 학습하여 예측을 결합하여 더 강력한 모델을 구성.


## 7.12 Dropout
학습 중에 무작위로 뉴런을 비활성화하여 모델을 정규화하는 방법.
예를 들면, 학습할 때마다 랜덤하게 뉴런을 삭제하여 모델을 학습.

## 7.13 Adversarial Training
적대적인 예제를 사용하여 모델을 강건하게 만드는 방법.
예를 들면, 적대적인 예제를 생성하여 모델을 학습시키고, 모델이 이러한 예제에 대해 견고하게 대응하도록 함.


## 7.14 Tangent Distance, Tangent Prop, and Manifold Tangent Classifier
접선 거리와 같은 기법을 사용하여 데이터 포인트를 모델링하는 방법.
예를 들면, 데이터 포인트를 곡면에 놓고 해당 곡면의 접선을 사용하여 분류하는 방법.


## Questions
**Q1.** 어떻게 추정기가 모델의 편향과 분산을 조절하는지 잘 모르겠습니다. 추정기의 정규화가 어떻게 이뤄지는지 이해가 잘 가지 않습니다.  <br>
**A1.** 

**Q2.** input에 noise를 추가한다는 것은 직관적으로 이해가 됩니다. 그런데 noise를 가중치에 적용한다는 것이 왜 성능 향상에 도움이 되는지 잘 이해가 가지 않습니다. 경험적 추론의 결과인가요? <br> 
**A2.** 

**Q3.**     <br>
**A3.** 

**Q4.**     <br>
**A4.** 


<!-- Links -->
[Deep Learning]: https://github.com/baejaeho18/MyLibrary/blob/main/Machine%20Learning/deeplearningbook.pdf
