---
title: "[js] javascript의 event loop 방식"
layout: post
date: 2020-02-04
author: wnsgur
tags: js
comments: true
---

> 면접 질문 리스트 중 하나가 event loop 방식이 뭘까요? 였습니다.
> 이 대답을 구체적으로 대답하기 위해서 포스팅을 하게 되었습니다.

`event loop`를 알아보기 전에 `javascript`의 런타임 환경을 먼저 간단하게 알아보겠습니다.

### 간단한 선 수 지식
`javascript`는 `싱글 스레드` 기반입니다. 이말은 즉슨, `호출 스택`이 하나라는 것을 뜻합니다. 그리고 `콜백 큐`를 사용합니다.

![호출 스택](https://developer.mozilla.org/files/4617/default.svg)

### 자바스크립트 엔진
자바스크립트의 엔진 중 하나인 `V8`은 구글에서 개발한 엔진입니다. `node.js`도 이 엔진을 사용하고 있죠. 
*자바스크립트 엔진은 `javascript`를 해석하는 엔진으로 `렌더링 엔진`과는 다릅니다.*

엔진의 주요 구성요소는 `memory heap`과 `call stack`, `Queue` 입니다.
- memory heap: 메모리 할당이 이루어지는 공간(변수)
- call stack: 코드를 실행함에 따라 순차적으로 쌓이는 스택
- Queue: 메시지 대기열(처리할 목록들), 각 메시지는 처리할 함수를 저장 

### Call stack
`call stack`은 하나의 함수가 실행이 되면 실행이 끝날 때까지 다른 `task` 를 실행할 수 없습니다.

아래의 코드를 실행하면 어떻게 될까요?
```js
function foo(b) {
  var a = 10;
  return a + b + 11;
}

function bar(x) {
  var y = 3;
  return foo(x * y);
}

console.log(bar(7)); //returns 42
```
지역 변수들은 `heap`영역에 쌓이고 함수들은 `호출 스택`에 쌓이게 됩니다.
*참고로 `스택`은 기본적으로 first-in-last-out 구조입니다.*

즉, 위 코드를 실행시키면 호출 스택은 아래와 같이 쌓이게 됩니다.
3.foo()
2.bar()
1.console.log()
그래서 foo() 함수부터 처리하게 됩니다.

지금까지 갖고 있는 지식으로 두 가지 궁금점을 갖게 됩니다.

1. 스택이 꽉차면?
2. 하나의 스택을 차지하고 있는 함수가... 엄청난 작업량을 요구한다면? 

1번의 답변은 간단합니다. `overflow`가 발생하여 에러 메시지를 뿜뿜합니다...
2번의 경우... 스택에서 호출한 함수가 작업량이 많아 다음 스택에 쌓인 함수를 호출을 못하고 대기하게 됩니다...이를 해결하기 위해 `비동기 콜백`과 `event loop`가 나온겁니다.

# Event Queue
- `task`를 임시 저장하는 대기 큐입니다. 
- `비동기`로 호출되는 함수는 `call stack`에 쌓지 않고 `Event Queue`에 쌓습니다.
- call stack이 비었을 때, 대기열에 들어온 순서대로 수행이 됩니다.

```js
// 예시
setTimeout(function(){console.log('first')}, 0);
console.log('second');

// 결과
// second
// first
```

위 예시에서 볼 수 있듯이, `비동기 함수 setTimeeout`는 `event queue`에 쌓이고
`console.log('first')` 함수는 `call stack`에 쌓이게 됩니다.

따라서, `console.log` 함수를 먼저 실행이 되고, `stack`이 비면서 `event queue`에 저장한 함수를 `enqueue` 하여 함수를 스택에 넣게 됩니다.

그러면 비동기로 실행되는 함수는 어떤 기준으로 정할까? 라는 의문을 갖게 됩니다.

일반적인 브라우저 환경이라면, `자바스크립트 엔진`에 정의된 함수가 아닌 `Web API` 영역에 따로 정의 된 함수를 뜻합니다.

# Event Loop

![아키텍처](https://prashantb.me/content/images/2017/01/js_runtime.png)

따라서 `Event Loop`라는 것은 `event queue`에 메시지가 쌓였는지 확인하고 이를 처리하는 과정을 말합니다.


# 참조
- [MDN 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)
- [자바스크립트 런타임 개념](https://joshua1988.github.io/web-development/translation/javascript/how-js-works-inside-engine/)
- [이벤트 루프](https://asfirstalways.tistory.com/362)
