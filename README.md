# ft_netwhat

<br/>

- 네트워크에 대한 전반적인 이해 후 42 사이트에서 문제를 푸는 

<br/>

# IP address

- 컴퓨터 네트워크에서 장치들이 서로를 인식하고 통신을 하기 위해서 사용하는 특수한 번호

  => 인터넷 연결을 하기 위한 주소
  
- network-id + host-id로 구성

- 라우터에게 패킷이 이동해야 하는 장치를 알려주는 "네트워크" + 라우터에게 무엇을 알려주는 "호스트"

  ### +

   ##### < 주소 >

  - network-id: domain(동일 속성들의 집합) 식별자 
    - ex) 팽
  - host-id : 동일 네트워크 안에서의 식별자 
    - ex) 건우
  - subnet-id : network 구분자
    - ex) 절강팽, 용강팽
  - routing : 서로 다른 network-id를 가진 시스템의 통신
  - switching : 동일 network-id를 가진 시스템의 통신
  - protocol :  컴퓨터나 원거리 통신 사이에서 메세지를 주고 받는 양식 / 규칙 체계
  - 패킷 : L4에서 전달받은 segment + L3의 정보 = 패킷
  - localhost : 127.0.0.1(예약된 IP주소로 인터넷상에 일반 IP로는 쓸 수 X)
  - CIDR (Class Inter-Domain Routing) : 클래스 없는 도메인 간 라우팅 기법



## 종류

1. IPv4
   - 32 bit 구성으로 일반적인 ip 주소
   - 0.0.0.0 ~ 255.255.255.255 까지 숫자 조합으로 이루어짐 (중간 사설 주소는 사용 X)

2. IPv6

   - 128 bit 구성으로 IPv4의 고갈, 보완 하기 위해 만들어진 주소

   

     ## Classful

   - network-id가 고정되어 있다.

   - 정해진 규칙에 따라서 network-id가 정해진다.

   - 맨 앞자리 주소(네트워크 주소)와 맨 뒷자리 주소(브로드캐스트 주소) 이므로 사용 불가

     - ex) A class에서 0.0.0.0(네트워크 주소), 127.255.255.255(브로드캐스트 주소) 사용불가

     

     #### << 형태 >>

     X.X.X.X [X 10진수] 

     xxxx xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx [x 2진수]

     를 가지며 A, B, C, D, E class가 존재 합니다.
     
     
     
    ![한국인터넷정보센터](https://user-images.githubusercontent.com/53526987/103192034-91dba380-491a-11eb-961f-526c06859561.jpeg)

     
     
     ##### 1.  A class (0 ~ 127)
     
     - 0xxx xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx (앞에 나와 있는 0 이 고정)
     - 0000 0000.0000 0000.0000 0000.0000 0000 ~ 0111 1111.1111 1111.1111 1111.1111 1111
     - 0.0.0.0 ~ 127.255.255.255
     - 구분 : 첫 X - network-id (2^(8 - 1)) + 나머지 X.X.X - host-id (2^24)
   	- ex) 11.1.1.1 -> 11 / 1.1.1

   	
   	
   	##### 2. B class (128 ~ 191)
   	
   	- 10xx xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx (앞에 나와 있는 10 이 고정)
   	- 1000 0000.0000 0000.0000 0000.0000 0000 ~ 1011 1111.1111 1111.1111 1111.1111 1111
   	- 128.0.0.0 ~ 191.255.255.255
   	- 구분 :  X.X - network-id (2^(16 - 2)) + 나머지 X.X - host-id (2^16)
   	- ex) 150.1.1.1 -> 150.1 / 1.1
   	
   	
   	
   	##### 3. C class (192 ~ 223)
   	
   	- 110x xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx (앞에 나와 있는 110 이 고정)
     - 1100 0000.0000 0000.0000 0000.0000 0000 ~ 1101 1111.1111 1111.1111 1111.1111 1111
     - 192.0.0.0 ~ 223.255.255.255
     - 구분 : X.X.X - network-id (2^(24 - 3)) + 나머지 X - host-id (2^8)
   	- ex) 195.1.1.1 -> 195.1.1 / 1

   	
   	
   	##### 4. D class (multicast 용)
   	
     - 네트워크 개념 X
     
     - 1110 xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx (앞에 나와 있는 0이 고정)
   	- 1110 0000.0000 0000.0000 0000.0000 0000 ~ 1110 1111.1111 1111.1111 1111.1111 1111
   	- 224.0.0.0 ~ 239.255.255.255
   	
   	
   	
   	##### 5. E class (연구용, 예약된 주소)
   	
   	- 1111 xxxx.xxxx xxxx.xxxx xxxx.xxxx xxxx (앞에 나와 있는 0이 고정)
   	
   	- 1111 0000.0000 0000.0000 0000.0000 0000 ~ 1111 1111.1111 1111.1111 1111.1111 1111
   	
   	- 240.0.0.0 ~ 255.255.255.255
   	
   	

    ## Classless

     - network-id가 유동적이다.
     - 정해진 규칙이 없다.

   

     ### << NetMask & SubnetMask>> 

     - network-id + mask

     - 변하지 않는 부분(network-id)을 2진수 1로 표기

     - 현재는 구분이 사라졌다. 그러나 나누자면 netmask를 작게 자른 것이 subnetmask라고 한다.

       #### +

       SubnetMask 

       - 255(네트워크 부분)와 0(호스트 부분)으로 이루어져 있다.

       - 255로 된부분 무시하고 0으로 된 부분에서 IP를 쪼개는 것이다. 

         => IP주소가 모자라기 때문

       - 브로드캐스트 영역(네트워크)를 나누기 위함

       

     ### Private address (인터넷이 안되는 주소 = 사설 망)

     - RFC 1918 표준

     - 주소 뒤에 /숫자는 netmask의 bit수(왼쪽 부터 표시된 1의 개수)를 의미합니다.

       - ex) 192.255.0.4/24 

         -> IP address : 192.255.0.4

         -> netmask : 255.255.255.0

     

  1. ### 10.0.0.0 ~ 10.255.255.255
   
     
        - 0000 1010.		0000 0000.0000 0000.0000 0000 ~ 0000 1010.		1111 1111.1111 1111.1111 1111
        - 10.0.0.0/8
        
        


  2. ### 172.16.0.0 ~ 172.31.255.255
   
     
        - 1010 1100.0001		0000.0000 0000.0000 0000 ~ 1010 1100.0001		1111.1111 1111.1111 1111
        - 172.16.0.0/12
        
        


   3. ### 192.168.0,0 ~ 192.168.255.255

      - 1100 0000.10101000		.0000 0000.0000 0000 ~ 1100 0000.1010 1000		.1111 1111.1111 1111
      - 192.168.0.0/16



