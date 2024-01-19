---
title : "유니티 ML Agents 연습 예제"
excerpt: "유니티 ML Agents 연습 예제"
categories:
  - AI
tag:
  - AI
toc: true
toc_sticky: true
use_math: true
---

# 개요

- 설치 및 github에서 예제를 다운로드 받는건 설명하지 않음
- ML Agents 연습 예제를 실행

---

# ML Agents 시작하기

[ML Agents](https://github.com/Unity-Technologies/ml-agents)

1. 깃헙에서 다운로드 받고 폴더안의 Project를 유니티로 실행

2. 경로를 따라서 Scene을 실행

> Assets -> ML-Agents -> Examples -> [게임] -> Scenes -> [선택]
ML Agents에서 제공하는 많은 게임 환경들이 존재한다.
그중에서 Hallway 환경을 사용

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_1.png)

유니티에서 실행되는것을 확인할 수 있다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_2.png)

먼저 Hallway 환경은 파란색 상자의 에이전트가 정면에 있는 표지판을 통해 O,X를 파악한 뒤 해당 목표가 있는 위치로 이동하는 게임 환경이다.

다음으로 Hierarchy 창이다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_3.png)

이창을 통해 게임의 환경 요소가 무엇이 있는지 알수있다.

이 게임 환경에는 땅, O, X, 목표지점, 벽, 에이전트 등이 있다.

지금은 예제를 실행해보고 ML Agents가 어떻게 작동하는지 어떠한 기능이 있는지 확인하는게 우선이기 때문에 환경 및 에이전트를 수정하지 않는다.

에이전트를 선택하고 Inspector 창은 다음과 같다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_4.png)

각각이 무슨 역할을 하는지는 다른 글에서 설명을 하고 그림에서 빨간 박스부분이 ML Agents에서 제공하는 스크립트이다.

Hallway Agent 스크립트를 통해 보상, 액션 등 환경과의 상호작용을 우리가 코드를 통해 작성할 수 있다.

그대로 게임을 실행 하면 에이전트가 스스로 앞의 모양을 확인하고 정확한 목표로 움직이는 모습을 볼 수 있을것이다.

이는 에이전트 컴포넌트에 Behavior Paramerters 스크립트에서 Model 부분을 보면 이미 학습된 모델이 들어가 있는 것을 확인할 수 있다.

따라서 현재 상태에서 게임을 실행하게 되면 모델이 학습된 결과를 보여주게 된다.

이번엔 우리가 직접 Hallway 환경에서 모델을 학습하고 실행까지 해본다.

Model을 None으로 변경 한 후 터미널을 열어서 가상환경을 실행

아래의 코드를 작성하자

```
mlagents-learn "[파라미터 yaml 경로]"
```

yaml 파일 경로는 다운로드 받은 깃헙 폴더에서

> config -> 'ppo' or 'sac' -> Hallway.yaml

ppo와 sac는 강화학습 알고리즘이니 원하는 것으로 선택

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_5.png)

여기까지 되었다면 실행한다.

실행을 하게 되면 다음과 같은 모습이 나올 것이다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_6.png)

다시 유니티로 돌아가서 게임을 실행해보자

유니티의 게임창에서는 에이전트가 움직이면서 빠른 속도로 학습하는 모습을 확인할 수 있다.

터미널에서는 다음과 같이 학습되는 것을 확인할 수 있다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_7.png)

아마 학습이 오래 걸릴 것이다.

일단 학습을 멈추고 ( 터미널에서 Ctrl + c ) 다은은 Ml agents의 명령어에 대한 설명이다.

터미널에서 다음 코드를 실행하면 설명 들이 나올 것이다.

```
mlagents-learn -h
```
---

많이 사용되는 주요 명령어

- trainer_config_path
  - 깃헙에서 내려받은 폴더의 config 폴더에 위치한 .yaml(학습 알고리즘 설정)파일이 위치한 경로

- env
  - 학습을 실행시킬 환경읠 경로, 빌드된 파일이 위치한 경로

- run-id
  - 학습이 진행되면서 나오는 텐서보드, 에이전트 모델 등을 저장할 폴더의 이름 ( 기본값 : ppo )

- num-envs
  - 학습을 수행할 때 여러 개의 환경을 동시에 실핸하고 한꺼번에 데이터를 수집하는 분산학습을 진행

- base-port
  - 여러 환경을 동시에 학습을 진행할때 동일한 포트를 사용하면 오류가 발생함 따라서 포트값을 다르게 설정하여 다른 환경을 동시에 학습

- resume
  - 같은 run-id를 가진 학습 결과가 이미 존재할 때, 해당 학습된 모델로부터 이어서 학습을 진행 할때 사용

- force
  - 같은 run-id를 가진 학습 결과가 이미 존재할 때, 해당 학습된 모델로부터 처음부터 새롭게 학습을 진행 할때 사용

- unference
  - 학습이 아니라 추론을 진행하기 위해 사용 resume과 함께 사용해야함

- width, height
  - 학습할때 실행되는 윈도우의 크기에 대한 너비와 높이를 결정

- no-graphics
  - 학습할때 렌더링을 하지 않는 명령어 당연히 학습 속도가 빨라지지만 학습 화면이 보이지 않고 만약 이미지 데이터를 입력으로 쓰는 경우 해다 ㅇ데이터가 검은 화면으로 나오는 문제가 발생할 수 있음

---

주요 명령어들을 확인해 보았다.

학습 속도를 높여주는 명령어들이 존재하는게 확인되었다.

Hallway에 적용을 하고 마무리를 하겠다.

먼저 Hallway 환경을 빌드를 진행한다.

```
mlagents-learn [trainer-path] --env[env-path] --run-id=[run-id] --num-envs=[number]
```

no-graphics는 사용하지 않겠다. 학습하는 모습을 보면 연습하는 느낌이 더욱 들기 때문이다.

너비와 높이도 원한다면 추가해도 좋다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_8.png)

저장폴더의 이름은 'Test1', 학습 환경의 수는 4개로 설정을 하였다.

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_9.png)

학습이 완료 되었다면 텐서보드를 통해 결과를 그래프로 볼수있다.

터미널에서 아래 코드를 실행하자

```
tensorboard --logdir=results\Test1 --port=6006
```

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_10.png)

![img]({{site.url}}/assets/images/2023-09-15-ML_agent2/img_11.png) ( 텐서보드 실행창 추가 예정)

학습이 잘 된것을 확인할 수 있다.

이제 우리가 학습시킨 모델을 환경에서 실행

앞선 예제와 같이 잘 작동하는 모습을 볼수있다.