# Container
<br>

-----------------------

### 도커란?

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------

<div align="center">
    <img src="./image/docker.png" width="50%"></img>
</div>

## 개념
도커란 컨테이너 기반의 오픈소스 가상화 플랫폼이다. 
도커도 가상화의 기술 중 하나라고 볼 수 있다. 

서버 가상화의 경우에는 하드웨어 통째로 가상화하여 리소스들을 논리적으로 나누어 여러 개의 가상 서버에 할당하는 기술이다.

하지만 컨테이너는 하나의 OS 환경에서 애플리케이션을 실행하기 위한 영역을 여러 개로 나누어 사용하며 OS에서는 이런 컨테이너 하나하나가 프로세솔 인식이된다. 

컨테이너를 이용하면 하나의 호스트 OS에서 여러 개의 OS를 동시에 사용할 수 있고, 
다른 컨테이너로 복제와 이식성이 뛰어나다. 
또한 가상화 환경 위에 또 다른 OS를 동작시킬 필요가 없어 개별 컨테이너가 필요로 하는 하드웨어 리소스가 줄어든다. 

무엇보다 각 컨테이너는 애플리케이션과 그 의존성을 포함하고 있지만 OS의 커널을 공유하기에 가볍고 더 빠르다.

컨테이너 기술을 활용하여 가장 활발하게 쓰이는 것이 바로 도커이다. 


## 도커의 구성 요소
1. Docker CLI

    Docker CLI란 도커 명령어가 설치된 서버를 말한다.

    도커 멸령을 통하여 컨테이너를 관리할 수 있다.

    ```
    docker run my-application
    ```

2. Docker Host

    도커 호스트의 경우에는 도커 엔진이 설치된 서버를 말한다.

    Docker Host는 컨테이너와 이미지를 관리하고 실제 컨테이너를 실행하는 역할을 수행한다. 

3. Image

    이미지는 컨테이너를 생성할 때 필요한 요소로 애플리케이션과 의존성이 포함된 읽기 전용 파일 시스템이다. 
    
    또한 여러 개의 계층으로 구성되어 있으며 새로운 변경 사항이 하나씩 쌓ㅇ이는 구조이다.


4. Container

    컨테이너는 이미지에서 생성된 인스턴스로 애플리케이션과 그 의존성을 포함하고 호스트와 다른 컨테이너로부터 격리된 자원과 네트워크를 사용하는 프로세스이다.

    이미지는 일기 전용으로 사용되고 컨테이너의 여러 변경은 컨테이너 계층에 저장된다. 

    하지만 이런 저장된 데이터들은 휘발된다.

5. Registry

    이미지를 저장하고 배포하는 저장소 이다. 

    대표적으로 도커 허브가 있다.

## 도커 라이프사이클 관련 명령어
1. 컨테이너 시작

    ```shell
    docker run -it [--rm] -d --name [container] -p [port] -v [mount point]
    ```

    사용 옵션
    
    - -it: 인터랙티브 모드
    - --rm: 컨테이너 종료 시 자동 삭제
    - -d: 백그라운드 모드
    - --name: 컨테이너 이름 설정
    - -p: 포트 매핑
    - -v: 볼륨 마운트

2. 컨테이너 상태 확인

    ```shell
    docker ps  # 실행 중인 컨테이너 목록
    docker ps -a # 모든 컨테이너 목록 (종료된 컨테이너 포함)
    docker inspect [container] # 컨테이너 세부 정보
    ```

3. 컨테이너 일시중지 및 재개

    일시중지는 SIGSTOP 시그널을 전달하여 프로세스를 잠시 중지한다.

    재개는 SIGCONT 시그널을 전달한다. 
    ```shell
    docker pause [container]
    docker unpause [container]
    ```

4. 컨테이너 종료

    ```shell
    docker stop [container]
    docker kill [container]
    ```

5. 컨테이너 삭제

    ```shell
    docker stop [container]
    docker rm [container]

    docker rm -f [container]

    docker container prune
    ```

6. 도커에 명령어 실행

    exec 명령어는 실행 중인 컨테이너에 사용되는 명령어이기에 특정 이슈 해결을 위해 많이 사용된다.


    ```shell
    docker exec -it [container] bash
    ```

