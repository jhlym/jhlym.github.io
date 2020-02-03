---
title: "[javascript] Iteration 프로토콜 그리고 for in, of 차이"
layout: post
date: 2020-02-04
author: wnsgur
tags: js
comments: true
---
> for in과 for of의 차이점을 알아보면서 iteration 프로토콜을 알게 되었습니다.  
> redux saga를 할때, generator 함수 때문에 iteration 프로토콜을 공부했었는데, 그때 정리를 안해놔서.... 
> 다시 정리 하는 겸 포스팅하게 되었습니다.

먼저 2가지 프로토콜이 있습니다.
[1. iterable protocol](#1-iterable-protocol)과 [2. iterator protocol](#2-iterator-protocol)

# 1. iterable(반복 가능) protocol
- `iteratable`은 순회할 수 있는 객체라고 말할 수 있습니다. 
- `for..of` 과 같은 loop 구조에서 iteration 동작을 정의하거나
- 사용자 정의하는 프로토콜입니다.
- `iterable`을 위해선 `object`는 `@@iterator`메소드를 구현해야 합니다.
- `String`, `Array`, `TypedArray`, `Map`, `Set`는 모두 iterable입니다.
- 위에 말한 객체들의 프로토 타입 객체들은 `@@iterator` 메소드를 가지고 있습니다.

```js
// @@iterator를 사용자 정의하는 예시
var someString = new String("hi");          // need to construct a String object explicitly to avoid auto-boxing

someString[Symbol.iterator] = function() {
  return { // this is the iterator object, returning a single element, the string "bye"
    next: function() {
      if (this._first) {
        this._first = false;
        return { value: "bye", done: false };
      } else {
        return { done: true };
      }
    },
    _first: true
  };
};
```
# 2. iterator protocol
- `iterator` 객체는 `next()` 메소드를 가지고 있습니다.
- `next()`함수는 객체를 반환하고 객체 속성에는 `done`과 `value`가 있습니다.
    - `done`은 `boolean` type 입니다.
    - `iterator`가 마지막 반복 작업을 마쳤을 경우 `true`
    - 작업이 남아 있을 경우 `false`가 됩니다.
    - `value`는 `iterator`로부터 반환되는 값입니다.
    
```js
// iterator 예시
var someString = "hi";
typeof someString[Symbol.iterator];          // "function"
var iterator = someString[Symbol.iterator]();
iterator + "";                               // "[object String Iterator]"
 
iterator.next();                             // { value: "h", done: false }
iterator.next();                             // { value: "i", done: false }
iterator.next();                             // { value: undefined, done: true }
```
# iterable, iterator 정리
- 다음 규칙을 따르고 있으면 `iterable`하다고 볼 수 있습니다.
    - `순회`할 수 있는 데이터를 가지고 있다.
    - `Symbol.iterator`을 메서드로 가지고 있다.
    - `Symbol.iterator` 메서드는 `iterator`객체를 반환해야 한다.
    - `iterator`객체는 `next` 메서드를 가지고 있어야 한다.
    - `next`메서드는 `{value: '', done: true || false}`를 반환해야 한다.
- `iterable` 반환된 객체를 `iterator`라고 부릅니다.

# for ...in
- 객체 속성들을 반복하여 작업을 수행할 수 있습니다.
- 모든 객체에서 사용이 가능합니다.
- `key`값에 접근이 가능하나, `value` 값에는 접근이 불가능 합니다.

```js
var obj = {
    a: 1, 
    b: 2, 
    c: 3
};

for (var prop in obj) {
    console.log(prop, obj[prop]); // a 1, b 2, c 3
}
```
# for ...of
- es6 추가된 새로운 컬렉션 전용 반복 구문입니다.
- `[Symbol.iterator]` 속성을 가지고 있어야 합니다.
```js
var iterable = [10, 20, 30];

for (var value of iterable) {
  console.log(value); // 10, 20, 30
}
```

# 참조
- [MDN 문서](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)
- [iterable, iterator 참조](https://medium.com/@hyunwoojo/javascript-iterator-iterable-%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-2c6a7bb42d87)
- [for..in과 for...of](https://jsdev.kr/t/for-in-vs-for-of/2938)
