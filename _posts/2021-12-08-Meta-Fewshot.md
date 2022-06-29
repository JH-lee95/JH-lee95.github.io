---
title: 메타러닝(Meta Learning)과 퓨샷러닝(Few-Shot Learning)
background : /img/posts/no_need_data_anymore.png
date: 2021-12-08 10:25:20 +0200
tags: [DEEP-LEARNING]
category : DEEP-LEARNING
# last_modified_at: 2021-12-08T10:25
---
Meta Learning은 "Learn to Learn"이라고 한다. "배우기 위해 배운다"? 굉장히 모호한 말이다.  
하지만 사실 우리는 모델을 학습 시킬 때 이미 Meta Learning을 끊임없이 적용하고 있다.   

딥러닝 모델로 최상의 결과를 내기 위해, 러닝레이트, 레이어의 개수, 노드의 수 등 여러 하이퍼파라미터를 조절하는데 이것 역시 Meta Learning의 일종이다.  

감성분류를 하는 지도학습을 예로 들면, 모델은 주어진 텍스트 데이터가 긍정/부정 인지 분류하는 테스크를 진행한다. 이것을 우리는 "Learning(학습)"이라고 한다.  
하지만, 일반적으로 한번의 학습만에 최적의 결과를 내는 것은 쉽지 않다. 이때 위에서 언급했던 것처럼, 여러 하이퍼파라미터를 조정해가면서, 테스크에 맞는 최적의 세팅을 찾아나선다. 이것이 Meta Learning의 예이다. (~~근데 이건 모델을 학습 시키기 위해 사람이 Learning한 것인가?.....~~)

이렇게 "배우기 위해 배운다" 라는 개념을 Few-Shot Learning에 적용해보자.  퓨샷러닝은 인간의 귀차니즘을 해결하기 위해 굉장히 적은 양의 데이터로 모델을 학습시키는 것을 말한다.  

일반적으로 분류모델에서의 지도학습이, 주어진 Input Data의 정확한 Class를 예측하는 것이라면, 퓨샷러닝의 핵심은 주어진 데이터가, 다른 데이터들과 얼마나 비슷한가?(또는 다른가?)를 학습 하는 것이다.

*이것을 메타러닝과 연관지어 보자면, 주어진 데이터의 Class를 정확하게 예측하는 모델을 **"학습"** 시키기 위해 유사성의 파악할 수 있는 방법을 **"학습"** 시키는 것이다. 즉 모델이 단순히 Class를 예측하는 방법을 배운 것이 아니라, 주어진 데이터 자체를 이해하는 방법을 배운 것이다.(나는 이렇게 이해했다.)*

*따라서 기존의 모델이 가지고 있지 않은 새로운 Class의 데이터가 들어와도, 모델이 그 동안 배운 데이터 이해 방법을 토대로, 새로운 데이터 역시 이해할 수 있는 것이다.* 

![Supervised](https://i.imgur.com/6MAisQL.png)

예를 들어, 이미지 분류 모델이, 위와 같은 데이터셋을 가지고, 지도학습을 진행했다고 하자. 


![Supervised](https://imgur.com/zQNCvWE.png)

근데 갑자기 학습할 때는 존재하지 않았던 Class의 이미지를 예측한다고 해보자.(이것을 Query라고 한다.)

만약 단순히 Class를 예측하는 학습을 진행한 모델이라면 "아니 내가 이걸 어떻게 알아?" 라고 말하겠지만, 괜찮다. 우리의 모델은 이미 이미지를 이해하는 방법을 배웠으니까! 
다만, 약간의 도움이 필요하다. Armadillo와 Pangollin 사진 몇장을 모델에게 보여주고, "이걸 참고해서 맞혀봐!" 라고 지시하면 된다.

이때 우리는 이 몇장의 참고용 사진을 Support Set이라고 한다. 

그리고 k-way와 n-shot이라는 개념이 등장한다. k-way는 새로운 데이터의 class개수를 의미하고, n-shot은 새로운 데이터 샘플의 개수를 의미한다.

위의 사진은 Aramadillo와 Pangolin 두개의 Class가 있으므로 2-way이고, 동시에 두개의 데이터 (2 row)가 있으므로 2-shot이다. 

따라서 데이터 샘플이 하나면 one-shot이고, 새로운 데이터가 없으면 이를 zero-shot이라고 한다.



## References
1. [(Youtube) Few-Shot Learning](https://www.youtube.com/watch?v=hE7eGew4eeg)