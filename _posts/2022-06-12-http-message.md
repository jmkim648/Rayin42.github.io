---
layout: post
title: http 공부 정리 - 4. HTTP 메시지
subtitle: 
categories: http
tags: [http, study]
---

## HTTP message 공식 스펙
![](/img/http-message-structure.JPG)
HTTP-message =
start-line
*( header-field CRLF )
CRLF                    : 엔터 같은 것
[ message-body ]        : HTML 등..

### 시작 라인(start-line) - 요청 메시지
 - start-line = request-line / status-line
 - request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)
 -> HTTP 메서드(GET: 조회), 요청 대상(/search?q=hello&hl=ko), HTTP version

#### HTTP 메서드
 - 종류 : GET, POST, PUT, DELETE...
 - 서버가 수행해야 할 동작을 지정
   - GET : 리소스 조회
   - POST : 요청 내역 처리
   - ...

#### 요청 대상
 - absolute-path[?query] (절대경로[?쿼리])
 - 절대경로 : "/"로 시작하는 경로
   - *, http://...?x=y와 같이 다른 유형의 경로지정 방법도 존재


### 시작 라인(start-line) - 응답 메시지
 - start-line = request-line / status-line
 - status-line = HTTP-version SP status-code SP reason-phrase CRLF
 -> HTTP 버전, HTTP 상태 코드, 이유 문구
   - HTTP 상태 코드
     - 200 : 성공
     - 400 : 클라이언트 요청 오류
     - 500 : 서버 내부 오류
   - 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글

### HTTP 헤더 (header-field)
 - header-field = field-name ":" OWS field-value OWS (OWS: 띄워쓰기 허용)
   - file-name은 대소문자 구분이 없음 (value는 대소문자 구분)
 - 예시 
   - Host: www.google.com (요청)
   - Context-Type: text/html;charset=UTF-8 (응답)
     Content-Length: 3423

#### HTTP 헤더의 용도
  - HTTP 전송에 필요한 모든 부가정보
    - 예) 메시지 바디의 내용, 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보, 서버 애플리케이션 정보, 캐시 관리 정보...
  - 표준 헤더는 굉장히 많음!
    - https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
  - 필요시 임의의 헤더 추가 가능

### HTTP 메시지 바디
#### 메시지 바디의 용도
 - 실제 전송할 데이터 부분
 - HTML 문서, 이미지, 영상, JSON 등 byte로 표현할 수 있는 모든 데이터 전송 가능