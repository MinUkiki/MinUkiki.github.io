---
title : "Ubuntu 20.04 ROS Noetic Install"
excerpt: "Ubuntu 20.04 ROS Noetic Install"
categories:
  - other
tag:
  - other
toc: true
toc_sticky: true
use_math: true
---

# 개요

Ubuntu 20.04에서 ROS Noetic 설치법

# Install

1. 소스 리스트 업데이트

```
sudo apt update
```

- 시스템의 패키지 리스트를 최신 상태로 업데이트

- 패키지 매니저가 최신 소프트웨어 목록을 가져와서 사용 가능한 업데이트를 확인

2. ROS 저장소 설정

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

- ROS 공식 저장소를 시스템에 추가

- ROS 패키지를 설치하기 위해 필요한 저장소를 설정

3. 키 추가

```
sudo apt install curl

curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
```

- curl 패키지를 설치하고, ROS 저장소의 공개 키를 시스템에 추가

- 이 키는 저장소에서 패키지를 안전하게 다운로드하기 위해 사용

