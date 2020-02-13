---
title: "[js] Javascript Number type의 toLocaleString"
layout: post
date: 2020-02-13
author: wnsgur
tags: js
comments: true
---

# Number type의 toLocaleString
> Javascript의 Number type에 toLocaleString 메소드를 알고나니, 숫자에서 천단위로 콤마 찍는 것도 편해졌을 뿐더러 국가별 단위를 쉽게 찍을 수 있었다.  

`toLocaleString()` 함수는 `string`을 반환하는데  언어별로 표현할 수 있는 특징을 같이 포함합니다.

예를 들어 일본의 엔화를 찍는다고 가정하면…(이시국에?)

```js
// the Japanese yen doesn't use a minor unit
console.log(number.toLocaleString('ja-JP', { style: 'currency', currency: 'JPY' }))
// → ￥123,457

```

이런 식으로 표현이 가능합니다.

꼭 화폐 단위가 아니라도 숫자를 어떤 식으로 표현할지에 대해  옵션 값을 주어서 `string` 값을 얻을 수 있습니다.

# 관련 라이브러리
[Dinero.js - Documentation](https://sarahdayan.github.io/dinero.js/)


# 참조
[Number.prototype.toLocaleString() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)
[JavaScript toLocaleString() Method](https://www.w3schools.com/jsref/jsref_tolocalestring.asp)
[Currency list](https://www.currency-iso.org/dam/downloads/lists/list_one.xml)

#javascript
