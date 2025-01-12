# 📝공인IP, 사설IP, 포트포워딩, 외부,내부 포트
## **공인 IP, 사설 IP**

### **공인(Public) IP** 
> 인터넷 사용자의 로컬 네트워크를 식별하기 위해 ISP(인터넷 서비스 공급자)가 제공하는 IP 주소이다. 공용 IP 주소라고도 불리며 외부에 공개되어 있는 IP 주소이다.

* 공인 IP는 전세계에서 유일한 IP 주소를 갖는다.
* 공인 IP 주소가 외부에 공개되어 있기에 인터넷에 연결된 다른 PC로부터의 접근이 가능하다. 
  * 공인의 경우 방화벽같은 보안프로그램을 설치할 필요가 있다.
<br>

### **사설(Private) IP** 
> 일반 가정이나 회사 내 등에 할당된 네트워크의 IP 주소이며, 로컬 IP, 가상 IP라고도 한다.<br>
> IPv4의 주소부족으로 인해 서브넷팅된 IP이기 때문에 라우터에 의해 로컬 네트워크상의 PC 나 장치에 할당된다.
<br>
<br>

### **공인IP에서 사설IP로의 변환은 어떻게 이루어지는가?**
* NAT(Network Address Translation)는 공인IP에서 사설IP로 변환해주는 역할을 한다.(OSI 3계층에 해당)
* NAT의 특징으로 IP를 숨길 수 있는 기능이 있어 보안성을 높여준다
  * 우리의 컴퓨터에서 팻킷을 외부로 전송할때 사설IP가 공인IP로의 변환이 이루어지면서 사설IP에 대한 정보를 외부에서는 알 수 없기 때문에 우리 컴퓨터의 내부로의 접근을 보호할 수 있다.
* 우리가 흔히 사용하는 공유기(라우터)의 경우 NAT의 종류중 하나인 NAPT를 사용한다.
    * NAPT(Network Address Port Translation)로 NAT처럼 IP주소를 변환해 주는 동시에 port번호로 변환해 준다.
    * 인터넷에 송출할때 자신의 IP 주소와 포트번호의 조합을 공유기(라우터)를 통해 공인IP주소 + 외부포트번호 조합으로 변환시킨다.


* NAT 동작원리  
 https://www.stevenjlee.net/2020/07/11/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-nat-network-address-translation-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%A3%BC%EC%86%8C-%EB%B3%80%ED%99%98/


