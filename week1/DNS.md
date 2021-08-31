[작성 링크](https://delirious-sock-4dc.notion.site/f9fb81c1201e4a988ff3ad3a4fa21303)

# 도메인 네임 시스템

생성 일시: 2021년 8월 9일
태그: CS, Network

# 개요

---

### IP

우리는 택배를 보낼때 수신자의 주소를 알아야 택배를 보낼 수 있다. 

마찬가지로 인터넷상에서 특정 웹사이트에 접속하려면 그 웹사이트의 주소가 필요한데, 이를 **IP**라고 한다.

우리가 흔히 알고 있는 네이버의 IP는 125.209.222.141이다.

### 도메인 네임

IP는 숫자로 구성되어 있기 때문에 사람이 이해하고 기억하기 어렵다.

그래서 IP에 이름을 부여했는데, 이를 **도메인 네임** 이라고 한다.

위에서 보았던 네이버의 IP 125.209.222.141은 도메인 네임 www.naver.com과 같은 의미를 지닌다.

### 도메인 네임 시스템

IP를 도메인 네임으로 바꾸거나 그 반대의 변환을 수행해주는 시스템이다.

우리가 브라우저상에서 www.naver.com을 입력하면 도메인 네임 시스템에 의해 25.209.222.141로 변환되어 네이버 웹사이트로 이동할 수 있게 된다.

### 도메인 네임 시스템의 성장

과거 스탠퍼드 연구소에서는 hosts.txt라는 파일 하나에 IP와 도메인 네임 정보를 저장해놓고 사용했다.

하지만 호스트가 계속 증가함에 따라 성능문제 및 관리의 어려움이 발생했고 이러한 단점을 보완하기 위해 새로운 형태의 시스템을 설계하게 되었다.

RFC에 도메인 네임 생성 규칙을 정리해 표준화 하고 분산 데이터베이스 시스템을 적욯하여 오늘날의 DNS가 만들어졌다.

**RFC (Request for Comments)**
비평을 기다리는 문서라는 의미로, 컴퓨터 네트워크 공학 등에서 인터넷 기술에 적용 가능한 새로운 연구, 혁신, 기법 등을 아우르는 메모를 나타낸다.

**분산데이터베이스 시스템**
물리적으로 분산된 위치에 있는 여러대의 데이터베이스를 논리적으로 하나의 데이터베이스 처럼 사용하는 시스템이다.

# 도메인 네임 시스템의 구성

---

도메인 네임 시스템 (이하 DNS)은 도메인 네임 공간, 도메인 네임 서버, 리졸버  3가지로 구성된다.

## 도메인 네임 공간
Domain Name Space

도메인 이름 공간은 **도메인 이름을 트리 형태로 구성**한 것이다.

트리는 루트 존에서 시작하여 여러 개의 하위 존으로 나뉜다. 

각 DNS 존은 하나의 권한 있는 DNS 서버에 의해 관리되는 노드들의 집합이다.

![dns-zone](https://user-images.githubusercontent.com/49011919/129351984-3adfa972-5595-4228-a597-2d494f3d0104.jpg)

- 하나의 존에는 여러개의 하위 도메인을 포함할 수 있고 동시에 여러 존이 동일한 서버에 존재 할 수 있다.

## 도메인 네임 서버
Domain Name Server

도메인 네임 공간의 트리 구조에 대한 정보 가지고 있어서 클라이언트의 질의 요청을 응답해주는 역할을 한다.

도메인 네임 서버는 유형에 따라 두가지로 나눌 수 있다.

### 권한 있는 DNS 서버

- 도메인에 대해 최종 권한이 있는 DNS 서버로서 도메인 이름을 IP 주소로 변환한다.
- 클라이언트는 재귀적 DNS 서버를 경유하여 권한 있는 DNS서버에 쿼리를 수행해 IP주소를 얻는다.

### 재귀적 DNS 서버

- DNS 레코드를 소유하고 있지 않지만 사용자를 대신해서 DNS 정보를 가져올 수 있는 중간자의 역할을 한다.
- 일정기간 동안 IP 정보를 캐시 할 수 있다.

## 리졸버
Resolver

웹 브라우저와 같은 DNS 클라이언트의 요청을 네임 서버로 전달하고, 네임 서버로부터 도메인 이름과 IP 주소를 받아 클라이언트에게 제공하는 기능을 수행한다.

# 도메인 네임 시스템의 동작 과정

---

www.naver.com의 IP를 찾아내는 여행

브라우저가 유저로 부터 도메인을 입력받으면..

1. C:\Users\UserName\AppData\Local\Microsoft\Windows 경로의 `cache` 폴더를 확인한다.
2. 1. 에 결과가 없으면 C:\Windows\System32\drivers\etc 경로의 `hosts` 파일을 확인한다.
3. 2.에서 결과가 없으면, `로컬 DNS 서버` 에 요청한다. 

이후에는 두가지 방법으로 나뉜다.

## 재귀적 질의 방법

그림과 같이 로컬 DNS 서버부터 시작해서 IP를 찾을때까지 재귀적으로 DNS 서버를 순회하는 방식이다.

재귀적 질의는 상위 레벨의 네임 서버에 과부하를 줄 수 있다는 단점이 있다.

![재귀.PNG](https://user-images.githubusercontent.com/49011919/129350830-4dd10634-ad1e-4c36-b8b9-16f4bc91a532.png)

## 반복적 질의 방법

그림과 같이 로컬 DNS 서버가 IP주소를 찾을때까지 상위 레벨의 네임 서버부터 하위 레벨의 네임 서버 순으로 반복적으로 질의를 하는 방법이다.

질의를 요청한 DNS서버에 찾고자 하는 IP주소가 없으면 응답으로 하위 레벨의 네임 서버의 정보를 넘겨준다.

![반복.PNG](https://user-images.githubusercontent.com/49011919/129350837-69bfffb4-573c-4520-9edc-ab12c250c046.png)

## 출처

---

[https://ict-story.tistory.com/59](https://ict-story.tistory.com/59)

[https://ko.wikipedia.org/wiki/도메인_네임_시스템](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)