---



# Broadcast Address & Network Address

## Broadcast Address

- 네트워크 주소 다중 접속에 접속 된 모든 장치들에 전송하는데 사용되는 통신 네트워크
- 네트워크에 연결된 모든 호스트에서 수신 하는 address 
- subnet-mask의 '0'부분을 1로 바꾼 것

#### Calculator

- IP Address	XAND	Netmask = Broadcast 



## Network Address

- 하나의 네트워크를 부르는 것 (첫번째 IP 주소)



#### Calculator

- IP Address   AND   subnet-mask = Network Address





---



# Subnetting & Supernetting

### Subnetting

- IP주소 낭비를 방지하기 위해 네트워크를 분리하는 과정

- network-id 늘리고 host-id를 줄인다.
- 네트워크 규모를 작게한다.
- 보안을 위함



### Supernetting

- 네트워크를 합쳐 네트워크를 확장하는 과정
- network-id 줄이고 host-id를 늘린다.
- 네트워크 규모가 커진다.
- 연산 부하를 줄이기 위함



---



# OSI 7 Layer

- 네트워크에서 통신이 일어나는 과정을 7 Layer로 나눈 것

- 장비호환성

- 개발용이




|layer|HOSTA|Request|HOSTB|
|:----:|:----:|:----:|:----:|
|7|Application|<< DATA >>|Application|
|6|Presentation|<< DATA >>|Presentation|
|5|Session|<< DATA >>|Session|
|4|Transport|<< Segments >>|Transport|
|3|Network|<< Packets >>|Network|
|2|DataLink|<< Frame >>|DataLink|
|1|Physical|<< Bits >>|Physical|




- 5 ~ 7 층은 상위계층(생성계층): 사람 쪽
- 1 ~ 4층은 하위계층(전송 계층): 기계 쪽 



## L7

- 사용자에게 편리한 인터페이스 제공
- GUI를 정해지는 protocol에 따라 만들어짐



## L6

- 포멧, 압축, 암호화



## L5

- 통신의 내용, 대화의 내용 -> stateless(전달만 되면 된다.) -> 통신 연결성 문제 -> SNL, cookie-id(연결정보-id)



## L4

- 통신을 활성화하는 계층으로 port를 열어 응용프로그램들이 전송할 수 있게 하는 계층

