---
layout: post
title: "[express] express에 typescript 적용방법"
date: 2020-02-02
author: wnsgur
tags: express
comments: true
---

> 이번 목표: 그냥 typescript를 사용해보고 싶었다!  
> 따라서, express에 typescript를 적용해봅니다.

# 1. package.json 생성

```bash
npm init -y
```

# 2. express/typescript/@types 설치

```bash
npm i -S express
npm i -D typescript
npm i -D @types/node @types/express
```

# 3. Typescript 컴파일 옵션 설정

아래 명령어로 `tsconfig.json` 파일 생성

```bash
npx tsc -init
```

# 4. tsconfig.json 수정

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es6",
    "moduleResolution": "node",
    "outDir": "dist"
  },
  "include": ["src/**/*"]
}
```

# 5. package.json 수정

```json
{
  "scripts": {
    "start": "tsc && node dist"
  }
}
```

# 6. src/index.ts 작성

```js
import express from "express";

const app = express();

app.get("/", function(req: express.Request, res: express.Response) {
  res.send("Hello world");
});

app.listen(3000, function() {
  console.log("Example app listening on port 3000!");
});
```

# 7. 실행

```bash
npm start
```

# 참고

- [참고 블로그 1](https://gongzza.github.io/javascript/nodejs/typescript-express-starter-1/)
