---
title: Inductive Bias란?
# author : Jeonghwan Lee
background : 
date: 2023-02-03 15:22 +0200
tags: [ML]
category : ML
# last_modified_at: 2021-09-08T09:09
---
논문을 읽다보면, "inductive bias" 라는 용어를 종종 접하게 된다. "Bias"라는 단어는 문맥에 따라 부정적인 의미로 해석 될 수도 있는데, inductive bias는 주로 모델의 데이터셋에 대한 성능을 향상 시킬 수 있는 긍정적인 의미로 받아들여진다. 밑의 예시를 보자.      


![Inductive_bias_paper](https://github.com/JH-lee95/jh-lee95.github.io/blob/master/img/posts/inductive_bias/inductive_bias.png?raw=true)


"Object Scene Representation Transformer"에서 발췌한 일부분이다. 내용의 이해와 상관없이, 아무튼 "object-cetnric learning을 통해 inductive bias를 형성하면 좋다!" 라는 내용의 긍정적인 의미를 담고있다.    

그렇다면 inductive bias란 무엇일까?

## **Definition**
> The inductive bias (also known as learning bias) of a learning algorithm is the set of assumptions that the learner uses to predict outputs of given inputs that it has not encountered. -Wikipedia-

*"학습자(모델)가 접해보지 않은 input으로부터 output을 예측할 때 사용하는 가정"*  이라고 위키피디아는 설명하고 있다.

이게 무슨 말일까? 빅데이터와 머신러닝(딥러닝)의 관계를 아는 사람들에게는 이는 너무나도 당연한 말을 하고 있는 것처럼 보인다. 왜냐하면 머신러닝의 가장 기본적인 학습방식 자체가 대량의 데이터로부터 학습하여, unseen data에 대하여 추론하는 것이기 때문이다.


하지만, 우리가 학습시킨 모델이 학습데이터를 넘어 접하지 않은 데이터에도 좋은 추론능력을 발휘한다는 것을 당연한 것으로 받아들이면 안된다. 모델 학습을 위해 대량의 데이터 즉 "빅데이터"가 필요한 이유는, 추론시에 모델이 unseen data를 접할 경우를 최대한 줄이기 위함이다. 하지만 학습데이터셋에서 모든 데이터를 다루기에는 사실상 불가능하다. 따라서 데이터단이 아닌 모델 단에서 unseen data에 대한 대처능력을 주입해주는 것이 바로 "Inductive bias" 이다.


$$y=wx················(1)$$

$$y=wx+b················(2)$$

위의 두 1차 식을 각각 이용하여 주택가격을(y) 예측하는 회귀분석 모델을 만든다고 가정해보자 위 두식의 차이는 (2)식에 b라는 bias가 들어가있다는 것 뿐이다.
 우연히, 모든 y들이 x만으로 완벽하게 설명이 가능하다면, (1) 수식으로 만든 모델이 parameter의 수가 적을테니 더 효율적인 모델일 것이다. 하지만 추론을 해보니 어떤 데이터의 주택가격이 wx에서 b만큼의 오차를 보여주고 있다면 (1)식은 그만큼의 오차가 생길수 밖에 없다. 반면에 (2)식은 이에 대한 대처가 가능하다. 즉 식 자체가 일종의 자유도를 얻어 unseen data에 대한 대처를 할 수 있게 된 것이다. 이는 (2)식이 (1)에 비해 inductive bias가 조금 더 강한 것이다.
 
 하지만 이를 "수식에 무조건 bias를 많이 넣어주면 좋다" 라고 받아들이면 안된다. 위의 설명은 어디까지나 이해를 돕기 위한 설명이지 엄밀한 해석이 아니다.

## **Types**

그렇다면 어떤 모델들이 inductive bias가 약하거나 또는 강한지 대표적인 예시를 살펴보자.

### Less Inductive Bias Model
- MLP : MLP는 데이터에 대한 특별한 가정없이, 모든 뉴런들이 서로 독립적으로 작동하는 모델이다. 따라서 모든 데이터형태에 적용가능하지만, 특정 데이터를 처리하기 위해 inductive bias를 강하게 준 모델에 비해 성능은 떨어질 확률이 높다.
    
- Transformer : Transformer 모델은 대표적인 inductive bias가 약한 모델이다. 이는 Attention 연산이 데이터들간의 관계성을 사전에 가정하지 않고, 모든 데이터들간의 곱을 통해 관계성을 직접 밝혀내기 때문이다. 하지만 inductive bias가 약한 것이 단점인 것만은 아니다. 데이터셋에 overfitting 하지 않는다는 것은, 다양한 형태의 데이터셋에 robust 하다는 것을 의미하기 때문이다. 이러한 사실 때문에 Transformer 기반의 BERT나 GPT같은 범용 사전학습 모델이 만들어질 수 있었다. 물론 다량의 데이터가 필요하다. 이를 data-intensive라고 하며 inductive bias가 약한 모델들의 특징이다. 


### More Inductive Bias Model
- Linear Regression Model : 위에서 설명을 위해 1차 회귀분석 모델을 예로 들며 (2)식이 inductive bias가 더 강한 모델이라고 했다. 하지만 사실 Linear Regression 모델 자체가 inductive bias를 가지고 있다. 즉 종속변수 y는 독립변수들과 선형관계에 있다는 가정을 하고 있는 것이다.


- Nearest negighbors : KNN은 서로 가까운 위치에 있는 데이터들은 같은 클래스라는 inductive bias를 가지고 있는 모델이다. 


## References

1. [WikiPedia-Indutive bias](https://en.wikipedia.org/wiki/Inductive_bias)
2. [The Inductive Bias of ML Models, and Why You Should Care About It](https://towardsdatascience.com/the-inductive-bias-of-ml-models-and-why-you-should-care-about-it-979fe02a1a56)