# Web Server와 WAS(Web Application Server)

## 목차
1. [정리를 하게 된 이유](#1-정리를-하게-된-이유)    
2. [Web Server](#2-web-server)  
2-1. [Web Server란?](#2-1-web-server란)  
2-2. [동작 순서](#2-2-동작-순서)  
2-3. [기능](#2-3-기능)  
2-4. [정적 컨텐츠란?](#2-4-정적-컨텐츠란)  
4. [WAS(Web Application Server)](#3-wasweb-application-server)  
5. [중간 정리](#4-중간-정리)  
6. [Web Server 사용시 장점](#5-web-server-사용시-장점)  
7. [결론](#5-결론)  

***

### 1. 정리를 하게 된 이유
  - Web Server와 WAS(Web Application Server)의 차이를 알아보기 위해
  - Web Server가 왜 필요한지 알아보기위해

### 2. Web Server
  - #### 2-1. Web Server란?
    - 웹 브라우저(클라이언트)로 부터 HTTP 요청을 받아 HTML 문서와 같은 `정적 컨텐츠`를 제공하는 프로그램  
      
    ![image](https://user-images.githubusercontent.com/65080004/119777275-e3578100-bf00-11eb-9f34-861e378b3c94.png)  
  
  - #### 2-2. 동작 순서
    ```
    1. 클라이언트가 특정 path로 요청
    2. 웹 서버는 특정 path를 통해 넘어온 값을 가지고 파일을 찾음
    3. 찾은 파일을 웹서버에 넘겨줌
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