### **NAPT 구조**
![NAT구조](https://user-images.githubusercontent.com/43923432/129305601-80d1e8ba-8124-4f2b-a2b0-751511249a65.png)



### **차이점** 
|      | 공인 IP | 사설 IP             |
| ---- | ------- | ----------------- | 
| 할당 주체 | ISP(인터넷 서비스 공급자) | 공유기(라우터) |
| 할당 대상 | 개인 또는 회사의 서버(라우터) | 개인 또는 회사의 기기 |
| 고유성 | 인터넷 상에서 유일한 주소 | 하나의 네트워크 안에서 유일 |
| 공개 여부 | 내/외부 접근 가능 | 외부 접근 불가능 |
> ❗ 사설 IP 주소만으로는 인터넷에 직접 연결할 수 없다.<br>
>  라우터를 통해 1개의 공인(Public) IP만 할당하고, 라우터에 연결된 개인 PC는 사설(Private) IP를 각각 할당 받아 인터넷에 접속할 수 있게 된다.

![image](https://user-images.githubusercontent.com/43923432/128640300-a8851f59-cde3-4a7f-81a9-cb5e03eb74b2.png)

> 💻➡🌏 : 사설 IP를 할당받은 스마트폰 혹은 개인 PC가 데이터 패킷을 인터넷으로 전송하면, 라우터(공유기)가 해당 사설 IP를 공인 IP로 바꿔서 전송한다.

> 🌏➡💻 : 인터넷에서 오는 데이터 패킷의 목적지도 해당하는 사설 IP로 변경한 후 개인 스마트폰 혹은 PC에 전송한다.

* * *

## **포트 포워딩, 내부포트, 외부포트**

## **포트 포워딩** 
>포트 포워딩이란 컴퓨터 네트워크에서 패킷이 라우터나 방화벽 같은 네트워크 게이트웨이를 통과하는 동안 네트워크 주소를 변환해주는 것을 의미합니다.<br>
**즉, 외부에서 내가 원하는 내부 기기에 접속을 할 수 있도록 연결해주는 것을 의미한다.**

## 외부 포트 
* 외부에서 어떤 포트로 접속을 하였을 때 지정된 컴퓨터로 연결을 할 것인가 입니다.

## 내부 포트
* 지정된 컴퓨터로 외부포트에서 연결을 해주었을 때, 지정된 내부 PC에서는 어떤 포트를 사용할 지 정해준다.

* 포트번호 : 컴퓨터안에서 작동하는 Application을 식별하기 위해 사용하는 숫자를 의미.(
0~65535)

* * *

![image](https://user-images.githubusercontent.com/43923432/128737164-1d4fdd05-45b9-40a5-abe3-a78d0de4ef9f.png)
> "공인 IP:외부포트"로 접속이 이루어지면 "사설IP:내부포트"로 연결이 되도록 해준다.

* 연결을 해주기 위해서 IPTIME을 예시로 들자면 

![image](https://blog.kakaocdn.net/dn/bQKrXK/btqH5Z5vf8A/KK3GfKkWudhB16PhFLmXMk/img.png)
> 규칙이름은 마음대로 정하면 되고 어떤 프로토콜을 사용할 것인지, 연결할 외부포트와 내부포트를 결정해주고 적용을 누르면 포트 포워딩이 끝난다.
* 범위 지정시 
  * 포트 한개만 지정 : 외부포트(1111~1111) , 내부포트(22~22)
    * 외부포트 1111로 접속하면 내부포트 22번으로 연결된다.
  * 포트 범위 지정 : 외부포트(1000~1111), 내부포트(20~30) 
    * 외부포트 1000~1111로 접속시 내부포트 범위에 해당하는 번호와 연결된다.


> 심화... -> 셀룰러가 아닌 내부 ip주소에서 다른 내부 ip주소로 포트포워딩 

<br>

* * *

<br>

## **nginx를 이용한 포트 포워딩 실습!!** 

### **📌포트 포워딩 설정**
1. **Kthub에 접속**하여 "포트 포워딩"할 **외부 포트, 내부 포트, 내부 IP주소**를 설정해 준다.
<img width="774" alt="스크린샷 2021-08-11 오전 2 18 42" src="https://user-images.githubusercontent.com/43923432/128905301-4cd53557-d412-4d69-ad1f-c33f21941165.png">

2. nginx 의 vi로 접속하여 default로 설정된 내부 포트번호를 바꿔준다. 
<img width="387" alt="스크린샷 2021-08-11 오전 2 12 57" src="https://user-images.githubusercontent.com/43923432/128904539-8ea25518-acc4-435a-8481-5ceac0b05cba.png">
    > **vi  /usr/local/etc/nginx.nginx.conf** <br>
      을 통해 vi편집으로 들어가서 Server-listen의 port번호를 위에서 설정한 **내부 포트 번호** 로 바꿔준다.

    <img width="355" alt="스크린샷 2021-08-11 오전 2 13 37" src="https://user-images.githubusercontent.com/43923432/128904615-329568ec-5397-40f1-8b5c-1d60a630d1a3.png">

    > 응용프로그램을 실행할때는 location에 실행하고자 하는 파일위치를 적어준다. 

    <img width="580" alt="스크린샷 2021-08-11 오전 1 49 45" src="https://user-images.githubusercontent.com/43923432/128902752-71b7a286-323f-4309-a84a-d191cdacfb33.png">

    > **nginx에 5156 포트**로 연결된걸 알 수 있다.
<br>

### **📌스마트폰으로 실행**
* ### 처음 시도는... 실패😨 

<img width="250" alt="포트포워딩실패" src="https://user-images.githubusercontent.com/43923432/128903622-417b44f9-abd7-4806-a2b4-a14f0fb33f6b.jpeg">

> 접속이 되지 않아 원인을 찾아보니 KT공유기의 경우 MAC주소별로 고정 IP할당이 불가능하여 와이파이를 재접속하게되면 내부IP주소가 바뀌어서 포트 포워딩을 다시 설정해 주어야 하는 문제가 발생하였다.

* ### 🎉두번째 시도 성공!!! 
<img width="280" alt="포트포워딩성공" src="https://user-images.githubusercontent.com/43923432/128903676-952f43e1-8e92-4264-a24e-d4be09e036d9.jpeg">

> 임시방편으로 와이파이를 유지한채 포트포워딩을 다시 설정해 주고 나서야 성공할 수 있었다.


## **정리**
> 간단하게 포트 포워딩에 대한 실습을 해봤는데 다음에는 실제 응용프로그램으로 돌려서 실행해보고 위에서 문제가 발생한 IP고정 할당에 대해서도 다른 방법이 있는지 찾아봐야겠다. 





