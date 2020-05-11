---
title:  "리눅스 ip, network, domain name 관련 utility 정리"
excerpt: "리눅스 환경에서 ip, network, domain에 관한 유틸리티를 다뤄 보자.."

categories:
  - 리눅스
tags:
  - 리눅스
---

# Network

## ifconfig
현재 설치된 네트워크 인터페이스 설정을 확인한다. 주로 IP주소를 확인한다. 

![image](https://user-images.githubusercontent.com/48200520/81061266-fde24500-8f0e-11ea-89aa-0f2450de6564.png)

## ip 
라우팅, 장치 그리고 터널링과 같이 네트워크에 관련된 부분들을 수정하고 조회할때 사용한다. 

![image](https://user-images.githubusercontent.com/48200520/81067598-dcd32180-8f19-11ea-8b31-9bf05d3f8d08.png)
### ip address
ip 정보를 출력합니다

![image](https://user-images.githubusercontent.com/48200520/81067953-7e5a7300-8f1a-11ea-8dd4-85b73896f424.png)

## netstat
네트워크 연결상태, 라이팅테이블, 인터페이스 상태등을 보여주는 명령어

### netstat -a
모든 네트워크 연결상태를 보여준다.

![image](https://user-images.githubusercontent.com/48200520/81068201-f0cb5300-8f1a-11ea-977f-ae07bdb60cea.png)

### netstat -at
TCP만 확인하기

![image](https://user-images.githubusercontent.com/48200520/81068286-13f60280-8f1b-11ea-95fe-9e9553e0606d.png)

### netstat -au
UDP만 확인하기

![image](https://user-images.githubusercontent.com/48200520/81068380-3c7dfc80-8f1b-11ea-99fe-5cbc1f9a95bc.png)

### netstat -nap | grep LISTEN
LISTEN 상태인 포트만 출력하기

![image](https://user-images.githubusercontent.com/48200520/81068489-69321400-8f1b-11ea-80be-b2f77952a3b1.png)

## host
도메인 명은 알고 있는데 ip주소를 모르거나 혹은 그 반대의 경우에 사용하는 명령어이다. 호스트명을 이용하여 ip주소 뿐만 아니라 하위 호스트명도 조회할 수 있다. 

![image](https://user-images.githubusercontent.com/48200520/81072275-e1e79f00-8f20-11ea-8faf-628aa70ff006.png)

## hostname
호스트의 이름을 출력한다. 

![image](https://user-images.githubusercontent.com/48200520/81072373-05aae500-8f21-11ea-8bc0-479d7eb1d3dc.png)

## traceroute [도메인명 혹은 ip주소]
명령어를 실행하는 컴퓨터에서 목적지 서버로 가는 네트위크 경로를 확인해주는 명령어입니다. 

![image](https://user-images.githubusercontent.com/48200520/81076062-23c71400-8f26-11ea-8c89-ced85290358b.png)

# Domain name
## nslookup
name server 관련한 조회를 할 수 있는 명령어이다. 서버의 네트워크가 제대로 설정되었는지 확인하는 용도로 자주 쓰인다.

![image](https://user-images.githubusercontent.com/48200520/81084804-59bdc580-8f31-11ea-9366-b397d3d462d5.png)

## ping
외부 호스트 서버가 네트위크상으로 접근이 가능한지 확인해보는 명령어이다. 

![image](https://user-images.githubusercontent.com/48200520/81085385-1dd73000-8f32-11ea-8d96-08c23c16cd6d.png)
