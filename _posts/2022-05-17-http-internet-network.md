---
layout: post
title: http 공부 정리 - 1. 인터넷 네트워크
subtitle: 
categories: http
tags: [http, study]
---

### Ip protocol

 ip 지정, 패킷 단위로 데이터 전달
 - 비연결성 : 패킷을 받을 대상이 없거나 꺼져있어도(불능) 패킷 전송
 - 비신뢰성 : 패킷이 사라지거나 순서대로 도착하지 않는 경우
 - 프로그램 구분 : 같은 IP 사용하는 서버에서 애플리케이션이 둘 이상
   -> 이를 해결하기 위해 TCP/UDP


### 인터넷 프로토콜 스택의 4계층

 전송할 때 위에서부터 아래로, 각각 추가 정보를 감싸는 느낌
 - 애플리케이션 계층 : HTTP, FTP		-> 메시지 등
 - 전송 계층 : TCP, UDP			-> TCP정보(출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보...)
 - 인터넷 계층 : IP				-> IP정보(출발지 IP, 목적지 IP, 기타...)
 - 네트워크 인터페이스 계층			-> Ethernet frame~


### TCP 특징
전송 제어 프로토콜(Transmission Control Protocol)
 - 연결지향 - TCP 3 way handshake(가상 연결) : 연결이 되었는지 확인 후 메시지 전송
    -> 가상연결 : 논리적 연결. 도중의 여러 노드들은 관계 모르고, SYN, ACK 교환한 클라이언트와 서버가 연결 됐음을 인식하는 정도
  - 데이터 전달 보증 : 메시지 보냈을 때 패킷 누락됐으면 알 수 있음
  - 순서 보장


### UDP 특징
User Datagram Protocol (TCP와 같은 계층)
 - 기능이 없음(하얀 도화지!) : TCP 3way handshake X, 전달보증X, 순서 보장X
   -> 데이터 전달 및 순서가 보장되지 않지만 단순하고 빠름
 - IP와 거의 같지만 PORT 개념 추가(+체크섬정도)
 - 지금까지 TCP가 90% 이상의 점유율을 보이고 있지만 최근들어와 UDP각광받기 시작(http3 등)


 ### PORT
 - 같은 IP사이에 여러 애플리케이션(게임, 화상통화 등)이 걸려 있을 경우 구분을 위해 PORT 설정
 - 클라이언트, 서버가 같은 PORT를 쓸 필요는 없으며 TCP정보에 포함된 출발지 PORT, 목적지 PORT 정보로 서로 알 수 있음
 - IP가 아파트, PORT가 xx동xxx호로 생각하면 편함!
   - 0~65535 	할당 가능
   - 0~1023		잘 알려진 포트, 사용하지 않는 쪽이 좋음
	 - FTP : 20, 21
	 - TELNET : 23
	 - HTTP : 80
	 - HTTPS : 443


 ### DNS
 Domain Name System : IP는 기억하기도 어렵고, 변경될 수 있기 때문에 도메인 네임이 필요
  - 전화번호부와 같은 역할, 도메인 명을 등록 후 그것을 IP주소로 변환
  - 클라이언트가 서버와 통신하기 전에 DNS 서버와 먼저 통신, 도메인에 할당된 IP를 받아 서버로 연결

-----------
# 참고
[인프런 강의 모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/)