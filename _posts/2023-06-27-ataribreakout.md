---
title : "Atari - Breakout DQN 실습"
excerpt: "Atari - Breakout DQN 실습"
categories:
  - AI
tag:
  - AI
toc: true
toc_sticky: true
use_math: true
---

# 개요
- [코드는 파이썬과 케라스로 배우는 강화학습] 책의 내용을 사용하였음

[github][githublink]

[githublink]: https://github.com/rlcode/reinforcement-learning-kr-v2/tree/master/3-atari/1-breakout-dqn

- 2023년 6월 실행할때의 환경 설정을 저장하기 위함
- 글에 없는 라이브러리 버전은 직접 찾야함
- GPU에서 구동하고 싶어서 먼길을 돌아감 물론 깃헙에서 요구하는 tensorflow==2.1.0이 더이상 지원 하는것도 있었음
- CUDA, cuDnn등은 다른 블로그 참고


# 가상환경

- Windows Anaconda 가상환경에서 진행
- 가상환경 이름은 atari로 진행하였음

```
# 가상환경 생성
conda create --name atari python=3.8.0 

# 가상환경 활성화
conda activate atari

# jupyter notebook 다운로드
conda install jupyter notebook

# ipykernel 다운로드
pip install ipykernel

# 가상환경 kernel 추가
python -m ipykernel install --user --name [가상환경이름] --display-name "[가상환경이름]"

# 필요한 라이브러리 설치 ( 권한이 필요하면 --user를 추가 )
pip install keras==2.6.0
pip install tensorflow==2.6.0
pip install tensorboard==2.6.0
pip install scikit-image==0.16.2 --user
pip install numpy==1.19.5
pip install gym==0.16.0

# jupyter notebook 실행
jupyter notebook
```

- 본인은 여기까지 해서 라이브러리로 인한 오류는 없었음
- 하지만 훈련하는 부분에서 atari게임에 대한 오류가 생길 것임
- 그러면 다음을 진행

```
pip install gym[atari]
conda install -c conda-forge atari_py
```
[.rar 파일 다운로드][rarlink]

[rarlink]: http://www.atarimania.com/rom_collection_archive_atari_2600_roms.html ".rar 파일 다운로드"


- 위 링크로 들어가서 .rar 파일을 다운로드한 뒤 압축풀기

```
python -m atari_py.import_roms [다운로드 받은 파일 경로]
```

- 이제 Atari - Breakout 게임이 훈련이 됨
- 코드는 위 링크의 깃헙 참고

# 학습 및 테스트 결과

- 학습 결과
- 6000 Episode / Max Scroe : 400 / score avg : 203 / Q avg : 5.3
- 테스트 결과


![gif]({{site.url}}/assets/images/2023-06-27-ataribreakout/1.gif)
![gif]({{site.url}}/assets/images/2023-06-27-ataribreakout/2.gif)
![gif]({{site.url}}/assets/images/2023-06-27-ataribreakout/3.gif)