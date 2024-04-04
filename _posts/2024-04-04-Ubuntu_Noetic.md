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

4. ROS 설치

```
sudo apt update

sudo apt install ros-noetic-desktop-full
```

- ROS Noetic Desktop-Full 패키지를 설치

- 이 패키지는 ROS의 주요 컴포넌트와 도구, 라이브러리 등을 포함하고 있어서 일반적으로 사용되는 모든 기능을 제공

5. ROS 환경 설정

```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc

source ~/.bashrc
```

- ROS 환경 설정을 자동으로 로드하기 위해 ~/.bashrc 파일에 ROS 환경 설정을 추가

- 매번 터미널을 열 때마다 ROS 환경이 자동으로 설정

6. 의존성 패키지 설치

```
sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

- ROS를 사용하기 위해 필요한 추가적인 패키지를 설치

- 이 패키지들은 ROS를 사용하는 데 필요한 도구와 라이브러리를 포함

7. rosdep 초기화

```
sudo rosdep init

rosdep update
```

- ROS의 의존성 패키지 관리자를 초기화하고 업데이트 

- ROS 패키지를 빌드하고 실행하는 데 필요한 모든 의존성 패키지를 관리할 수 있음

