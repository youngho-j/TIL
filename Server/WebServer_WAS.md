# Web Server와 WAS(Web Application Server)

## 목차
1. [정리를 하게 된 이유](#1-정리를-하게-된-이유)    
2. [Web Server](#2-web-server)  
2-1. [Web Server란?](#2-1-web-server란)  
2-2. [동작 순서](#2-2-동작-순서)  
2-3. [기능](#2-3-기능)  
2-4. [정적 컨텐츠란?](#2-4-정적-컨텐츠란)  
3. [WAS(Web Application Server)](#3-wasweb-application-server)  
3-1. [WAS(Web Application Server)란?](#3-1-wasweb-application-server란)  
3-2. [동작 순서](#3-2-동작-순서)  
3-3. [기능](#3-3-기능)  
3-4. [동적 컨텐츠란?](#3-4-동적-컨텐츠란)  
4. [중간 정리](#4-중간-정리)  
5. [Web Server를 따로 사용하는 이유](#5-web-server를-따로-사용하는-이유)  
5-1. [Web Server와 WAS의 목적이 다르기 떄문](#5-1-web-server와-was의-목적이-다르기-떄문)  
5-2. [책임 분할(기능 분리)을 통한 서버 부하 방지](#5-2-책임-분할기능-분리을-통한-서버-부하-방지)  
5-3. [여러대의 WAS 로드 밸런싱(부하 분산)](#5-3-여러대의-was-로드-밸런싱부하-분산)  
5-4. [여러대의 WAS Health check](#5-4-여러대의-was-health-check)  
5-5. [보안](#5-5-보안)    
6. [결론](#6-결론)  
6-1. [참고](#6-1-참고)   

***

### 1. 정리를 하게 된 이유
  - Web Server와 WAS(Web Application Server)의 차이를 알아보기 위해
  - Web Server가 왜 필요한지 알아보기위해

### 2. Web Server
  - #### 2-1. Web Server란?
    - 웹 브라우저(클라이언트)로 부터 HTTP 요청을 받아 HTML 문서와 같은 `정적 컨텐츠`를 제공하는 서버  
    - Ex) Apache, NGINX, IIS(windows 전용)  
      
    ![image](https://user-images.githubusercontent.com/65080004/119777275-e3578100-bf00-11eb-9f34-861e378b3c94.png)  
  
  - #### 2-2. 동작 순서
    ```
    [정적 컨텐츠의 경우]
    1. 클라이언트가 특정 path로 요청
    2. 웹 서버는 특정 path를 통해 넘어온 값을 가지고 파일을 찾음
    3. 찾은 파일을 웹서버에 넘겨줌
    4. 웹서버는 클라이언트에게 응답
    
    [동적 컨텐츠의 경우]
    1. 클라이언트가 특정 path로 요청
    2. 웹 서버는 요청을 WAS에 보냄
    3. WAS는 요청을 처리한뒤 웹 서버에 전달
    4. 웹서버는 클라이언트에게 응답
    ```
  - #### 2-3. 기능
    ```
    1. 클라이언트로부터 HTTP 요청을 받을 수 있다.
    
    2. 정적 컨텐츠 요청시
        - 정적 컨텐츠를 제공  
    
    3. 동적 컨텐츠 요청시  
        - WAS로 전달하여 WAS의 처리 결과를 클라이언트에 전달
    ```
 - #### 2-4. 정적 컨텐츠란?
   - 요청 인자 값에 상관없이 달라지지 않는 컨텐츠   
   - 어느 사용자 요청이든 `항상 동일한 컨텐츠`   
     
   ![image](https://user-images.githubusercontent.com/65080004/119777807-a8098200-bf01-11eb-8b73-8e01262d004a.png)  

### 3. WAS(Web Application Server)
  - #### 3-1. WAS(Web Application Server)란?
    - HTML 만으로는 할 수 없는 데이터베이스 조회나 다양한 로직처리 같은  
      `동적인 컨텐츠를 제공`하기 위해 만들어진 어플리케이션 서버  
    - HTTP 를 통해 컴퓨터나 장치에 어플리케이션을 수행해주는 `미들웨어`라고도 함  
    - 웹 서버와 웹 컨테이너의 결합으로 다양한 기능을 컨테이너에 구현하여 다양한 역할을 수행할 수 있는 서버  
    - Web Container / Servlet Container 라고도 불림
    - Web Server + Web Container 의 역할을 수행
    - Ex) Tomcat, Jeus, JBoss, Web Sphere 등  
    
    ![image](https://user-images.githubusercontent.com/65080004/119796341-430b5780-bf14-11eb-96c1-e90f4981a823.png)  
  
  - #### 3-2. 동작 순서
    ```
    1. 클라이언트가 특정 path로 요청
    2. WAS가 DB에서 데이터를 찾거나 로직 처리를 함
    3. 해당 값을 클라이언트에게 응답
    ```
    
  - #### 3-3. 기능
    ```
    1. 클라이언트로부터 HTTP 요청을 받을 수 있다. (대부분의 WAS는 WebServer 내장)
    2. 요청에 맞는 정적 컨텐츠를 제공할 수 있다.
    3. DB 조회나 다양한 로직처리를 통해 동적 컨텐츠를 제공할 수 있다. 
    4. Server단에서 어플리케이션을 동작할 수 있도록 지원한다. 
    ```  
    
    ![image](https://user-images.githubusercontent.com/65080004/119797854-9205bc80-bf15-11eb-918d-62915d7f1350.png)  
    
  - #### 3-4. 동적 컨텐츠란?
    - 누가, 언제, 어떻게 서버에 요청했는지에 따라 바뀔 수 있는 컨텐츠
    - Ex) 쇼핑몰, SNS와 서비스, 유튜브 추천영상 등  
    
### 4. 중간 정리
  - Web Server와 WAS(Web Application Server)의 차이는 `컨테이너 기능이 가능한지`의 차이  
    
    ![image](https://user-images.githubusercontent.com/65080004/119797471-39362400-bf15-11eb-9643-2a976c38e4f9.png)  

  - WAS의 기능을 보면 WebServer를 사용하지 않아도 정적, 동적 컨텐츠를 둘다 처리할 수 있음  
    그렇다면, WAS만을 사용하면 되는 것 아닌가?  
    
### 5. Web Server를 따로 사용하는 이유
  - #### 5-1. Web Server와 WAS의 목적이 다르기 떄문  
    - 정적인 콘텐츠 처리시 Web Server를 통하면 WAS를 이용하는 것보다 처리가 빠르고 안정적  
  
  - #### 5-2. 책임 분할(기능 분리)을 통한 서버 부하 방지  
    - 정적인 컨텐츠는 WebServer, 동적인 컨텐츠는 WAS가 담당

  - #### 5-3. 여러대의 WAS 로드 밸런싱(부하 분산)  
    - WAS가 처리해야 하는 요청을 여러 WAS가 나누어 처리할 수 있도록 설정 가능
  
  - #### 5-4. 여러대의 WAS Health check  
    - Health check란?  
      - 서버에 주기적으로 HTTP요청을 보내 서버의 상태를 확인
      - Ex) 특정 url 요청에 200응답이 오는지 확인
    - 명령어  
      - Interval - 서버 상태를 확인하는 요청을 날리는 주기 (default : 5s)
      - Fail - 지정된 횟수이상 연속 실패시 서버가 비정상이라고 인지 (default : 1회)
      - Passes - 서버가 복구되어 지정된 횟수 이상 연속 성공시 서버가 정상이라고 인지 (default : 1회)  
  
  - #### 5-5. 보안  
    - 리버스 프록시를 통해 실제 서버를 외부에 노출하지 않을 수 있음  
    - SSL / TLS에 대한 암복호화 처리에 사용  

### 6. 결론
  - WAS만으로 서비스가 가능하다. 
  - 그러나, WebServer를 사용한다면 서비스 확장성, 안정성 측면에서 WAS만 쓰는 것보단 향상 된다.

  - #### 6-1. 참고  
    - Web Server, WAS 아키텍처의 보편적 구조 
      다양한 구조를 가질 수 있음  
      ```
      예시
      
      1. Client → Web Server → DB
      2. Client → WAS → DB
      3. Client → Web Server → WAS → DB
      ```
        
      ![image](https://user-images.githubusercontent.com/65080004/119959004-8a5e1a80-bfde-11eb-851c-af69a1d8aba1.png)  
      
      TIER 1 - Web Server / TIER 2 - WAS / TIER 3 - Database(MySQL, Oracle, ...) 
      
    - 3번 구조의 동작과정
      ```
      1. Client 가 Web Server 로 HTTP Request를 전송
      
      2. Web Server 는 Client 의 Request 를 WAS 로 전송
      
      3. WAS 는 관련된 Servlet 을 메모리에 올림
      
      4. WAS는 web.xml을 참조하여 해당 Servlet에 대한 Thread를 생성
      
      5. HttpServletRequest 와 HttpServletResponse 객체를 생성하여 Servlet에 전달
      
      6. Thread 는 Servlet 의 service() 메서드를 호출
      
      7. service() 메서드는 요청에 맞게 doGet() 또는 doPost() 메서드를 호출
         메서드 예시 : protected doGet(HttpServletRequest request, HttpServletResponse response) { .. 
      
      8. WAS 는 해당 로직을 수행하다 DB 접근이 필요하면 Database 에 SQL Query 를 진행
      
      9. Database 는 SQL Query 에 따른 결과값을 Response 에 담아서 반환
      
      10. doGet() 또는 doPost() 메서드는 인자에 맞게 생성된 적절한 동적 페이지와 쿼리 결과를 Response 에 담아 WAS 에 전달
      
      11. WAS 는 Response 를 HttpResponse 형태로 바꾸어 Web Server 에 전달
      
      12. 생성된 Thread 를 종료하고, HttpServletRequest 와 HttpServletResponse 객체를 제거
      
      13. Web Server 는 HTTP Response 를 Client 에게 응답한다.
      ```

## Reference
  - [jaykee 정적 콘텐츠 그리고 동적 콘텐츠](https://itgit.co.kr/static_dynamic_content/)    
  - [우아한 tech Web Server vs WAS](https://www.youtube.com/watch?v=mcnJcjbfjrs)  
  - [Kim Ha Song Web Server와 WAS 차이](https://has3ong.github.io/webwas/)    
  - [Bubble Guppies 웹의 정적 & 동적 콘텐츠 ..](https://armontad-1202.tistory.com/entry/%EC%9B%B9%EC%9D%98-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0)  
  - [ResearchGate Tier3 Server Architecture](https://www.researchgate.net/figure/A-Typical-3-Tier-Server-Architecture-Tier-1-Web-Server-Tier-2-Application-Server-Tier_fig1_221147997)  
  - [Heee's Development Blog Web Server와 WAS의 차이와 웹 서비스 구조](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)  

***
[목록으로 이동](https://github.com/youngho-j/TIL/blob/main/Server/README.md) 

