---
layout: post
title: "[DL] 6. Representation Learning"
category: study
tags: ai
---

> [Deep Learning]을 정리하겠다.

# 15. Representation Learning
정보의 표현 방식은 정보 처리 난이도에 큰 영향을 미칠 때가 있다. 좋은 표현은 처리 과제를 쉽게 만들어준다.

<!--more-->
## 15.1 Greedy Layer-Wise Unsupervised Pretraining
비지도 사전훈련은 CNN이나 RNN 같은 특화된 구조가 아니더라도 십층 지도 신경망을 훈련시키는 절차이다.
입력의 형태을 포착하려는 비지도 학습에서 배운 표현이, 같은 입력 영역에 대한 지도학습에도 유용할 수 있음을 보여준다.
사전 훈련 이전에는 CNN이나 RNN을 통해 깊어진 신경망으로만 학습할 수 있다고 생각했다.

신경망의 각 층을 비지도로 greedy하게 최적화하는 일련의 절차가 사전 훈련 단계이다.
이 사전 훈련 단계에서 배운 특징에 기초하여 분류기를 훈련하거나 심층신경망을 초기화한다. 
이 과정을 거치면 test error을 크게 개선할 수 있다.
사전 훈련을 거치며 심층 신경망의 매개변수들에 강한 정칙화 효과가 있을 것이라 추측한다. 예컨데, 특정한 극소점에 잘 도달하는 시작 위치로 모델을 초기화하는 것이다.
또 다른 추측으로는 사전 훈련된 특징 표현들이 지도 학습 모델에서도 유용할 수 있다는 것이다. 이 가설은 직관적이지만 수학적 이론으로 파악되지는 않았다.

그러나 label이 5000개 이상인 medium-sized dataset에서는 심층 지도 학습이 유리하고, 극히 작은 dataset에서는 베이즈 방법들이 더 유리하다. 따라서 비지도 사전훈련은 자연어 처리 분야에서만 활발히 사용되고 있다. 단어들의 표현인 one-hot vector가 유사도 정보를 담지 않고, 아주 큰 unlabeled set을 사용가능하다는 점에서 사전훈련으로 좋은 (단어 혹은 문장의) 표현을 배워 견본이 부족한 지도 학습 과제에 사용할 수 있다.

## 15.2 Tranfer Learning and Domain Adaptation
사전 훈련은 결국 비지도 학습과제의 표현을 지도 학습 과제로 전달(transfer)하는 것이다. 이를 발전 시킨 것이 전이 학습이다.
완전히 무관하지는 않은 둘 이상의 과제들을 수행하는 것이 목표이다. 

## 15.3 Semi-Supervised Disentangling of Causal Factors
좋은 표현은 무엇이고, 어떻게 구할 수 있을까?

## 15.4 Distributed Representation

## 15.5 Exponential Gains from Depth
## 15.6 Providing Clues to Discover Underlying Causes

## Questions
**Q1.** 15.1.1에서 극소점을 접근할 수 없는 사례들을 설명했는데, 수학적으로 이해를 하지 못했습니다. "for example, a region that is surrounded by areas where the cost function varies so much from one example to another that minibatches give only a very noisy estimate of the gradient, or a region surrounded by areas where the Hessian matrix is so poorly conditioned that gradient descent methods must use very small steps" 부연 설명이 가능할까요?    <br>
**A1.** 

**Q2.**  <br> 
**A2.** 

**Q3.**   <br>
**A3.**




<!-- Links -->
[Deep Learning]: https://github.com/baejaeho18/MyLibrary/blob/main/Machine%20Learning/deeplearningbook.pdf
[effective capacity]: https://munjeongkang.github.io/ANN2/
[LeCun, 1998a]: http://vision.stanford.edu/cs598_spring07/papers/Lecun98.pdf
[Deng&Yu, 2014]: https://nowpublishers.com/article/Details/SIG-039
[Graves, 2015]: https://arxiv.org/pdf/1508.0850.pdf