7. 도커 로그 

    컨테이너에서 로그를 다루기 위해서는 애플리케이션에서 stdout과 stderr로 내보내야한다. 

    애플리케이션에서 로그를 내보내면 도커가 해당 로그를 받고 쌓아서 로깅 드라이버가 처리하도록 한다.
    로깅 드라이버는 다양하게 많지만 기본적으로는 json-file 드라이버를 사용한다.

    json-file 드라이버를 사용하면 호스트에 파일로 저장이 되고 호스트에 있는 log 에이전트가 엘라스틱서치나 splunk 같은 중앙화된 로그 시스템으로 파일들을 전달한다.

    ```shell
    docker logs [container]
    docker logs -f [container]
    ```

## 도커 네트워크

도커 네트워크는 컨테이너간의 통신을 위한 네트워크 환경을 제공한다. 

1. docker0 브릿지 네트워크

    docker0은 도커가 기본적으로 생성하는 가상 네트워크 브릿지이다. 

    도커를 설치하면 자동으로 생성되며 호스트에서 컨테이너로 기본 네트워크 인터페이스 역할을 수행한다. 
    즉, 호스트와 컨테이너 간의 통신을 하도록 한다. 

2. veth

    veth는 가상 이더넷 디바이스이다. 하나의 엔드포인트가 호스트 네트워크 네임스페이스에 있고, 다른 엔드포인트가 컨테이너의 네임스페이스에 있다.

    그래서 veth는 브릿지와 컨테이너 간의 실제 실제 네트워크 연결을 제공한다. 

3. 컨테이너 내의 eth

    컨테이노 내부에서는 일반적으로 eth0 인터페이스를 통해 네트워크에 접근한다. 

    이 eth0이 veth의 한쪽 엔드포인트에 해당한다. eth0은 컨테니어 내부에서 네트워크 통신을 담당하며 외부 네트워크와 통신하거나 다른 컨테이너와 통신할 때 사용이 된다.

4. 네트워크 동작

    1. 컨테이너 생성

        도커는 veth를 생성하고 호스트와 컨테이너에 연결이 된다. 

        호스트쪽 veth는 docker0 브릿지에 연결되도 컨테이너쪽 veth는 컨테이너의 eth0과 연결된다. 

        그리고 docker0 브릿지가 컨테이너의 eth0에 ip 주소를 할당한다.

    2. 컨테이너간 통신

        컨테이너A에서 컨테이너B와 통신을 위해선 컨테이너A의 eth0을 통해 veth를 거쳐 docker0으로 전달되어 docker0이 컨테이너B veth로 전달하고 veth가 컨테이너B의 eth0으로 데이터를 전달한다.

    3. 호스트와 컨테이너간 통신

        호스트에서 데이터를 전달하려고 하면 호스트에서 데이터를 docker0으로 전달하고 docker0는 해당 컨테이너의 veth로 전달하고 이후 컨테이너의 eth0으로 데이터가 전달이 된다. 


다음으로는 도커 네트워크 드라이버를 알아보도록 하겠다.

도커 네트워크는 여러 드라이버를 사용하는데, 기본적으로 브릿지와 호스트 그리고 none 네트워크 드라이버를 사용한다.

1. 브릿지 네트워크 드라이버

    브릿지 네트워크는 docker0과는 다른데, docker0 도커 설치 시 자동으로 생성되는 브릿지 네트워크이지만 브릿지 네트워크는 사용자 정의 브릿지 네트워크이다. 

    그래서 더 유연하게 네트워크 구성을 할 수 있다. 

    브릿지 네트워크 드라이버 사용 예시
    ```shell
    # 사용자 정의 네트워크 생성
    docker network create --driver=bridge my_br_network 

    # 사용자 정의 네트워크를 사용한 컨테이너 생성
     docker run -d --network=my_br_network nginx
    ```

2. 호스트 네트워크 드라이버

    호스트 네트워크 드라이버는 컨테이너의 가상 네트워크를 사용하는 것이 아니라 호스트 네트워크에 직접 연결하여 사용하는 것을 말한다.

    이를 통하여 포트 바인딩을 하지 않아도 되지만 네트워크 격리가 사라지게 된다. 

    ```
    docker run -d --network=host nginx
    ```

3. none 네트워크 드라이버

    none 네트워크는 컨테이너에 네트워크가 필요없거나 사용자 정의 네트워크를 사용할 때 사용하는데, 해당 드라이버를 사용하면 아무런 ip가 할당되어 있지 않다. 

    ```
    docker run -d --network none nginx
    ```

