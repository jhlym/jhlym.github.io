---
title: "[docker] 도커를 이용하여 gitlab 구축"
layout: post
date: 2020-02-04
author: wnsgur
tags: docker
comments: true
---

> gitlab을 스스로 구축해보고 ci/cd 툴을 직접 이용해보는 것을 오늘 목표로 했습니다.
> mac에서 진행 했습니다.

대학생 때는 `ubuntu`를 회사원이 되면서는 `centos`를... 이렇게 리눅스를 다뤄본거 같습니다.
최근에 많이 이용했던 `centos`를 이용하기로 했습니다.

먼저 `mac`을 사용하고 있기 때문에, `vagrant`를 이용했습니다. `vagrant`는 `가상 머신`을 빌드하고 다루는 툴입니다.

### homebrew 설치
`mac` 사용자라면 `homebrew` 패키지 관리 도구는 필수겠죠?!!!

아래 명령어를 이용하면  다운 받으실 수 있습니다.
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
참조 [homebrew 공홈](https://brew.sh/index_ko)

### homebrew를 이용한 vagrant 설치
```bash
brew cask install virtualbox
brew cask install vagrant
brew cask install vagrant-manager
```
참조 [install vagrant by using homebrew](https://sourabhbajaj.com/mac-setup/Vagrant/README.html)

### vagrant를 이용한 리눅스 설치
먼저 적당한 폴더에 이동합니다.
그리고 저희는 `centos`를 설치하기 위해서 아래 명령어를 입력해줍니다.

```bash
vagrant init centos/7
```

그러면 현재 경로에 `Vagrantfile` 파일이 생성된 것을 확인할 수 있습니다.
이 파일에는 가상머신 환경 설정 값들이 있습니다.

그리고 정신건강을 위해 `vagrant-vbguest` 플러그인을 설치합시다! 

```bash
# 플로그인 설치
vagrant plugin install vagrant-vbguest

# 가상머신 생성 및 실행
vagrant up
```
가상머신을 실행시키면 `host 2222 port`와 `가상머신의 22 port`가 바인딩 됩니다. default 값으로 저렇게 세팅이 되어 있고 `Vagrantfile`에서 수정할 수 있습니다.

```bash
# 가상머신에 접속
vagrant ssh

# (optional) 이 방법으로도 접속이 가능합니다.
# ssh 클라이언트 프로그램이 깔려 있어야 합니다. 
# mac은 open ssh가 기본적으로 깔려 있습니다.
ssh vagrant@127.0.0.1 -p 2222

# 가상머신 중지 명령어 참조하세요
vagrant halt
```

처음 접속하면 `vagrant` 계정이 있습니다. `root` 비밀번호는 `vagrant`로 되어 있습니다.
*로그인 되어 있는 사용자에 비밀번호를 설정하고 싶으면 `passwd` 명령어를 이용하시면 됩니다.*

참조
[vagrount box](https://app.vagrantup.com/centos/boxes/7)


### docker 설치
[docker 설치 방법](https://wnsgur.dev/2020/02/02/docker-install-docker-on-centos.html)을 참조 하시거나

`Vagrantfile`에 다음과 같이 환경 설정 값을 주면, 가상머신이 시작될 때 docker를 설치하고 이미지를 다운 받을 수 있습니다.

```vagrant
Vagrant.configure("2") do |config|
  config.vm.provision "docker" do |d|
    d.build_image "/vagrant/app"
  end
end
```

자세한 내용은 [여기서](https://www.vagrantup.com/docs/provisioning/docker.html) 확인하시길 바랍니다.

### docker compose 설치
저는 `docker compose`를 이용해서 docker 이미지를 pull하고 컨테이너를 생성해서 실행 시킬겁니다. 그래서 `docker compose`를 먼저 설치 합니다.

```bash
#1
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.3/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

#2
sudo chmod +x /usr/local/bin/docker-compose

#3
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

#4
docker-compose --version
```
[docker compose 설치 참조](https://docs.docker.com/compose/install/)

### yaml 파일 작성
```yaml
web:
  image: 'gitlab/gitlab-ce:latest'
  restart: always
  hostname: 'gitlab.example.com'
  environment:
    GITLAB_OMNIBUS_CONFIG: |
      external_url 'https://gitlab.example.com'
      gitlab_rails['gitlab_shell_ssh_port'] = 234
      # Add any other gitlab.rb configuration here, each on its own line
  ports:
    - '80:80'
    - '443:443'
    - '234:22'
  volumes:
    - '/srv/gitlab/config:/etc/gitlab'
    - '/srv/gitlab/logs:/var/log/gitlab'
    - '/srv/gitlab/data:/var/opt/gitlab'
```

가상머신에서 `22번 포트`는 이미 사용 중입니다. host -> guest 접속할 때, `22번 포트`를 사용한다고 정의했기 때문입니다. 따라서 전 `234`라고 다시 정의 했습니다.
*포트:도커 컨테이너가 이용할 포트*
- 443 port는 https
- 80  port는 http
- 234 port는 gitlab shell ssh port

[yaml 파일 작성 참조](https://docs.gitlab.com/omnibus/docker/)
*yaml은 환경 설정 값을 관리하기 위한 하나의 format 입니다.*

yml 파일이 작성이 되었다면, `docker-compose up -d` 명령어를 통해 도커 컨테이너를 실행 시킵니다.

`docker ps -a` 명령어를 통해 도커 컨테이너의 status를 확인할 수 있습니다.

여기까지 따라왔다면, `gitlab` 도커 컨테이너가 실행되고 있을겁니다.
참고로 뭔가 에러가 났다하면 `docker logs -f 컨테이너 id 값`을 통해 확인할 수 있습니다.

### 방화벽 오픈
`80 port` 방화벽을 오픈해줍니다.

```bash
# 포트 오픈
firewall-cmd --permanent --zone=public --add-port=80/tcp
# 오픈한 포트 적용 위해 방화벽 재구동
firewall-cmd --reload
```

### 가상머신 포트와 호스트 OS 포트 바인딩
그리고 `Vagrantfile`에서 다음 구문을 추가해줍니다.
```Vagrantfile
config.vm.network "forwarded_port", guest: 80, host: 80
```

자 여기까지 했다면, 다 끝난겁니다. 
네... 저도 여기까진 인터넷 보면서 슝슝슝 30분도 안돼서 했습니다....
그런데 브라우저를 켜고 `127.0.0.1`을 쳐보니 gitlab 페이지가 안뜨더랍니다.... 가상머신을 다시 실행 해보기도 하고...`localhost:80`, `127.0.0.1:80` 이런식으로 쳐도 안돼더라고요...

docker 상태를 확인해보니 또 정상적으로 동작하고 있고... 

그래서 삽질 하던 중 다음 명령어를 그냥 쳐봤습니다.
```
ssh vagrant@127.0.0.1 -p 2222
ssh vagrant@localhost -p 2222
```
이렇게 하다보니 핑거프린트 등록하겠냐는 문구가 뜨면서 뭔가 느낌이 쎄 했습니다.
등록하고 나서 브라우저에 주소창에 `127.0.0.1:80`을 치니 들어가지는 겁니다.

왜 갑자기 됐는지는 자세히 모르겠.... 그래서 `127.0.0.1`과 `localhost`로 ssh 접속하는 것이 무슨 차이가 있는지 한번 조사 해봐야겠습니다.

`gitlab`을 설치 했으니, 이제 gitlab에서 제공하는 플러그인을 이용해서 `CI/CD` 환경을 구축해보렵니다!!