### < Port >

- 통신하는 문

- 0 ~ 255: 공공의 목적 (http: 80, ftp: 20~21)

-  ~ 1023: 상용의 목적

-  ~ 49151 : 등록 포트 -> 충돌 방지를 위해 미리 등록하고 사용

-  ~ 65545:  동적 포트 -> 동적 포트, 임의 포트

  

  #### TCP(Transmission Control Protocol)

- 연결지향 protocol : 통신하기 전에 사전에 미리 통신 채널을 만든다.
  
  - 신뢰성 있는 protocol(확인 후 실행) 
  
- UDP 보다 속도가 느리다.
  
  
  
#### UDP(User Datagram Protocol)

  - 비연결지향 protocol : best effort 최선을 다해 전송
  - 비신뢰성 protocol(확인 안하고 실행) 그러나 상위 계층에서 신뢰성 확보
  - TCP 보다 속도가 빠르다. (여러 지점에 전송 가능)



## L3

- 데이터를 목적지까지 가장 안전하고 빠르게 전달하는 기능(라우팅 - 주소를 찾아가는 과정)
- 경로와 주소를 정하여 패킷을 전달해주는 계층
- 라우팅 테이블 : 목적지를 찾아가기 위한 지도
- Gateway : 데이터가 목적지를 향하기 위해 이동해야하는 연결된 장비의 주소(라우팅하는 자식)
  - default Gateway
    - netmask가 0.0.0.0 (특정 목적지가 아닌 모든 곳)



## L2

- physical 계층을 통해 송수신되는 정보의 오류와 흐름을 관리하여 안전한 정보를 수행하도록 도와주는 계층
- mac address(컴퓨터의 고유주소)를 가지고 통신



## L1

- 기기를 이용해서 통신 케이블로 데이터를 전송





---



# DHCP

- 네트워크에서 동적으로 IP 주소를 할당해주는 protocol (IP 주소는 영구적 X)
- IP가 DCHP서버에서 지정해놓은 사용시간만큼 임대해 온다.



### 구성

- #### DHCP 서버
  - 인터넷을 제공해주는 곳의 서버에서 실행되는 것으로 IP주소를 다른 client에게 할당하여 자동으로 설정해주는 역할
  
  
  
- #### DHCP 클라이언트

  - 시스템이 시작할 때 DHCP 서버에게 IP주소를 요청하고 TCP/IP 설정은 초기화 되어 다른 HOST와 TCP/IP를 사용해서 통신할 수 있다.

    => DHCP 서버에게 IP주소를 할당 받으면 다른 HOST와 TCP/IP 통신을 할 수 있다.

     ##### +

  TCP/IP protocol : 인터넷을 하기 위한 protocol 집합 




### 동작

![DHCP1](https://user-images.githubusercontent.com/53526987/103192073-b6d01680-491a-11eb-8cac-c09f48f85cf0.PNG)



- #### DHCP Discover

  - HOST -> DHCP 서버
  - HOST가 DHCP 서버를 찾기위한 통신

  

- #### DHCP Offer

  - DHCP 서버 -> HOST
  - DHCP 서버가 HOST에게 자신의 존재를 알리고 HOST에 할당할 IP주소 정보 + 네트워크 정보들을 같이 HOST에게 전달.

  

- #### DHCP Request

  - HOST -> DHCP 서버
  - HOST가 DHCP 서버의 존재알며 DHCP 서버가 HOST에 제공할 네트워크 정보(IP address, subnet-mask 등)을 알았다. => HOST는 DHCP Request 메세지를 통해 DHCP 서버 한개를 선택하고 해당 DHCP 서버에게 HOST가 사용할 네트워크 정보를 요청

  

- #### DHCP Ack

  - DHCP서버 -> HOST
  - DHCP서버가 HOST에게 네트워크 정보를 전달해 주는 마지막 메세지 이다.



---



# DNS

- Domain Name System
- 도메인 이름을 기기가 읽을 수 있는 IP주소로 변환
- ex) www.amazon.com -> 192.0.2.44



### 웹 Application 라우팅 방법



![DNS](https://user-images.githubusercontent.com/53526987/103193073-88543a80-491e-11eb-8aa7-7ee290ba4347.png)

- 사용자가 웹 브라우저에 domain 이름을 입력
- 브라우저가 DNS에 접속하여 dmain 이름과 관련된 IP 주소를 서버에 요청
- domain이름의 웹 페이지를 웹 브라우저로 반환하고 페이지를 표시
