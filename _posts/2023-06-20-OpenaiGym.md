---
title : "Openai gym install on windows"
excerpt: "Openai gym install on windows"
categories:
  - AI
tag:
  - AI
toc: true
toc_sticky: true
use_math: true
---

# 가상환경

[anaconda](https://www.anaconda.com/download)로 접속 후 이메일 제출하면 메일로 다운로드 링크를 받음

설치가 완료 되면 anaconda prompt를 열어서 가상환경 생성 및 활성화

```
conda create -n [가상환경이름]

conda activate [가상환경이름]
```

python 설치

```
conda install python=3.11
```

# install gym

기본적인 환경부터 설치

```
pip install gymnasium[classic-control]

pip install gymnasium[mujoco]

pip install gymnasium[atari]
pip install gymnasium[accept-rom-license]

conda install swig
```

[visual studio c++ build tools](https://visualstudio.microsoft.com/ko/visual-cpp-build-tools/)에서 build tools 다운로드

c++을 사용한 데스크톱 개발 선택후 설치

```
pip install gymnasium[box2d]
```

# 실행

visual studio code 실행

py 파일 생성

Ctrl + Shift + p

python select iterpreter 선택 후
생성한 가상환경 선택

Ctrl + Shift + p

terminal select default profile 선택 후 command prompt 선택

```python
import gymnasium as gym
env = gym.make("LunarLander-v2", render_mode="human")
observation, info = env.reset(seed=42)
for _ in range(1000):
   action = env.action_space.sample()
   observation, reward, terminated, truncated, info = env.step(action)

   if terminated or truncated:
      observation, info = env.reset()
env.close()
```

실행 debug

[Openai gym Doc](https://www.gymlibrary.dev/index.html)에서 환경 가져오기