---
title : "Linux Anaconda Download"
excerpt: "Linux Anaconda Download"
categories:
  - other
tag:
  - other
toc: true
toc_sticky: true
use_math: true
---

# 개요

설치는 [Anaconda](https://docs.anaconda.com/free/anaconda/install/linux/) 문서와 동일하나 마지막에 내가 겪은 오류에 대해서 해결방법을 작성한다.

# Install

```
apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6
```

## 패키지 다운로드
```
curl -O https://repo.anaconda.com/archive/Anaconda3-<INSTALLER_VERSION>-Linux-x86_64.sh
```
INSTALLER_VERSION은 [버전 목록](https://repo.anaconda.com/archive/)에서 원하는 버전을 선택한다

예) `curl -O https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh`

```
bash ~/Downloads/Anaconda3-<INSTALLER_VERSION>-Linux-x86_64.sh
```

버전은 위에 다운로드 받은것과 동일한 버전을 사용

실행하고 다음 순서를 따라하면 설치가 완료된다.

1. `Enter`
2. `yes`
3. 스크롤이 끝날때 까지 `Enter`
4. `yes`
5. `Thank you for installing Anaconda3!` 가 뜬다면 설치가 완료

## 오류

터미널에 `conda`를 실행하면 `conda : command not found` 오류가 발생하면서 실해되지 않는다.

터미널에 `export PATH=~/anaconda3/bin:$PATH` 를 실행하면 정상적으로 실행되는것을 확인할 수 있다.