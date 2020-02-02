---
title: "[React] 상태관리 라이브러리 Mobx"
layout: post
date: 2020-02-02
author: wnsgur
tags: react
comments: true
---

> React로 개발을 하다보니 상태관리 라이브러리 redux를 알게되었고,  
> 그보다 더 접근하기 쉬운 mobx라는 라이브러리를 알게 되었습니다.  
> 그래서 mobx가 어떤 라이브러인지 간단하게 정리하는 포스팅을 하게 되었습니다.

# mobx란?

간단하고 확장성에 용이한 상태 관리 라이브러리 입니다.

# 핵심 개념 및 data flow

![data flow](https://mobx.js.org/assets/flow.png)

## 1. observable & observer

observable는 관찰 대상의 state 값이라고 이해하면 쉽습니다.  
observer는 observable state 값을 변경하는 주체입니다.  
즉, observer에 의해 state 값이 변경됩니다.

## 2. Computed values

성능 최적화에 주로 쓰입니다.  
연산에 기반이 되는 값이 변경되었을 때만, 연산하게 합니다.

## 3. Reactions

state 값이 변경되었을 때, 어떤 event를 trigger 시킬지 정의합니다.

## 4. Action

state의 상태 변화를 일으킵니다.

# 참조

- [mobx 공식 홈페이지](https://mobx.js.org/README.html)
- [velopert님의 포스팅](https://velog.io/@velopert/begin-mobx)
