---
layout: post
title: html 공부 정리 - 2. URI&웹브라우저 흐름
subtitle: 
categories: html
tags: [html, study]
---

### URI(Uniform Resource Identifier)
리소스를 식별하는 통합된 방법
 - URI : URI는 로케이터(locator), 이름(name) 또는 둘 다 추가로 분류될 수 있다
 ![URL-URN](/img/URL-URN.JPG)
 - Uniform : 리소스를 식별하는 통일된 방식
 - Resource : 자원. URI로 식별할 수 있는 모든 것(제한 없음)
 - Identifier : 다른 항목과 구분하는데 필요한 정보(주민번호 같은 것)
   - URL(Uniform Resource Locator) : 리소스가 있는 위치를 지정
   - URN(Uniform Resource Name) : 리소스에 이름을 부여(잘 안씀)
     - 위치는 변할 수 있지만, 이름은 변하지 않는다.
     - URN 예시 : 서적의 고유번호 isbn
     - URN만으로 실제 리소스를 찾을 수 있는 방법이 보편화되어 있지 않기 때문에 흔히 URI는 URL을 지칭

### URL 문법
scheme://[userinfo@]host[:post][/path][?query][#fragment]
https://www.google.com:443/search?q=hello&hl=ko
 - 프로토콜(https)
 - 호스트명(www.google.com)
 - 포트번호(443)
 - 패스(/search)
 - 쿼리 파라미터(q=hello&hl=ko)

#### scheme
 - 주로 프로토콜 사용
 - 프로토콜: 어떤 방식으로 자원에 접근할 것인가 정하는 약속 규칙
 - ex) http, https, ftp 등
 - http는 80포트, https(HTTP Secure)는 443포트를 주로 사용(포트는 생략 가능)

#### userinfo
 - URL에 사용자 정보를 포함해서 인증
 - 거의 사용하지 않음

#### host
 - 호스트명
 - 도메인명 또는 IP 주소 그대로 사용

#### port
 - 접속 포트(PORT)
 - 상기한대로 일반적으로는 생략. default는 http = 80, https = 443

#### path
 - 리소스 경로, 계층적 구조
 - ex)
   - /hmoe/file1.jpg
   - /members
   - /members/100, /items/iphone12

#### query
 - key=value 형태
 - ?로 시작하며 &로 추가 가능 ?keyA=valueA&keyB=valueB
 - 보통 query parameter, query string 등으로 불림 (웹서버에 제공하는 파라미터, 문자 형태기 때문에)

### fragment
 https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-introducing-spring-boot

 윗 부분중 #getting-started-introducing-spring-boot
  - html 내부 북마크 등에 사용하며 서버에 전송하는 정보는 아님, 자주 사용하지 않음

### 웹브라우저 요청 흐름
사용자가 웹브라우저에서 구글 서버에 검색 요청을 보냈을 때!
![Http-massage](/img/Http-massage.JPG)
TCP/IP 패킷에 하단과 같은 HTTP 메시지를 포함해 전달
 - HTTP 요청 메시지 형태
 ```
 GET/search?q=hello&hl=ko HTTP/1.1
 Host: www.google.com
 ```

 요청 패킷이 구글 서버에 도착하면 구글 서버에서 하단과 같은 응답 메시지를 만들어 사용자에게 전달

 - HTTP 응답 메시지 형태 
 ```
 HTTP/1.1 200 OK
 Content-Type: text/html;charset=UTF-8
 Content-Length: 3423
 <html>
  <body>...</body>
 </html>
 ```

 응답 메시지가 도착하면 사용자의 웹브라우저에서 HTML 렌더링