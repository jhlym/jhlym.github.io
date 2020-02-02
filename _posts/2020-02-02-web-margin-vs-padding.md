---
title: "[web] margin vs padding"
layout: post
date: 2020-02-02
author: wnsgur
tags: web
comments: true
---
> margin vs padding 언제 사용하면 좋을까.... 고민했습니다. 
> 평소에는 아무 생각없이 섞어서 사용했는데, 과연 어떤 상황에 어떤 속성을 사용해야 하는지 궁금해져서 포스팅하게 되었습니다.

`margin`과 `padding`은 여백을 주는 의미에서 같습니다.  

### 쓰임새
하지만 `margin`은 `외부 여백`을 말하고, `padding`은 `내부 여백`을 의미합니다.

보통 웹 페이지의 최상단 또는 최하단일 경우 `padding`을 사용합니다.

### 차이점
`margin`은 `자동 병합`이 생기고, `padding`은 그렇지 않다는 것입니다. 인접한 `margin`끼리 겹치게 되면 겹치는 것 중 큰 `margin`이 적용됩니다.

### 한눈으로 알아보기
![margin vs padding](https://uxengineer.com/wp-content/uploads/2018/10/css-box-model-with-dimensions-1024x441.jpg)

### 알아두면 좋은 것!
> box-sizing의 border-box 속성을 이용하면 margin, padding, border 크기를 element에 포함시킬 수 있습니다.

```css
div {
   box-sizing: border-box;
}
```
![box-sizing](https://uxengineer.com/wp-content/uploads/2018/10/css-box-model-border-box-1024x449.jpg)

# 참조
- [stackoverflow](https://stackoverflow.com/questions/2189452/what-is-the-difference-between-margin-and-padding-in-css)
- [코딩 팩토리](https://coding-factory.tistory.com/187)
- [ux engineer](https://uxengineer.com/padding-vs-margin/)
