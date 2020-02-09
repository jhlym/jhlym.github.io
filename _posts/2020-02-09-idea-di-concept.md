---
title: "[idea] DI 개념"
layout: post
date: 2020-02-09
author: wnsgur
tags: idea
comments: true
---
#디자인패턴

# DI (Dependency Injection)
의존성 주입은 외부에서 객체를 생성해서 파라미터 혹은 다른 방법으로 넘겨주는 방식을 말합니다.
**어디까지나 제가 정의한 개념입니다….틀린 부분이 있으면 지적해주세요!**

자바를 예로 들어서 사족을 달면  `A class`와  `B class`가 있다고 가정합니다.
`B class` 내부에서는 `A class의 instance`를 사용하는 구조입니다.

```java
class B {
	A a;
	B(){
		this.a = new A();
	}
}
```

`B class`는 지금  `A class`에 의존하는 의존관계가 생성되었습니다.

이것을  `Injection` 형식으로 바꾸겠습니다.
```java
class B {
	Instance i;
	B(instance) {
		this.i = instance;
	}
}
B test = new B(new A());
```

이렇게 파라미터에  `A class` 인스턴스를 넘겨주게되면  `Injection`을 하게 됩니다. 즉, 외부에서 객체를 생성해서 넘겨주는 개념입니다.

# Spring에서의 DI
스프링에서 `DI`는  `Life cycle`관리와 `instance` 생성을 `container`인 스프링이 대신 해주는 역할입니다.

`instance`의 생성 및 관리 주체가 `나`가 아닌  `container`가 되기 때문에  `Inversion Of Controls`가 생기게 됩니다.

# typedi(node module) 
위 패키지를 설치하면 `js`도 `di`를 사용할 수 있습니다. 데코레이터는 es7 문법이고 아직 정식적인 문법이 아니기에, 사용을 하시려면 `babel`과 함께 사용하셔야 됩니다.

`typedi`의 대표적인   `decorator`을 알아보겠습니다.

### 1. @Service()
이 데코레이터를 사용한 `class` 내부에서는 `@Inject`  데코레이터을 사용할 수 있으며,  다른 `class`에서 `@Inject`를 다알 수 있습니다.

### 2. @Inject()
컨테이너에 등록되었거나 `@Service` 데코레이터로 선언된 class는 `@Inject` 데코레이터를 이용하여 다른 클래스에 주입할 수 있습니다.



> docker 명령어를 사용할 때 docker 데몬이 root 권한으로 실행되기 때문에 sudo 권한을 이용하여 docker 명령어를 실행해야 합니다.  
> 따라서, 일반 계정에서 docker를 사용할 때는 로그인 계정을 docker 그룹에 추가하면 됩니다.

```bash
sudo usermod -aG docker $USER
```

# 참조

- [docker 공식 홈페이지](https://docs.docker.com/install/linux/docker-ce/centos/)
- [블로그1](https://www.slipp.net/questions/485)
