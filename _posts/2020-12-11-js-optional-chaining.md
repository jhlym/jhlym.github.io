---
title: "[js] Optional Chaning"
layout: post
date: 2020-12-11
author: wnsgur
tags: js
comments: true
---

> 역시 다른 사람의 코드를 보는게 중요한 것 같다.  
> 우물안의 개구리 식으로 내 코드만 보고 짜다간 고정적인 틀 안에 갇히기 마련이기 때문이다.  
> github에 올라 온 react-antd-admin 프로젝트의 소스를 우연히 보게 되었는데, Optional Chaining을 알게 되었고 이를 정리하는 겸 포스팅 하게 되었다.

# 들어가며
javascript 언어의 표준화와 명세화를 위해 ECMA 기술 위원회들이 담당하고 있다. 실제로 신규 기능의 제안이나 검증 및 도입들이 이뤄지고 있으며, [Gihub Repository](https://github.com/tc39) 에서 어떤 기능이 새롭게 고안되고 deprecated 되는지 확인할 수 있다.

참고로 TC39라는 위원회가 javascript 언어의 명세화를 담당하고 있다.

# Optional Chaning ?

Optional Chaining은 es2020에 있는 문법입니다.
따라서, 해당 문법을 지원하지 않는 브라우저 버전은 babel의 polyfill을 이용해서 사용해야 합니다.

# 어떻게 사용할까 ?
javascript에서는 `.`을 통해서 객체 프로퍼티에 접근을 해왔습니다. 예를 들면,

```js
var hi = {
  hello: {
    what: '?'
  }
}
console.log(hi.hello.what) // ?
```

이런식으로 객체에 접근할때 `.`을 사용해왔습니다.

만약에 없는 프로퍼티 속의 프로퍼티에 접근하면 어떻게 될까요?
예를 들면,

```js
var hi = {
  hello: {
    what: '?'
  }
}
console.log(hi.oops.fuck)
// Uncaught TypeError: Cannot read property 'fuck' of undefined
```

`oops`란 프로퍼티가 존재하지 않아, `undefined`인데 `undefined`의 `fuck`프로퍼티를 참조할려고 해서 에러가 발생합니다.

이걸 방지하기 위해선 아래 처럼 대응할 수 있습니다.
```js
if (hi.oops) {
  console.log(hi.oops.fuck)
}

// or
hi.oops && console.log(hi.oops.fuck);
```

이렇게 방어 로직이 필요한데, Optional Chaining 문법은 방어 로직 없이 깔끔하게 프로퍼티에 접근할 수 있습니다.

```js
console.log(hi?.oops?.fuck) // undefined
console.log(hi?.oops?.fuck ?? 'unknown') // unknown
```

# 마무리
실무를 하다보면, api 통신을 통해 받아 온 객체 값에 접근하는 경우가 많습니다.
특히나 있어야 할 데이터가 없는 경우도 다반사라 방어 로직을 많이 넣어둬야 하는데, 
`optional chaining` 문법을 이용한다면 손쉽게 해결할 수 있습니다.

최신 브라우저는 대부분 지원하며(물론 섭종한 IE는 제외) Node.js는 14버전 부터 지원합니다.
이전 버전에서는 Babel을 이용해서 사용하실 수 있습니다.

간만에 좋은것 하나 얻어 가네요.

# 참조
- [proposal-optional-chaining](https://github.com/tc39/proposal-optional-chaining)
- [dev-momo](https://dev-momo.tistory.com/entry/Javascript-Optional-Chaining)
- [@babel/plugin-proposal-optional-chaining](https://babeljs.io/docs/en/babel-plugin-proposal-optional-chaining.html)
- [tc39](https://ahnheejong.name/articles/ecmascript-tc39/)
- [canIuse?](https://caniuse.com/?search=optional%20chaining)