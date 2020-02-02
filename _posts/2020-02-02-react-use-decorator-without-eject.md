---
title: "[React] CRA eject 없이 데코레이터 사용하기"
layout: post
date: 2020-02-02
author: wnsgur
tags: react
comments: true
---

> CRA 프로젝트 eject 없이 decorator 사용할수 있도록 설정을 알아봅니다.

# 1. 필요한 패키지 추가 (npm or yarn 이용)

```bash
// npm
npm install --save -d customize-cra
npm install --save -d react-app-rewired

// yarn
yarn add --dev customize-cra
yarn add --dev react-app-rewired
```

# 2. package.json 수정

```json
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom",
    "eject": "react-scripts eject",
}
```

# 3. 프로젝트 루트 디렉토리에 `config-overrides.js` 파일 생성

```js
const {
  addDecoratorsLegacy, // decorator를 사용할 수 있도록 해주는 config
  disableEsLint,
  override
} = require("customize-cra");

// 사용자 정의 웹팩 설정
module.exports = {
  webpack: override(disableEsLint(), addDecoratorsLegacy())
};
```

# (optional) Mobx 사용 설정

### 1. 필요 패키지 다운로드

```bash
// babel 플러그인 설치
yarn add --dev @babel/plugin-proposal-decorators @babel/plugin-proposal-class-properties

// 추가적인 es7 데코레이터 설치
yarn add --dev core-decorators

// mobx 설치
yarn add mobx mobx-react
```

### 2. package.json 수정

```json
...
"babel": {
    "presets": [
      "react-app"
    ],
    "plugins": [
      [
        "@babel/plugin-proposal-decorators",
        {
          "legacy": true
        }
      ],
      [
        "@babel/plugin-proposal-class-properties",
        {
          "loose": true
        }
      ]
    ]
  }
...
```

# 참조

- [velog 포스팅](https://velog.io/@wlsdud2194/Mobx-%EB%8D%B0%EC%BD%94%EB%A0%88%EC%9D%B4%ED%84%B0-yarn-eject-%EC%97%86%EC%9D%B4-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
