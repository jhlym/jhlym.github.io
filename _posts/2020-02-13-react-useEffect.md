---
title: "[React] React useEffect"
layout: post
date: 2020-02-13
author: wnsgur
tags: react
comments: true
---

# useEffect
> 매번 useEffect를 사용하면서  이것이 어떻게 동작하는지에 대해 정확히 알지 못했습니다.    
> 그래서 정리하는 글을 포스팅하게 되었습니다.  

# why useEffect ?
`useEffect`는 `side effect` 를 관리하기 위한 `hook`입니다. 

 `class component`에서 제공하던 `componentDidMount` , `componentDidUpdate` , 그리고`componentWillUnmount` 메소드를 합친 것과  같습니다.

컴포넌트가 렌더링이 된 후에 호출이 됩니다!

# How to use ?
사용 방법은 [Using the Effect Hook – React](https://ko.reactjs.org/docs/hooks-effect.html) 공식 홈페이지에 자세히 나와있습니다.

필히 참고하셔서 보시길 바랍니다!

저는 어떻게 사용하는지에 대한 예제는 위에 있으니, `useEffect`를 사용할 때 알아둬야 될 것들을  정리해봤습니다.

## 1. useEffect 내부에 side effect 함수 정의하기
`side effect`를 일으키는 함수는 `useEffect`의 첫 파라마터인 일급 객체 함수 안에 정의 되어야 합니다. 예시는 아래와 같습니다.
```js
useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // Specify how to clean up after this effect:
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

```


## 2. useEffect의 첫 번째 파라미터 함수 안에 정의된 state 들
```js
const [count1, setCount1] = React.useState(0);
const [count2, setCount2] = React.useState(0);

React.useEffect(() => {
	consol.log(count1);
	consol.log(count2);
});
```

`useEffect` 첫 번째 파라미터 함수 안에 정의한 변수를 주시하면서, 변경 되었을때만 `useEffect` 함수를 호출 합니다.

위 예시에서 봤을 때, `count1`과 `count2`  두 변수 중 하나라도 변경이 되면 `useEffect` 함수를 호출하게 됩니다.

다만 `count1`과 `count2` 두 변수 모두 이전 상태와 같다면 호출 되지 않습니다.

## 3. useEffect 함수 내에 정의 되지 않은 state 값이 바뀌면?
```js
const [count1, setCount1] = React.useState(0);
const [count2, setCount2] = React.useState(0);
const [count3, setCount3] = React.useState(0);

React.useEffect(() => {
	consol.log(count1);
	consol.log(count2);
});

<div onClick={() => setCount3(count3 + 1)}>test</div>

```

Test 버튼을 클릭하게 되면 `useEffect` 함수는 호출이 될까요?

컴포넌트 내부 state 값이 변경 되었기 때문에 호출이 됩니다. 따라서, 특정 값이 변경될 때만 `useEffect` 함수를 호출하고 싶다면……
다음 섹션에서 알아 보겠습니다.

## 4. 두번째 파라미터에 배열 형태로 관찰할 state 값을 넘긴다.
```js
const [count1, setCount1] = React.useState(0);
const [count2, setCount2] = React.useState(0);
const [count3, setCount3] = React.useState(0);

React.useEffect(() => {
	consol.log(count1);
	consol.log(count2);
}, [count1, count2]);

<div onClick={() => setCount3(count3 + 1)}>test</div>

```

 `useEffect` 함수 두 번째 파라미터에 관찰할 state 값을 배열 형태로 넘겨 주면 됩니다.

위에 예시를 봤을 때, `count1`과 `count2`가 바뀔때만 `useEffect` 함수를 호출 합니다.

# 정리
React Hook 중에 `useEffect` 함수를 왜 사용하는지와 사용 시 어떤 부분을 조심해야 할지 알아봤습니다.

자세한 것은 꼭 공식문서를 참조하셔서 예제 코드를 따라해보세요.

제가 설명한 것 중 틀린 부분이 있다면  꼭 댓글 달아주세요!


#React
