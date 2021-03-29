# SPRING 노트
## 목차
1. [@Value annotation 사용하여 properties 값 받아오기](#1-value-annotation-사용하여-properties-값-받아오기)     
1-1. [현재 프로젝트 내 파일 위치](#1-1-현재-프로젝트-내-파일-위치)  
1-2. [해결 시도](#1-2-해결-시도)  
1-3. [배운점](#1-3-배운점)  
1-4. [Reference](#1-4-Reference)  
***
### 1. @Value annotation 사용하여 properties 값 받아오기
  - #### 1-1. 현재 프로젝트 내 파일 위치
    - .properties 파일 : WEB_INF 폴더 내부
    - root-context.xml : spring 폴더 내부
      ```
      properties 값을 사용하기 위한 내부 bean 선언
      <bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
	  	  <property name="location" value="/WEB-INF/properties/config.properties"/>
        <property name="fileEncoding" value="UTF-8" />
  	  </bean>
      ```
  
  - #### 1-2. 해결 시도 
    1. [호형 Spring PropertyPlaceholderConfigurer를 통해 불러온 값이 null이 나오는 현상 해결방법](https://oingdaddy.tistory.com/100)  
    2. [Hello World? SPRING에서 .properties 파일 사용하기](https://letter20.tistory.com/35)  
    3. [포르테시모 spring 설정 xml과 소스코드에서 properties 사용하기](https://jijs.tistory.com/entry/spring-%EC%84%A4%EC%A0%95-xml%EA%B3%BC-%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C%EC%97%90%EC%84%9C-properties-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)  
    4. 그외 삽질.. (시도 해봤는데 안됨.. 느낌은 있으나 확실하지 않으니까 더 모르겠음)  
    5. 시도 했으나 ${kl.clientid}값이 그대로 들어오는 것 확인 (오기생겨서 끝까지 해보자함.. ㅋㅋㅋㅋㅋ)  
       [ktko SPRING properties 읽어오기](https://ktko.tistory.com/entry/Spring-properties-%EC%9D%BD%EC%96%B4%EC%98%A4%EA%B8%B0)    
    6. 드디어 해결.. 변수 선언 후 setter 메서드에 @Value annotation 추가하여 해당 값 확인, 감사합니다  
       [복붙노트 Spring @Value 주석은 항상 null로 평가됩니까?](https://cnpnote.tistory.com/entry/SPRING-Spring-Value-%EC%A3%BC%EC%84%9D%EC%9D%80-%ED%95%AD%EC%83%81-null%EB%A1%9C-%ED%8F%89%EA%B0%80%EB%90%A9%EB%8B%88%EA%B9%8C)  
       ```java
       @Service
       public class ...Service {
        //properties에 있는 값(clientid) 받아오기 위한 변수
	      private String clientId;
	      ...
        
        // setter로 변수에 ${kl.clientid} 값을 넣어줌
        @Value("${kl.clientid}")
        public void setClientId(String clientId) {
          this.clientId = clientId;
        }
        // 받아온 값을 활용하기 위한 getter
        public String getClientId() {
          return clientId;
        }
       ```
  - #### 1-3. 배운점
    - web.xml
      ```
      설정을 위한 설정 파일
      
      WAS가 처음 구동될 때 web.xml을 읽어 웹 애플리케이션 설정을 구성
      
      DispatcherServlet을 등록해주면서 스프링 설정 파일을 지정
      DispatcherServlet은 초기화 과정에서 지정된 설정 파일을 이용해 스프링 컨테이너를 초기화시킨다
      
      <servlet-mapping>
		      <servlet-name>appServlet</servlet-name>
		      <url-pattern>/</url-pattern>
	    </servlet-mapping>
      web.xml 코드 중 ↑ 코드는 모든 요청을 DispatcherServlet이 처리하도록 서블릿 매핑을 설정한 것
      
      하지만, 위와 같은 설정을 하게되면 tomcat에 있는 / 설정을 무시하게 되므로 
      
      servlet-context.cml에 ↓ 코드를 통해 해결 가능
      <resources mapping="/resources/**" location="/resources/" />
      ```
    
    - servlet-context.xml
      ```
      이 context에 등록되는 Bean들은 servlet-container에만 사용되어진다
      @Controller 를 등록
      
      web.xml에서 DispatcherServlet 등록 시 설정한 파일
      설정 파일을 이용해서 스프링 컨테이너를 초기화
      
      ↓ 코드는 Annotation을 활용할 때 기본적인 Default 방식을 설정
      <!-- Enables the Spring MVC @Controller programming model -->
      <annotation-driven />

      ↓ 코드는 해당 패키지를 스캔해서 애노테이션을 명시한 클래스를 빈으로 등록
      <context:component-scan base-package="com.board.controller" />
      
      ↓ 코드의 viewResolver는 사용자의 요청에 대한 응답 view를 렌더링 하는 역할
      controller에서 return "home"; 시 /WEB-INF/views/home.jsp가 나옴
      <!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
      <beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
          <beans:property name="prefix" value="/WEB-INF/views/" />
          <beans:property name="suffix" value=".jsp" />
      </beans:bean>
      ```
      
    - root-context.xml
      ```
      context에 등록되는 Bean들은 모든 context에서 사용되어 진다.(공유가 가능하다)
      @Service와 @Repository 등
      공통적으로 사용하려는 Bean을 그때그때 사용한다?
      ```
      
    - 생각한 내용을 코드로 구현하기엔 아직 개념이 많이 부족함을 다시 한번 느꼈고, 구글 갓에게 감사함을 느낀 하루(거진 이틀..)였다.. 
  
  - #### 1-4. Reference
    - [호형 Spring PropertyPlaceholderConfigurer를 통해 불러온 값이 null이 나오는 현상 해결방법](https://oingdaddy.tistory.com/100)  
    - [Hello World? SPRING에서 .properties 파일 사용하기](https://letter20.tistory.com/35)  
    - [포르테시모 spring 설정 xml과 소스코드에서 properties 사용하기](https://jijs.tistory.com/entry/spring-%EC%84%A4%EC%A0%95-xml%EA%B3%BC-%EC%86%8C%EC%8A%A4%EC%BD%94%EB%93%9C%EC%97%90%EC%84%9C-properties-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)  
    - [ktko SPRING properties 읽어오기](https://ktko.tistory.com/entry/Spring-properties-%EC%9D%BD%EC%96%B4%EC%98%A4%EA%B8%B0)  
    - [복붙노트 Spring @Value 주석은 항상 null로 평가됩니까?](https://cnpnote.tistory.com/entry/SPRING-Spring-Value-%EC%A3%BC%EC%84%9D%EC%9D%80-%ED%95%AD%EC%83%81-null%EB%A1%9C-%ED%8F%89%EA%B0%80%EB%90%A9%EB%8B%88%EA%B9%8C)  
    - [좋은 글 수집가 스프링 설정](https://node-js.tistory.com/entry/Spring-webxml-root-contextxml-servlet-contextxml-%EC%97%AD%ED%95%A0Servlet-DispatcherServlet%EC%9D%B4%EB%9E%80)  
