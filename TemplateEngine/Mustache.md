# 머스테치(Mustache)

## 목차
1. [Mustache](#2-mustache)  
1-1. [Mustache?](#2-1-mustache)  
1-2. [문법](#2-2-문법)  
1-3. [Reference](#2-3-reference)  
***

### 1. Mustache
  - #### 1-1. Mustache?
    - Ruby, JS, Python, Java 등 대부분의 언어를 지원하는 심플한 템플릿 엔진

    - Java에서 사용될 땐 서버 템플릿 엔진, JS에서 사용될 땐 클라이언트 템플릿 엔진으로 사용 가능

    - 제일 큰 장점 =  Thymeleaf(Spring 권장)나 JSP와 달리 커뮤니티 버전에서도 플러그인 사용 가능!

  - #### 1-2. 문법
     - 변수
       ```
       데이터
       {
          "name" : "ABBO",
          "company" : "<b>Tistory</b>"
       }
       
       템플릿에서 사용시
       {{name}} - 이스케이프 된 HTML 언어 표시
       {{birth}} - 해당 변수는 없으므로 아무런 값도 표시 되지 않음
       {{company}} - 이스케이프 된 HTML 언어 표시
       {{{company}}} - 이스케이프 되지 않은 문자열 표시
       
       결과
       ABBO
       
       &lt;b&gt;Tistory&lt;/b&gt
       <b>Tistory</b>
       ```  
       
     - 파일 가져오기  
       ![image](https://user-images.githubusercontent.com/65080004/114388861-397d9880-9bcf-11eb-965b-708465d1ce51.png)  
       
       ```
       템플릿에서 사용시
       {{>layout/header}} - 현재 머스테치 파일(index.mustache)을 기준으로 다른 파일을 가져옴
       ```  
     
     - 반복문 - 변수가 배열일 경우 
       ```
       데이터 
       {
          "user" : [
           { "name" : "Mike" },
           { "name" : "Alsa" },
           { "name" : "Silly" }
         ]
       }
       
       템플릿에서 사용시
       {{#user}} - user라는 List를 순회, 자바의 for문과 동일 / 변수의 값이 배열로 되어 있기 때문에 반복문이 됨
           {{name}} - List에서 뽑아낸 객체의 필드 사용
       {{/user}}

       결과
       Mike
       Alsa
       silly
       ```
       
     - 조건문 - 변수가 배열이 아닐 경우, 단 0이나 false, 빈 문자열은 거짓으로 평가되므로 내용 출력 되지 않음
       ```
       데이터 
       {
          "sessionUser" : ABBO
       }
       
       템플릿에서 사용시
       {{#sessionUser}} - sessionUser가 존재할 경우 로그아웃 링크 a태그 표시
          <a href="/users/logout" class="navbar-brand">로그아웃</a>
       {{/sessionUser}}
       {{^sessionUser}} - sessionUser가 존재하지 않을 경우 로그인 링크 a태그 표시
          <a href="/users/loginForm" class="navbar-brand">로그인</a>
       {{/sessionUser}}
       

       결과
       
       객체 o
       로그아웃
       
       객체 x
       로그인
       ```
       
  - #### 1-3. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [ABBO Mustache 템플릿 문법 알아보기](https://abbo.tistory.com/5)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/TemplateEngine/README.md "Go README.md")
