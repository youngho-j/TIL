# standaloneSetup vs webAppContextSetup
  - MockMvc
    - 실제 네트워크에 연결하지 않고 API 테스트가 가능하도록 모킹된 객체
    - MockMvcBuilders를 통해 세팅 필요함
  - MockMvcBuilders 제공 메서드
    ```java
    public static DefaultMockMvcBuilder webAppContextSetup(WebApplicationContext context)
    - 파라미터로 주어진 초기화된 WebApplicationContext를 사용하여 MockMvc 인스턴스를 빌드
    - Spring MVC 및 컨트롤러 인프라가 포함된 Spring 구성을 가리키는 것
      
    public static StandaloneMockMvcBuilder standaloneSetup(Object... controllers)
     - 테스트 할 컨트롤러를 수동으로 초기화하여 주입
     - 테스트하려는 컨트롤러를 직접 가리키고 Spring MVC 인프라를 프로그래밍 방식으로 구성하는 것
    ```

  - 정리  
    - standaloneSetup()
      ```
       - 단위 테스트에 조금 더 가까움
       
       - 한 번에 하나의 컨트롤러를 테스트
       
       - controller에 수동으로  mock dependencies를 주입할 수 있음
       
       - Spring configuration 로드를 포함하지 않는다
       
       - 스타일에 더 중점을 두고 있으며 테스트 중인 컨트롤러,  
         특정 Spring MVC configuration이 작동해야 하는지 여부 등을 쉽게 확인 가능
       
       - 일부 동작을 확인하거나 문제를 디버그하기 위해 임시 테스트를 작성하는 매우 편리한 방법
      ```
    - webAppContextSetup() 
      ```
       - 실제 Spring MVC 구성을 로드하여 보다 완전한 통합 테스트를 수행
       
       - TestContext 프레임워크는 로드된 Spring configuration을 을 캐시하기 때문에  
         더 많은 테스트가 추가되더라도 테스트를 빠르게 실행하는 데 도움이 됨
       
       - 웹 레이어 테스트에 집중하기 위해 Spring configuration을 통해 controllers에 mock 서비스를 주입할 수 있음
      ```
    - 둘 중 무엇을 써야할까?
      ```
      무엇을 사용하던 옳고 그른 답은 없음
      
      "standaloneSetup"을 사용하면 Spring MVC 구성을 확인하기 위해 몇 가지 추가 "webAppContextSetup" 테스트가 필요함을 의미
      
      "webAppContextSetup"으로 모든 테스트를 작성하고 항상 실제 Spring MVC 구성에 대해 테스트하도록 할 수 있음
      ```
  - 참고
    - @RunWith(SpringJUnit4ClassRunner.class)  
      ```
      ApplicationContext를 만들고 관리하는 작업을 할 수 있도록 jUnit의 기능을 확장
      
      기능 확장?
      - 기존 junit : 테스트 메서드별로 객체를 따로 생성해 관리
      
      - 확장된 junit : 컨테이너 기술 사용하여 `싱글톤`으로 관리되는 객체를 사용해 모든 테스트에 사용할 수 있음
      ```
    - @ContextConfiguration(locations = "classpath:xml파일위치")
      ```
      스프링 빈(Bean) 설정 파일의 위치를 지정할 수 있음  
      
      별도로 컨테이너를 추가하지 않고 Bean을 등록해둔 xml 파일을 지정해 컨테이너에서 사용할 수 있도록 도움
      
      Tip
      1. file:Full path" 형식으로 지정하면 불러오기 편함
      
      2. 대괄호"{}"를 통해 여러개 파일을 가져올 수 있음
      ```
    - @WebAppConfiguration
      ```
      통합 테스트를 위한 ApplicationContext가 WebApplicationContext여야 하는 경우 사용
      
      사용 이유
      - 테스트 시 WebApplicationContext가 로드 되었다는것을 보장  
        (백그라운드에서 MockServletContext 가 생성되어 TestContext 프레임워크 에 의해 테스트의 WebApplicationContext 에 제공)  
      
      - 어플리케이션의 루트 패스인 "file:src/main/webapp"를 디폴트 값으로 사용하는것을 보장
      ```
## Reference   
  - [Spring Testing docs](https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html#spring-mvc-test-server-setup-options)  
  - [Spring docs_MockMvcBuilders](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/test/web/servlet/setup/MockMvcBuilders.html)  
  - [Baeldung spring-webappconfiguration](https://www.baeldung.com/spring-webappconfiguration)  
  - [저장하고 까먹자 Spring junit test](https://jungguji.github.io/2020/05/30/Spring-Controller-Junit-Test/)  
  - [Spring Test 사용법](https://codevang.tistory.com/259)    
  - [keepgoing standaloneSetup vs webAppContextSetup](https://velog.io/@hanblueblue/Spring-mvc-standaloneSetup-vs-webAppContextSetup)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Test/README.md "Go README.md")