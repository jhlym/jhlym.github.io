---
title: "[git] 자주 사용하는 git 명령어"
layout: post
date: 2020-02-02
author: wnsgur
tags: git
comments: true
---

## 1. 여러 개의 remote repository 설정하기

> github와 gitlab을 같이 사용하여 동일한 소스를 양쪽에서 관리하고 싶은 상황이 와서 이 명령어를 찾게 되었습니다.

```bash
git remote add 태그명 repository 주소
```

- 예시

```bash
git remote add alt https://remote-git.example.com/project/myproj.git
```

## 2. Remote branch update

```bash
git remote update
```

## 3. Remote address (원격 주소) 변경

- Remote 주소 확인

```bash
git remote -v
```

- Remote 주소 변경

```bash
git remote set-url origin 주소
```

# 참조

- [참조1](https://www.lesstif.com/pages/viewpage.action?pageId=17105553)
