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

## Reference
  - [jaykee 정적 콘텐츠 그리고 동적 콘텐츠](https://itgit.co.kr/static_dynamic_content/)    
  - [우아한 tech Web Server vs WAS](https://www.youtube.com/watch?v=mcnJcjbfjrs)  
  - [Kim Ha Song Web Server와 WAS 차이](https://has3ong.github.io/webwas/)    
  - [Bubble Guppies 웹의 정적 & 동적 콘텐츠 ..](https://armontad-1202.tistory.com/entry/%EC%9B%B9%EC%9D%98-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EC%BD%98%ED%85%90%EC%B8%A0)  

***
[목록으로 이동](https://github.com/youngho-j/TIL/blob/main/Server/README.md) 