## 도커 볼륨

도커 볼륨은 컨테이너의 데이터 지속성을 보장하기 위해 사용된다. 

이는 컨테이너 레이어의 휘발성을 보완하고 컨테이너가 종료되거나 삭제되어도 데이터를 유지할 수 있다. 

또 이런 볼륨을 사용하면 컨테이너 간의 데이터 공유, 백업, 성능 향상을 할 수 있다.

컨테이너 파일 시스템 구조

1. 이미지 레이어

    이미지는 Dockerfile을 기반으로 빌드가 되는데, 이 Dockerfile에는 여러 명령어들이 작성되어 있다.

    이 명령어들이 순차적으로 레이어가 쌓이듯 저장이 되며 각 레이어는 이전 레이어의 변경 사함을 포함하고 있다. 

    이렇게 이미지를 레이어 아키텍처로 구성하면 수정이 용이하다는 장점이 있다. 

    왜냐하면 여러 레이어 중 하나의 레이어에 변화가 있다면 해당 레이어만 변경하면 끝이기때문이다.

    또 이렇게 생성된 이미지는 읽기 전용으로 변경이 되지 않는다. 

2. 컨테이너 레이어
    
    컨테이너 레이어는 이미지 레이어와 다르게 Read/Write 권한이 있기에 수정이나 변경이 가능하다. 

    그래서 컨테이너의 모든 변경 사항이 저장이 된다.

    하지만 컨테이너 레이어는 컨테이너가 종료되면 사라지기에 임시 저장소와 같다. 그래서 컨테이너 레이어와 그 안에 있는 모든 데이터도 사라지게 된다.

도커 볼륨 종류

1. 호스트 볼륨

    호스트 볼륨은 호스트의 디렉터리를 컨테이너의 특정 디렉터리를 마운트하여 사용하여 컨테이너의 데이터를 영구적으로 사용할 수 있도록 한다.

    ```shell
    # 호스트 볼륨 사용 예시
    docker run -d --name nginx \
    -v /opt/html:/usr/share/nginx/html
    -p 80:80
    nginx
    ```

2. 도커 볼륨

    도커 볼륨은 도커가 제공하는 볼륨 괸리 기능을 활용하여 컨테이너의 데이터를 영구적으로 사용하도록 한다.

    도커 볼륨을 사용하면 /var/lib/docker/volumes/$(volume-name)/_data에 컨테이너의 데이터가 저장이 된다.

    ```shell
    # volume 생성
    docker volume create --name my-volume

    # volume 확인
    docker volume ls

    # docker-volume 사용 컨테이너
    docker run -d --name my-mysql \ 
    -e MYSQL_DATABASE=test \
    -e MYSQL_ROOT_PASSWORD=test \
    -v my-volume:/var/lib/mysql \
    -p 3306:3306 \
    mysql:5.7
    ```

</details>

-----------------------

<br>

### 도커 설치 방법

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------
## CentOS
Vagrantfile 내용
```shell
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # vagrant provider 설정
  config.vagrant.plugins = "vagrant-libvirt"

  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # define Docker Server 
  config.vm.define "hj-server" do |cfg0|

    # 1. setting server spec
    cfg0.vm.provider :libvirt do |spec|
      spec.cpus = 2
      spec.memory = 4096
    end

    # 2. choose box and setting network
    cfg0.vm.box = "hj-docker"
    cfg0.vm.box_url = "/project/hj/docker/createBox/hj-docker-box.box"
    cfg0.vm.network "public_network", :dev => "br1", :type => "bridge"
    cfg0.vm.network "forwarded_port", guest: 22, host: 20010, id: "ssh"

    # 3. disable of firwalld and selinux 
    cfg0.vm.provision "shell", inline: "sudo systemctl disable firewalld --now"
    cfg0.vm.provision "shell", inline: "sudo sed -i 's/^SELINUX=enforcing.*$/SELINUX=disabled/' /etc/selinux/config"

    # 4. remove docker on OS
    cfg0.vm.provision "shell", inline: <<-SHELL
      sudo yum remove -y docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
    SHELL

    # 5. setup docker repository
    cfg0.vm.provision "shell", inline: "sudo yum install -y yum-utils"
    cfg0.vm.provision "shell", inline: " sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo"

    # 6. install docker package
    cfg0.vm.provision "shell", inline: "sudo yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin"

    # 7. enable docker
    cfg0.vm.provision "shell", inline: "sudo systemctl enable --now docker"

    # 8. server reboot
    cfg0.vm.provision "shell", inline: "sudo reboot"

  end
end
```

