---
title: "[React] React project boiler pate 개발하기"
layout: post
date: 2020-02-02
author: wnsgur
tags: react
comments: true
---

> React로 개발하면서 나만의 boiler plate를 만들어 놓으면 좋겠다고 생각했습니다.  
> 기본적으로 저는 css 라이브러리 중에 semantic-ui를 좋아합니다.  
> 공홈에 예시가 정말 자세히 나와있고, 커스텀도 가능하기 때문입니다.  
> 그리고 상태관리에는 Saga를 이용할 건데요.  
> 왜냐하면 dispatch 후에 다시 dispatch가 필요한 경우에도 유용하고,  
> socket.io를 이용하기에도 적합하고, 무엇보다 saga는 순수 함수형을 지향하기 때문에 모듈화가 더 쉽기 때문입니다.

# 프로젝트 디렉토리 기본 구조

```
asset         # 정적 리소스(css, scss, img, svg 등등...)
api           # restful api 호출 관련 디렉토리
components    # 재사용 가능한 컴포넌트
containers    # 비즈니스 로직이 들어간 컴포넌트
pages         # 컨테이너 컴포넌트들을 조합하여 만든 페이지 컴포넌트
layout        # 페이지 컴포넌트마다 쓰이는 공통 레이아웃
route         # route 컴포넌트를 관리하는 디렉토리
redux         # ducks pattern으로 action type, create action function, reducer를 하나의 파일에서 관리합니다.
utils         # 유틸 함수
```

# 사용 라이브러리

- `react`
- `react-dom`

- Router

  - `react-router-dom`

- Redux

  - `redux`
  - `redux-actions`
  - `react-redux`
  - `redux-saga`
  - `redux-devtools-extension`

- UI

  - `semantic-ui-react`
  - `semantic-ui-css`
  - `styled-components`

- API

  - `axios`

- Utils

  - `react-helmet-async`
  - `qs`

# 주의 사항

- `yarn` 패키지 모듈 관리자 사용을 권장합니다.
- `yarn install`로 `module`을 설치한 후에 `yarn start`로 실행하길 바랍니다.
