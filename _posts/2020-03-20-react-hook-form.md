---
title: "[react] react hook form 라이브러리 후기"
layout: post
date: 2020-03-20
author: wnsgur
tags: react
comments: true
---
> react-hook-form 이란 유효성 체크 `hook`라이브러리를 약 2주? 정도 사용하고 느낀 점을 적어보았습니다.

# 장점

## 1. 공식 문서가 잘 정리되어 있다.
[공식 홈페이지](https://react-hook-form.com/)에 접속해보면 알 수 있듯이, 라이브러리에 대한 사용법, 예시가 잘 정리되어 있습니다. 문서가 잘 되어 있다는 것은, 빠른 시간 안에 라이브러리의 사용법을 파악하고 본인의 프로젝트에 적용시킬 수 있어, 라이브러리 선정에 어느정도 큰 부분을 차지합니다....(본인 기준)

## 2. 라이브러리 유지/보수가 잘 되고 있다.
`react-hook-form` 메인 개발자인 [bill](https://github.com/bluebill1049)님은 `issue`에 있어 보통 `7일`이내에 해결을  해주시고 업데이트도 잘 해주시는 것 같습니다! 

2020년 3월 20일 기준으로 오픈 되어 있는 이슈 건수는 4건 밖에 없습니다....

## 3. 높은 자유도
`hook` 패턴으로 짜였기 때문에, 유효성 체크 관련 로직들을 `react-hook-form`을 이용하여, 재사용할 수 있습니다.
참고로 `react-hook-form`은 `React.Context`를 기반으로 컴포넌트 간 데이터를 교환합니다.
validation check 하는 로직들을 빼왔고, 다른 UI 라이브러리와 결합할 수 있도록 만들어 졌기 때문에, 높은 자유도를 갖습니다!!

## 4. 입력 검증 라이브러리 yup/joi 와 찰떡 궁합
`react-hook-form` 개발자도 `yup 혹은 joi` 라이브러리와 결합을 염두해두고 개발했기 때문에, `yup / joi` 라이브러리를 `react-hook-form`에 쉽게 붙여서 쓸 수 있습니다!

음... 그러니깐 `react-hook-form`을 이용해서 유효성 체크할 컴포넌트 대상을 등록해놓고, `yup이나 joi`라이브러리를 이용하여 해당 컴포넌트에 입력 값을 개발자가 미리 정의 해둔 `schema`를 이용하여 `validation` 체크를 할 수 있게 해줍니다!

***[여기](https://react-hook-form.com/advanced-usage#SchemaValidation)를 참조하시면 좋습니다.***

```js
const schema = yup.object().shape({
  firstName: yup.string().required(),
  age: yup
    .number()
    .required()
    .positive()
    .integer(),
});
```
`schema`는 위의 예시 코드를 보면 바로 알 수 있듯이, `firstName`이란 필드는 `string` 형태만 들어오고, 필수 입력 값이 다란 것을 정의 해놓는 것입니다.

# 단점
음... 제가 쓰면서 단점이라고 느꼈던 것은, 단 하나입니다.
만약에 `redux`를 이용해서 `state` 관리가 필요하다면, `dispatch` 하는 부분을 일일히 구현해야 합니다.

대체품으로 `redux-form`이 있습니다...`redux-form`은 애초에 redux store에 등록할 컴포넌트를 지정해놓고, 특정 컴포넌트 안에 입력 값이 들어올때마다 `dispatch`가 일어나서 `redux store`에서 `state` 값을 관리하기 때문에, 일일히 `dispatch` 부분을 구현하지 않아도 됩니다...

유효성 체크 라이브러리는 많으니, 잘 찾아보시고 선정하시길 바랍니다~
