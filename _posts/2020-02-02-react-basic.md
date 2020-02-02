---
title: "[react] Back To Basic React"
layout: post
date: 2020-02-02
author: wnsgur
tags: react
comments: true
---

> React 공홈 문서를 읽고 중요한 부분들은 제 메모리에 저장하기위해 정리 해봤습니다.

# JSX

> jsx는 xml 문법처럼 데이터 표현식입니다.

```javascript
const element = <img src={user.avatarUrl} />;
```

- 컴파일이 끝나면 js 함수 호출에 의해 `JSX`는 javascript `객체`로 인식됩니다.
- `JSX`에 삽입된 모든 값들은 렌더링 전에 [이스케이프](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-in-html)를 하기 때문에 `XSS`공격을 방지할 수 있습니다.
- `JSX`는 `React.createElement()`를 호출하여 컴파일합니다.

```javascript
const element = React.createElement("h1", { className: "greeting" }, "Hello, world!");
```

# 이벤트 핸들러

- React에서 기본 동작을 방지하기 위해선 `preventDefault`를 명시적으로 호출해야 합니다.

# Hook

> Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다.  
> HoC을 대체합니다.(무려 새 컴포넌트를 추가하지 않아도...)

### Hook을 사용하는 이유?

1. 비즈니스 로직을 재사용하기 위함

- wrapper 지옥에서 벗어날 수 있다.

2. 상태 관리 메소드를 더 단순하고, 재사용성을 높이기 위해!
3. `class` 사용을 지양하기 위해서!

```
Class는 최근 사용되는 도구에도 많은 문제를 일으킵니다. 예를 들어 Class는 잘 축소되지 않고, 핫 리로딩을 깨지기 쉽고 신뢰할 수 없게 만듭니다. 우리는 코드가 최적화 가능한 경로에서 유지될 가능성이 더 높은 API를 제공하고 싶습니다.
```

## Effect Hook

- `useEffect`는 함수 컴포넌트 내에서 side effects를 수행할 수 있게 도와줍니다.
- `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` API를 하나로 통합한 것입니다.
- [예제](https://ko.reactjs.org/docs/hooks-effect.html)

## Hook의 규칙

- 최상위(at the top level)에서만 Hook을 호출해야 합니다. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하지 마세요.
- React 함수 컴포넌트 내에서만 Hook을 호출해야 합니다. 일반 JavaScript 함수에서는 Hook을 호출해서는 안 됩니다. (Hook을 호출할 수 있는 곳이 딱 한 군데 더 있습니다. 바로 직접 작성한 custom Hook 내입니다. 이것에 대해서는 나중에 알아보겠습니다.)

### Hook API

https://ko.reactjs.org/docs/hooks-reference.html
