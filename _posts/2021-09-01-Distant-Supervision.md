---
title: Distant Supervision 이란?
# author : Jeonghwan Lee
img : /img/posts/guess.jpg
date: 2021-09-01 17:36:20 +0200
tags: [ML]
category : ML
# last_modified_at: 2021-09-08T09:09
---
Knowledge Graph 관련 연구를 하면서, Distant Supervision이란 기법을 알게됐다.    
Distant Supervision은 label이 없는 상황에서 두 entity 간의 관계를 추측 하기 위해 사용되는 방법이다.     


지도학습은 학습과정에서 feature와 target이 필수이다. 하지만 우리가 가진 데이터가 target label을 가지고 있지 않다면, 직접 labeling을 해주어야 한다. 이 작업은 귀찮고 소모적이다.

두 사람 사이의 관계를 예측하는 모델을 만든다고 해보자.  
예를 들어, ("미쉘오바마, "버락오바마")의 관계를 예측하기 위해서는 우리는 먼저 두 사람 사이의 관계가 labeled된 데이터셋을 만들어야 한다. (이 예시에서 label은 "결혼" 정도로 할 수 있겠다.) 

이때, 우리의 학습 데이터셋이 아닌, 사전에 만들어진 어떠한 데이터베이스(Freebase)가 있고, 그 데이터베이스에 두 entity 사이의 관계를 설명해주는 데이터가 있다면, 우리는 이를 이용하여 우리의 학습 데이터셋을 만들 수 있다.

- "A person has two legs" => (person,has,legs)   

Freebase에 위와 같은 데이터가 있다고 하자. 그러면 우리는 'person과 legs가 나오면 그 둘의 관계는 has 이다' 라고 가정할 수 있다.
이를 그대로 우리의 데이터셋에 적용하는 것이다.

- (Peter,strong legs), (Tom,short legs), (Harry,long legs) => "has"  

위 처럼, entity들이 'person'과 'legs'로 태깅만 될 수 있다면, 우리는 비슷한 문장이 나올때 모두 'has'로 labeling 할 수 있는 것이다.

이것이 바로 Distant Supervision 이다.



## References
1. [Distant Supervision](http://deepdive.stanford.edu/distant_supervision)