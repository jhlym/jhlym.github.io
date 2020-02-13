---
title: "[js] Javascript setTimeout과 Promise"
layout: post
date: 2020-02-13
author: wnsgur
tags: js
comments: true
---

> jsconf 채널의 영상을 보고 정리하는 겸 포스팅 해봤습니다.  
> 영상링크 : [JSconf](https://www.youtube.com/watch?v=cCOL7MC4Pl0)

# # setTimeout 그리고 Promise 

웹 페이지에는  `메인  스레드` 라는 것이 있습니다.
이 `메인 스레드`는  `javascript` 렌더링이 실행되고, `DOM`이 있는 곳입니다.

발표자 `Jake Archibald` 는  인간을 멀티 스레드라고 비유합니다.  팔, 다리, 얼굴 등등 여러부위를 각각 움직일 수 있기 때문이죠. 하지만 `재채기`를 하는 상황이라면?
인간은 본인의 의도완 상관없이 얼굴이 찌푸려지며 `재채기` 밖에 못하는 `싱글 스레드` 상황으로 돌아갑니다.

이런 `재채기`를  `setTimeout` 함수와 같은 상황이라고 jake는 말합니다.

```js
setTimeout(callback, ms)
```

`setTimeout`에 파라미터로 받은 `callback` 함수는 `task Queue`에 들어갑니다. 그러고 `event loop`가 돌면서 큐에 있는 작업들을 순서대로 꺼내서 실행 시킵니다.

하지만 브라우저에 업데이트가 생겨 렌더링과 함께 작업이 걸린 경우는 조금 더 복잡합니다.

왜냐하면 렌더링하는 작업은 또다른 큐에서 관리하기 때문이죠. 그렇기 때문에 발표자 jake는 `requestAnimationFrame` 사용을 권장하는데 이것과 관련해서는 나중에 정리해서 포스팅하겠습니다. (아직 저도 제대로 이해가 안됐습니다 ㅠㅠ)

그리고 `Promise`와 `setTimeout`의 우선순위는 `Promise`가 높다고 하네요. 즉, 동시에 실행된다면, `Promise`가 먼저 실행됩니다.

이 이유는 `MicroTask`와 관련이 있다고 하는데… 글들을 찾아보기도 했고 30분 가량 되는 영상을 봤음에도 불구하고 머리로는 잘 이해가 되지 않는것 같습니다.

이 부분 또한 시간 내서 정리해 봐야 겠습니다.



## 생각 정리
promise와 settimeout 중에 어느 것이 우선순위가 높을지….최근에 받은 질문이였습니다.  

왜 이런 질문을 했을까?? 라는 생각을 해보면서 검색을 해보니,  주로 이벤트전 페이지를 개발하다 보면 몇초후에 팝업창을 띄우고 애니메이션 효과를 넣고 등등  `setTimeout`을 사용 할 일이 많았던 것으로 보입니다. 그래서 이런 우선순위에 대한 것을 이해하고 있는지에 대한 것을 물어봤던 것 같습니다.


## 참조
- [JSconf](https://www.youtube.com/watch?v=cCOL7MC4Pl0)
- [비동기와 Promise #3 NonBlock](https://blog.javarouka.me/2016/11/12/javascript-async-promise-3/)


#javascript
