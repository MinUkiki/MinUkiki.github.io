---
title : "Anaconda Install"
excerpt: "Anaconda Install"
categories:
  - other
tag:
  - other
toc: true
toc_sticky: true
use_math: true
---

# 개요

Ananconda 설치법을 알아보자

# Install

Ananconda 사이트에 접속 [here](https://www.anaconda.com/)

![img]({{site.url}}/assets/images/2024-03-20-Anaconda_install/image_1.png)

- Free Download 클릭

![img]({{site.url}}/assets/images/2024-03-20-Anaconda_install/image_2.png)

- email을 작성하고 체크 박스 체크후 Submit 클릭

![img]({{site.url}}/assets/images/2024-03-20-Anaconda_install/image_3.png)

- Download 클릭

- 이후 설치 파일 실행 후 설치 ( 전부 next )

![img]({{site.url}}/assets/images/2024-03-20-Anaconda_install/image_4.png)

- anaconda_prompt 설치

- anaconda_prompt 실행

- 가상환경 생성 및 활성화 ( anaconda navigator에서도 만들 수 있음 )
```
conda create -n [가상환경이름] python=3.11.9

conda activate [가상환경이름]
```

- python 실행 후 버전 확인 3.11.9로 되어있다면 성공

```
python
```