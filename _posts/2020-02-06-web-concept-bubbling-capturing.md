---
title: "[web] 버블링과 캡쳐링 그리고 stopPropagation, preventDefault"
layout: post
date: 2020-02-06
author: wnsgur
tags: web
comments: true
---
#javascript

> 버블링과 캡쳐링에 대해 간단히 정리하는 시간을 갖겠습니다.  
>   
# 버블링
하위 `element`에서 이벤트가 발생 했을 때, 상위 요소로 전달 되는 것이라고 정의할 수 있습니다.

브라우저는  특정 요소의 이벤트가 발생하면 상위 요소까지 이벤트를 전파합니다.

다음 예시를 보겠습니다.

```html
<div class="one">
    <div class="two">
      <div class="three"></div>
    </div>
  </div>
```

```js
var divs = document.querySelectorAll('div');
    divs.forEach(function (div, index) {
      div.addEventListener('click', logEvent);
    });

    function logEvent(event) {
      console.log(event.currentTarget.className)
    }
```

이렇게하면 콘솔에는 `three` , `two`, `one` 순서로 찍히게 됩니다.

하위 요소부터 버블링이 일어나기 때문입니다.

# 캡쳐링
캡쳐링은 버블링과의 반대로 상위 요소부터 하위 요소에게 이벤트를 전파하는 방식입니다.

```html
<div class="one">
    <div class="two">
      <div class="three"></div>
    </div>
  </div>
```

```js
var divs = document.querySelectorAll('div');
    divs.forEach(function (div, index) {
      div.addEventListener('click', logEvent, {capture: true});
    });

    function logEvent(event) {
      console.log(event.currentTarget.className)
    }
```

`div.addEventListener`의 세번째 파라미터에 객체형식으로, capture 프로퍼티에 `true` 속성만 주면 됩니다.

그러면 버블링과 반대로 `one`, `two`, `three` 순서로 콘솔이 찍힐겁니다.


# event.stopPropagation()
이벤트 전달 방식을 사용하고 싶지 않을 때, 이용하는 메소드입니다.

```js
function logEvent(event) {
	event.stopPropagation();
	console.log(event.currentTarget.className)
}
```


# event delegation
이벤트 위임은 하위 요소에 이벤트 리스너를 붙이지 않고 상위 요소에서 하위 요소들의 이벤트를 제어하는 방식입니다.

상위 요소에만 리스너를 달아두면 동적으로 생기는 하위 요소들도 손쉽게 제어할 수 있는 이점이 있습니다.

# preventDefault()
`a`태그를 클릭하면 `href`에 정의한 이동경로로 페이지가 전환됩니다. 또 `form` 태그 안에 `submit` 타입의 `input` 을 클릭하면 `form`에 지정한 `url`로 데이터를 전송합니다.

`preventDefault`는 이런 고유한 이벤트들을 막는데 사용됩니다.



# 참조
- [이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지 • Captain Pangyo](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
- [개념잡기 e.preventDefault() 와 stopPropagation() 의 차이](https://pa-pico.tistory.com/20)
