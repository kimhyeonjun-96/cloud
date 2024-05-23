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

컨테이너 기술을 활용하여 가장 활발하게 쓰이는 것이 바로 도커이다. 


## 도커의 구성 요소
1. Docker CLI

    Docker CLI란 도커 명령어가 설치된 서버를 말한다.

2. Docker Host

    도커 호스트의 경우에는 도커 엔진이 설치된 서버를 말한다.

    이 호스트는 컨테이너와 이미지를 관리한다. 

3. Image

    이미지는 컨테이너를 생성할 때 필요한 요소이다.

    컨테이너의 목적에 맞는 바이너리와 의존성이 설치되어 있다. 

    또한 여러 개의 계층으로 된 바이너리 파일로 존재한다. 

    즉, 새로운 변경 사항이 하나씩 쌓이는 구조이다. 


4. Container

    컨테이너는 호스트와 다른 컨테이너로부터 격리된 시스템 자원과 네트워크를 사용하는 프로세스이다. 

    이미지는 읽기 전용으로 사용되고 컨테이너의 여러 변경 사항은 컨테이너 계층에 저장이 된다. 

5. Registry

    이미지들이 저장되어 있는 장소이다. 

## 도커 라이프사이클 관련 명령어
1. 컨테이너 시작

    ```shell
        docker run -it [--rm] -d --name [container] -p [port] -v [mount point]
    ```

2. 컨테이너 상태 확인

    ```shell
        docker ps 
        docker ps -a
        docker inspect [container]
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



## 도커 볼륨

</details>

-----------------------

<br>

### 도커 설치 방법

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

-----------------------



</details>

-----------------------

<br>

### 도커 이미지 빌드 하기

<details>
    <summary>🤔 내용 보기 </summary>
<br/>

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