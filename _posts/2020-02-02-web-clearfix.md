---
title: "[web] clearfix"
layout: post
date: 2020-02-02
author: wnsgur
tags: web
comments: true
---
> clearfix를 사용하는 이유를 알아보자...

### 개요

`부모 요소`가 있고,  `자식 요소`가 있습니다.
`자식 요소`에게 `float` 속성을 주면, `부모 요소`는 `자식 요소`의 높이를 인식하지 못합니다.

이것은 css를 만든 개발자가 float 속성을 가로로 배치하기 위해 만든것이 아니기 때문에 생긴 버그입니다.

본래 `float` 속성은 `img`태그가 텍스트와 공존하기위해 만든 것이였다고 합니다.

따라서, `float`를 맥인 `자식 요소`의 높이를 `부모 요소`가 인식하기 위해서는 `clearfix`라고 하는 꼼수가 필요합니다.

`clearfix`는 버그를 고쳐준다는 의미에서 사용되었습니다.

### float를 clear하는 4가지 방법
1. 가상요소 `::after` 사용
2. `overflow` 속성 사용
    - `부모 요소`에 `overflow:hidden` 속성을 줍니다.
    - 이렇게하면 `block format context`가 생기기 때문에 `float`현상을 해결할 수 있습니다.
    - [block format context 자세히 알아보기](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Block_formatting_context)
3. 빈 엘리먼트로 `clear`속성 적용
4. `float`로 대응

첫 번째 방법만 구체적인 예로 확인해보겠습니다.

### clearfix(권장사용)
```css
.parent {}
.child {
    float: left;
}
.clearfix::after {
    content: block;
    clear: both;
    display: block;
}
```

```html
<div class="parent clearfix">
    <div class="child"></div>
</div>
```

# 참조
- [블로그1](https://nyhya.tistory.com/379)
- [블로그2](https://takeuu.tistory.com/60)