</details>

-----------------------

<br>

### 도커 이미지 빌드 하기

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

도커 이미지 빌드하는 방법을 알아보기 전 다시한번 도커 이미지에 대해서 확인하자.

도커 이미지는 레이어 아키텍처를 가지고 있어 새로운 변경사항이 하나씩 쌓이는 구조로 추가된 레이어는 이전 레이어의 내용을 가지고 있다. 

또 이미지는 읽기 전용으로 컨테이너를 생성하면 이미지 레이어의 내용은 변경이 불가능하다.

```shell
# 이미지 레이어 확인하기
docker images
docker images inspect nginx:latest # "RootFS"를 확인하면 레이어를 확인할 수 있다.
```

## Dockerfile

Dockerfile은 이미지 빌드를 위해 작성되는 파일이다. 

Dockerfile에 어떤 이미지를 만들것인지 지시어와 인자값으로 된 구성하여 Dockerfile을 만들고 이미지를 빌드한다.

## 이미지 빌드를 위한 핵심 개념
1. 빌드 컨텍스트
    
    빌드 컨텍스트란 도커 빌드 명령 수행 시 현대 디렉터리를 말한다. 

    "docker build" 명령을 수행할 떄, 해당 디렉터리의 모든 정보가 도커 데몬으로 전달된다. 

    이렇게 이미지 빌드에 필요한 정보를 도커 데몬으로 전달하기 위해 사용되는 개념이다. 

2. .dockerignore

    빌드 컨텍스트에는 이미지 빌드를 위한 모든 데이터들이 있다. 
    
    그런데 이 데이터들의 사이즈가 크다면 빌드 되는데 오래 걸리고 비효율적이다. 

    그래서 .dockerignore 파일로 디렉터리 또는 파일 목록을 빌드 컨텍스트에서 제외한다.

    gitignore파일과 같은 개념으로 보면 된다.

## Dockerfile을 통한 이미지 생성

```shell
# 어떤 베이스 이미지를 사용할지 결정하는 지시어와 값
FROM node:16 

# 이미지의 메타데이터를 결정하는 지시어와 값
LABEL maintainer="Peter Kim <khjlove8427@naver.com>"
LABEL description="Simple server with Node.js"

# workdirectory 결정, cd를 통하여 디렉토리 이동을 한다라고 생각하면 된다.
WORKDIR /app

# COPY 지시어는 SRC(host os)와 DEST(이미지 상의 경로)를 가진다.
COPY pacakage*.json ./ # 현재 디렉토리의 pacakage*.json 모든 파일을 현재 디렉토리(/app)에 복사

# RUN 지시어는 해당 명령어를 실향하도록 하는 지시어
RUN npm install # /app디렉토리에서 pacakage*.json을 읽어 패지키들을 설치한다.

COPY . . # 현재 디렉토리를 /app 디렉토리에 모두 복사하라, 위에서 COPY를 한 것은 패키지는 다른 레이어로 관리하기 위해 설정 한 것

# EXPOSE 지시어는 포트를 사용하겠다고 알려준다. -p 옵션을 통해서 실제 포트를 맵핑한다.
EXPOSE 8080

# CMD 지시어는 해당 이미지를 가지고 어떤 명령어를 수행할 것인지 결정하는데, 즉 주요 프로세스를 결정
CMD ["node", "server.js"]


# 이미지 빌드 및 컨테이너 생성
docker build --force-rm -t nodejs-server . # 이미지 빌드, --force-rm: 이전에 생성된 임시 컨테이너 및 이미지를 삭제하고 빌드를 다시 시작, -t : 이미지에 태그를 지정
docker images # 확인
docker run -d -p 8080:8080 nodejs-server
curl localhost:8080

```

-----------------------



</details>

-----------------------

<br>



### 도커 개인 레포지토리 구성하기

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------

</details>

-----------------------

<br>

### 도커 활용 - 01

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------

    

</details>

-----------------------

<br>

### 도커 활용 - 02

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------



</details>