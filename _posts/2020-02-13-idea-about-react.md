---
title: "[idea] React 라이브러리에 대한 나의 생각"
layout: post
date: 2020-02-13
author: wnsgur
tags: react
comments: true
---

# React에 대한 나의 생각
> React를 왜 사용하는지.... 왜 편리한지 제가 경험했던 것들을 토대로 적어봤습니다.

## React를 사용하며 좋았던 점
- `DOM`제어의 편의성

`JSX` 문법을 통해서 `DOM`에 대한 제어권을 가져오기 때문에 `DOM`에 불필요한 속성들을 추가할 필요가 없어졌습니다.

`id` 혹은  `class`를 이용하여 `DOM`을 선택하는 일이  없어졌습니다.

참고로 `JSX`는 `React.createElement()` 함수에 의해 `javascript`  객체로 인식합니다.

- js 로 모든 것을 해결

`styled-components` , `emotion`같은 모듈을 사용하면
`css`나 `scss` 같이 마크업을 꾸며주는 작업을 `js`  하나의 파일 안에서 모두 가능하게 해주기 때문입니다.

- 프로젝트 생성의 편리함

페이스북에서 개발한 `CRA`는  `react`관련 프로젝트를 빠르게 실행하기 위해 `boiler plate `를 제공합니다.

`CRA` 에서는 `react` 프로젝트에서 `es6`문법을 사용하기 쉽도록  `webpack` 설정이  되어 있고, 그밖에  프로젝트 `build`시에는 `코드 스플리팅`을 지원하고  프로젝트 내에서 `js`파일이 아닌 다른 형식의 파일을 `import ` 시켜서 js 코드를 이용하여 사용할 수 있습니다.

- pure javascript 사용

jquery같이 라이브러리에 의존적인 상황을 만들지 않습니다. 즉, 더이상 라이브러리에서 제공하는 메소드에 의존적이지 않게 됩니다.


#react
