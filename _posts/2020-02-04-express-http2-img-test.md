---
title: "[express] express를 이용한 http2 간단 테스트"
layout: post
date: 2020-02-04
author: wnsgur
tags: express
comments: true
---
> 그냥 인터넷을 떠돌던 중 프로토콜 관련 기사를 끄적이고 있었는데...  
> http2가 기존 http/1.x 훨씬 빠르다는 것을 확인하고 한번 테스트할겸 express 서버에 http2 프로토콜을 적용 시켜보는 간단한 예제를 진행해봤습니다.

[소스 코드 전문](https://github.com/jhlym/node-server-playground/commit/4d1fe83d083da5d00a1071fa36c189645cd5b1ed) 여기서 소스 확인할 수 있습니다.

참고로 저는 `typescript`를 적용시킨 `boiler plate`를 가지고 프로젝트를 진행했습니다.
`express` 프로젝트에 `typescript`를 적용하고 싶으시면 [여기](https://wnsgur.dev/2020/02/02/expresss-typescript-apply.html)서 확인하고 진행해보세요.... 금방합니다 ㅎㅎ;

# openssl을 이용한 인증서 발급
`http2` 프로토콜을 사용하려면 `https` 통신이 기본입니다. 즉 `tls` 보안 통신이 되어야 합니다.

지금 집 데스크탑(windows 10)으로 작업을 하기 때문에, `windows 10` 기준으로 `openssl`을 이용하여 `인증서` 발급 과정을 설명하겠습니다.

[여기서](https://sourceforge.net/projects/openssl/) openssl 프로그램을 설치합니다.
그리고 터미널 환경에서 openssl 명령을 실행시키기 위해 [환경 변수 설정](https://blog.naver.com/PostView.nhn?blogId=baekmg1988&logNo=221454486746)이 필요합니다.
한번 쓰시고 말거라면 openssl.exe 파일이 있는 경로에 터미널을 열고 실행하시면 됩니다.

### 개인키 발급

```bash
genrsa -des3 -out private.pem 2048
```
터미널에 위 명령어를 치고 비밀번호를 입력하면 `개인키`가 발급됩니다. `private.pem` 제가 임의로 지정한 파일명입니다. 여러분이 임의로 정의해서 사용하셔도 됩니다.

### 공개키 발급
```bash
rsa -in priavte.pem -pubout -out public.key
```
이전에 발급 받은 `개인키`를 이용해서 `공개키`를 만듭니다.

### CSR 생성(로컬 테스트에선 생략 가능)
SSL 인증의 정보를 암호화하여 `인증기관`에 보내 인증서를 발급받게하는 신청서입니다.
정보항목에는 국가코드, 도시, 회사명, 부서명, 이메일, 도메인주소 등이 들어가있습니다.

```bash
req -new -key private.key -out private.csr
```
### CRT 생성
사설 CA에서 인증까지 받은 인증서를 만들어보려고 합니다.
#### root CA key 생성
```bash
genrsa -aes256 -out rootCA.key 2048
```
#### rootCA 사설 CSR 생성
rootCA.key를 사용하여 10년 짜리 rootCA.pem을 생성합니다.
```bash
req -x509 -new -nodes -key rootCA.key -days 3650 -out rootCA.pem
```
커스텀 CA인 rootCA의 인증을 받아 private.crt로 생성합니다.
```bash
x509 -req -in private.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out private.crt -days 3650
```
사실 제가 진행하는 프로젝트는 private.key와 private.crt만 이용합니다.

# express 서버 구성
필요한 부분만 발췌했습니다. 전체소스는 [여기서](https://github.com/jhlym/node-server-playground/commit/4d1fe83d083da5d00a1071fa36c189645cd5b1ed) 확인해보세요.

```js
const app = express();
const options = {
  key: fs.readFileSync(path.join(__dirname, "/config/cert/private.key")),
  cert: fs.readFileSync(path.join(__dirname, "/config/cert/private.crt")),
  passphrase: "admin"
};

app.get("/test", (req, res) => {
  res.set("Content-Type", "image/png");
  const r = fs.readFileSync(path.join(__dirname, "../assets/img/momo.png"));
  res.send(Buffer.from(r));
});

app.use(express.static("images"));
app.use(cors());

const port = 3000;
spdy.createServer(options, app).listen(port, () => {
  console.log(`App started listening on PORT ${port}`);
});
```
자 이렇게 서버 구성을 하고 돌리려니깐....
`How to fix (node:12388) [DEP0066] DeprecationWarning: OutgoingMessage.prototype._headers is deprecated in windows`
에러를 내뿜내요...
스택오버플로우는 사랑입니다...[여기](https://stackoverflow.com/questions/56697360/how-to-fix-node12388-dep0066-deprecationwarning-outgoingmessage-prototype) 친절히 답변이 있습니다.

제가 사용한 Node 버전은 12.13.1 LTS 버전이였습니다. 하지만 `spdy`에서 사용하는 `OutgoingMessage.prototype._headers`는 Node 12버전에선 `deprecated`..... 그래서 노드 버전을 낮춰야 했습니다. ㅠㅠ

# NVM 설치
노드 버전 관리를 위해서 기존 설치된 것을 지웠습니다. `C:\Users\현재 로그인 계정\AppData\Roaming\npm` 디렉토리도 삭제했습니다. 참고로 여기를 지우면 global로 설치했던 npm들 다 날라갑니당.... 조심조심ㅎㅎ;

지운 뒤에는 `nvm`을 설치했습니다. [nvm github](https://github.com/coreybutler/nvm-windows/releases) 여기서 받으세요
- `nvm install <필요버전>`
- `nvm list`
- `nvm use <사용할 버전>`

전 11.0 버전을 다시 설치했습니다.

[참조](http://hong.adfeel.info/backend/nodejs/window%EC%97%90%EC%84%9C-nvmnode-version-manager-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/)

# 테스트
`http/1.1`과 `http2` 프로토콜일 때, 비교를 해봤습니다. 
음...별 차이가 없는거 같습니다...라고 생각할때, 새벽이라 머리가 굳었었습니다.....
[http1과 http2 차이](https://medium.com/@shlee1353/http1-1-vs-http2-0-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EA%B0%84%EB%8B%A8%ED%9E%88-%EC%82%B4%ED%8E%B4%EB%B3%B4%EA%B8%B0-5727b7499b78)를 보면 다음과 같습니다.

![http/1.1과 http/2 동작 방식](https://miro.medium.com/max/664/1*rf2AnDQyHfGO_ThYfb-hWA.png)

http/1.1는... 90년대 개발되고 여태 ..읍읍
아무튼 보면 `하나의 커넥션`은 하나의 요청만 처리할 수 있습니다.
반면에, `http/2`는 `하나의 커넥션`에 다수의 요청을 처리할 수 있는거죠.
그렇기에 제가 짠 코드는 잘못된겁니다. 저는 이미지 파일 하나만 넣고 테스트 하려 했으니......
다음에 시간이 날때, 이미지 100개정도 때려넣고 두 개의 속도를 비교해보겠습니다.
그리고 `http` 통신 방법과 `http2`에 대해서도 자세히 포스팅 하겠습니다.

### ps
참고로 테스트를 하다보면 `크롬 개발자도구 네트워크 탭`에 "transferred"란 문구를 볼 수있습니다.
![](https://i.stack.imgur.com/PMFNR.jpg)
이것은 브라우저에 캐싱 되어 있을 가능성이 있어서 입니다.
[참조](https://webmasters.stackexchange.com/questions/121785/what-is-resources-in-google-chrome-develper-tools-network-section)
