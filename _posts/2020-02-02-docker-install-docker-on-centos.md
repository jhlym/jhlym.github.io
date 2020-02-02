---
title: "[docker] CentOS docker 설치"
layout: post
date: 2020-02-02
author: wnsgur
tags: docker
comments: true
---

> CentOS 7에 docker 설치  
> yum 패키지 관리자 사용을 전제

# 설치

### 1. yum 패키지 업데이트

```bash
yum -y update
```

### 2. 도커 설치를 위한 필수 패키지 설치

```bash
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

### 3. docker repository 추가

```bash
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
```

### 4. docker 설치

```bash
sudo yum install docker-ce docker-ce-cli containerd.io
```

### 5. docker 실행

```bash
sudo systemctl start docker
```

## sudo 권한 없이 docker 실행 하기

> docker 명령어를 사용할 때 docker 데몬이 root 권한으로 실행되기 때문에 sudo 권한을 이용하여 docker 명령어를 실행해야 합니다.  
> 따라서, 일반 계정에서 docker를 사용할 때는 로그인 계정을 docker 그룹에 추가하면 됩니다.

```bash
sudo usermod -aG docker $USER
```

# 참조

- [docker 공식 홈페이지](https://docs.docker.com/install/linux/docker-ce/centos/)
- [블로그1](https://www.slipp.net/questions/485)
