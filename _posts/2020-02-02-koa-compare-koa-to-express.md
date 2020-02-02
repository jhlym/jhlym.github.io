---
title: "[koa] Koa vs Express"
layout: post
date: 2020-02-02
author: wnsgur
tags: koa
comments: true
---

> Koa vs Express 무슨 차이점이 있는 지 머리속으로 대충 알고 있어서... 정리할겸 포스팅합니다.

# Koa 특징

- `Promise`와 `async` function을 이용합니다.
  - callback 지옥에서 벗어날 수 있다....
  - 에러를 다루기 쉽다
- `ctx.request`, `ctx.response` 사용
  - 노드의 `req`, `res` 객체 대체
- node.js의 http 모듈을 추상화 한 것입니다.
- Koa는 다른 미들웨어를 포함하지 않습니다.

# 참조

- [koa docs](https://github.com/koajs/koa/blob/master/docs/koa-vs-express.md)
- [개인 블로그1](https://devsoyoung.github.io/posts/koa-api-tutorial/)
