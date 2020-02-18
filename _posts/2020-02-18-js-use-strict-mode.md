---
title: "[javascript] use strict mode"
layout: post
date: 2020-02-18
author: wnsgur
tags: js
comments: true
---
# use strict mode란?
Ecma5에서 나온 문법으로 다음과 같은 역할을 합니다.

1. 기존에 무시되던 에러들을 throwing 합니다.
2. 자바스크립트 엔진의 최적화 작업을 어렵게 만드는 실수를 바로 잡습니다.
3. ECMAscript의 차기 버전들에서 정의될 문법을 금지합니다.


정리하자면 문법과 런타임 시 일어날 수 있는 문제들을 더 엄격히 체크한다고 선언하는 것입니다.

한 파일 전체에 strict mode를 적용시킬 수 있고, 일부 함수에서만 동작하도록 설정할 수 있습니다.

저는 이렇게 뜻과 사용법을 정의 했는데, 구체적으로 어떤 상황에 쓰일까란 고민을 하게 되어 다른 블로그들을 참조하다 보니 어느정도 이해가 갔습니다.

밑에는 예시입니다.

```js
"use strict"
// var, let, const 등 변수를 생성한다는 키워드를 쓰지 않아 오류가 발생합니다.
test = 4;
```


```js
"use strict"; 
// 읽기 전용 객체는 쓰는 것이 불가능합니다.
var testObj = Object.defineProperties({}, { prop1: { value: 10, writable: false // by default }, prop2: { get: function () { } } }); testObj.prop1 = 20; testObj.prop2 = 30;

출처: https://beomy.tistory.com/13 [beomy]
```

```js
// get으로 선언된 객체는 수정할 수 없습니다. (getter-only property 수정 불가능)
"use strict"; 
var obj2 = { get x() { return 17; } }; obj2.x = 5; // throws a TypeError
```

이외에도 `use strict`의 여러 예시가 있습니다.
[자바스크립트 엄격 모드(strict mode)](https://beomy.tistory.com/13) 여기서 한번 예시들을 확인하시길 바랍니다!


## 참조
* https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode
* [자바스크립트 엄격 모드(strict mode)](https://beomy.tistory.com/13)
