# 스프링 핵심원리 - 기본편

## 목차  
1. [객체 지향 설계와 스프링](#1-객체-지향-설계와-스프링)  
1-1. [스프링의 탄생](#1-1-스프링의-탄생)  
1-2. [스프링이란?](#1-2-스프링이란)  
1-3. [좋은 객체 지향 프로그래밍?](#1-3-좋은-객체-지향-프로그래밍)  
1-4. [스프링과 객체 지향](#1-4-스프링과-객체-지향)  
1-5. [좋은 객체 지향 설계의 원칙](#1-5-좋은-객체-지향-설계의-원칙)  

***

### 1. 객체 지향 설계와 스프링  
### 1-1. 스프링의 탄생 
<details>
  <summary>스프링의 탄생 흐름 보기</summary>
  
- 예전 자바 진영의 기술 : `EJB(Enterprise Java Beans)`
  - 포함된 기술은 많았지만 어렵고, 복잡하고 느리다는 한계가 존재 
  
- EBJ에서 벗어나보려는 시도 발생
  - 순수한 자바로 복귀하자는 POJO 운동
  - `스프링 개발`  
 
- 스프링이 개발 됨으로써 EJB 컨테이너가 대체 됨  
  - 개발자  
    - 로드 존슨(EJB 문제점 지적과 EBJ 없이 개발하는 방법을 스프링에 녹임)  
    - 유겐 휠러(핵심 코드 대부분 개발)    
  - 전통적인 J2EE(EJB)라는 겨울을 넘어 새로운 시작이라는 의미로 스프링이라는 이름으로 탄생  
  - 또한, 하이버네이트가 EJB Entity 빈 기술 대체, 이후 자바 표준 JPA도 개발  
  
</details>  

### 1-2. 스프링이란?  
<details>
  <summary>자세히</summary>
  
- `여러 기술들의 모음`  
  
  ```
  [필수]
  스프링 프레임 워크, 스프링 부트
  
  [선택]
  스프링 데이터, 스프링 세션, 스프링 시큐리티, 스프링 Rest Docs, 스프링 배치, 스프링 클라우드, ...
  ```
  
#### 스프링 프레임워크[핵심 기술이 중요]
  
  ```
  - 핵심 기술 : 스프링 DI 컨테이너, AOP, 이벤트, 기타
  
  - 웹 기술 : 스프링 MVC, 스프링 WebFlux
  
  - 데이터 접근 기술 : 트랜잭션, JDBC, ORM 지원, XML 지원
  
  - 기술 통합 : 캐시, 이메일, 원격접근, 스케줄링
  
  - 테스트 : 스프링 기반 테스트 지원
  
  - 언어 : 코틀린, 그루비
  
  - 최근 스프링 부트를 통해 스프링 프레임워크의 기술들을 편리하게 사용
  ```
  
#### 스프링 부트
  ```
  - 스프링을 편리하게 사용할 수 있도록 지원, 최근에는 기본으로 사용
  
  - 단독으로 실행 할 수 있는 스프링 애플리케이션을 쉽게 생성
  
  - Tomcat 같은 웹 서버를 내장해서 별도의 웹서버를 설치하지 않아도 됨
  
  - 손쉬운 빌드 구성을 위한 starter 종속성 제공
    * 즉, starter 를 사용하면 starter에 포함된 여러 라이브러리를 가져다 쓸 수 있음 
  
  - 스프링과 3rd party(외부) 라이브러리 자동 구성
    * 스프링과 호환이 되는 라이브러리 버전을 지정하여 자동 구성
  
  - 메트릭, 상태 확인, 외부 구성 같은 프로덕션 준비 기능 제공
    * 운영환경에서 모니터링 같은 기능을 제공
  
  - 관례에 의한 간결한 설정
    * 왠만한 기능은 default로 되어있고, 필요시 커스텀하면 됨

  - "중간에서 편리하게 사용할 수 있도록 도와주는 것" (스프링 부트는 스프링 프레임워크와 별도로 사용하는 것은 아님!)
  ```

#### `스프링을 왜 만들었을까?`
  
  - `핵심 컨셉` : 단순하지만 매우 중요함
  
  - 어떤 컨셉을 가지고 만들었기에 스프링에 열광하는가
  
  - `스프링의 핵심 개념, 컨셉?`  
    - 스프링 : '자바 언어 기반'의 프레임 워크
    
    - 자바 언어의 큰 특징 : `객체 지향 언어`
    
    - 스프링은 `객체 지향언어가 가진 강력한 특징을 살려내는 프레임워크`
    
    - 즉, `좋은 객체 지향 애플리케이션을 개발할 수 있게 도와주는 프레임워크`  
  
</details> 

### 1-3. 좋은 객체 지향 프로그래밍?
<details>
  <summary>자세히</summary>  
  
#### 객체 지향 프로그래밍
  
  - 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러개의 독립된 단위로 파악하는 것  
    즉, `객체들의 모임으로 파악`하고자 하는 것  
  
  - 각각의 객체는 메시지를 주고 받는 `협력`을 통해 데이터를 처리한다. 
  
  - 프로그램을 `유연하고 변경이 용이`하게 만들어 대규모 소프트웨어 개발에 많이 사용됨  
    
  - 핵심 키워드 
    - `객체들의 모임`
    - `협력`  
      > 객체간 요청과 응답을 통해 데이터 처리 가능  
  
    - `다형성`  
      > 유연하고 변경이 용이함  
  
#### 객체 지향의 특징  
  
  - `추상화`, `캡슐화`, `상속`, `다형성`  
  
#### 객체 지향의 개념 중 다형성이 중요한 이유  
  
  - 다형성의 실세계 비유
    - 실세계와 객체 지향을 1:1로 매칭 할 수는 없지만 이해하기는 좋음
    
    - `역할(인터페이스)`과 `구현(인터페이스를 구현한 객체)`으로 세상을 구분
    
    - 예시  
      > 운전자 - 자동차  
        운전자는 자동차 모델(자동차 구현)이 바뀌어도 운전이 가능함  
        왜? 자동차의 역할을 충실히 수행하기 때문에  
      
      > 역할과 구현을 분리한 이유?  
        운전자(클라이언트)를 위해  
  
      > 클라이언트는 자동차 내부 구조를 몰라도 자동차 운전이 가능함  
        즉, 클라이언트에 영향을 주지 않고 새로운 기능을 제공할 수 있다.   
        이것이 가능한 이유는 역할과 구현이 분리되어 있기 때문이다. 
  
      > 공연무대(로미오와 줄리엣)  
        로미오 역할 - 배우(대체 가능)  
        줄리엣 역할 - 배우(대체 가능)  
  
#### 역할과 구현을 분리  
  
  - `역할`과 `구현`으로 구분하면 세상이 `단순`해지고, `유연`해지며 `변경`도 편리해짐
    
  - 장점
    - 클라이언트는 대상의 역할(인터페이스)만 알면 된다.
      
    - 클라이언트는 구현 대상의 내부구조를 몰라도 된다.
      
    - 클라이언트는 구현 대상의 내부 구조가 변경되어도 영향을 받지 않는다.
      
    - 클라이언트는 구현 대상 자체를 변경해도 영향을 받지 않는다.
  
  - 자바에서의 역할과 구현 분리    
    - 자바 언어의 다형성을 활용
      > 역할 = 인터페이스  
  
      > 구현 = 인터페이스를 구현한 클래스, 구현 객체
      
    - 객체 설계시 `역할과 구현을 명확히 분리`
      
    - 객체 설계시 역할(인터페이스)을 먼저 부여하고, 그 역할을 수행하는 구현 객체 만들기
    
#### 객체의 협력 관계부터 생각하기    
  ![image](https://user-images.githubusercontent.com/65080004/167812955-9f6e2430-4bbb-4b97-b4b0-b396219f5f12.png)  
  
  - 혼자 있는 객체는 없다.
      
  - 클라이언트 : 요청  
    서버 : 응답(요청에 반응한 행위)
      
  - 수 많은 객체 클라이언트와 객체 서버는 서로 협력 관계를 가진다.

  - 서버가 클라이언트가 되어 요청할 수도 있다.  
  
#### 자바 언어의 다형성  
 ![image](https://user-images.githubusercontent.com/65080004/167814088-b242ca44-4e29-4a4d-87fd-61335fc4c029.png)  
   
 - 오버라이딩 
   - 다형성으로 인터페이스를 구현한 객체를 실행 시점에 유연하게 변경할 수 있음  
   - 클래스 상속관계에서도 다형성, 오버라이딩 적용 가능  
     ![image](https://user-images.githubusercontent.com/65080004/167814390-5ee9f237-9ba6-42ea-ba77-4d250b8b80d2.png)  
     - 위 그림의 코드  
       ```java
       public class MemberService {
         private final MemberRepository memberRepository; 
         
         public MemberService(MemberRepository memberRepository) {
           this.memberRepository = memberRepository;
         }
         
         ...
       }
  
       // MemberService(new MemoryMemberRopository());
       MemberService(new JdbcMemberRopository());
       ```
       - 클라이언트는 MemberRepository에 의존한다면  
         [의존한다는 것은 내(MemberService)가 쟤(MemberRepository)를 알고 있다는 뜻]  
         MemoryMemberRepository와 JdbcMemberRepository를 모두 받아들일 수 있다.
  
#### 다형성의 본질
  - 인터페이스를 구현한 객체 인스턴스를 `실행 시점`에 `유연`하게 `변경` 가능
      
  - 다형성의 본질을 이해하려면 `협력`이라는 객체 사이의 관계에서 시작해야함
      
  - `클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경 가능`
    
#### 정리  
  
  - 실세계의 역할과 구현이라는 편리한 컨셉을 `다형성`을 통해 객체 세상으로 가져올수 있음
      
  - 유연하고, 변경이 용이
      
  - 확장 가능한 설계가 됨
      
  - 클라이언트에 영향을 주지 않는 변경 가능
      
  - `인터페이스(역할)를 안정적으로 잘 설계하는 것이 중요`  
    
#### 한계  
  
  - 역할 자체가 변하면, 클라이언트, 서버 모두 큰 변경 발생
      
  - 자동차를 비행기로 변경해야한다면?
      
  - 대본 자체가 변경된다면?
      
  - 즉, `인터페이스를 안정적으로 잘 설계하는 것이 중요`

</details>  
     
### 1-4. 스프링과 객체 지향  
<details>  
  <summary>자세히</summary>

- `다형성`이 가장 중요
  
- 스프링은 `다형성을 극대화해서 이용할 수 있게 도와준다.`
  
- 제어의 역전(IOC), 의존관계주입(DI)은 다형성을 활용해서 역할과 구현을 편리하게 다룰 수 있도록 지원
  
- 스프링을 사용하면 레고 블럭 조립하듯 구현을 편리하게 변경 할 수 있다. 
  
</details>  

### 1-5. 좋은 객체 지향 설계의 원칙  
<details>
  <summary>자세히</summary>  

#### SOLID란?
  
  - 로버트 마틴(클린코드 저)이 좋은 객체 지향 설계의 5가지 원칙의 앞 글자를 따서 만든 용어  
    `SRP`, `OCP`, `LSP`, `ISP`, `DIP`  
  
  - SOLID 원칙이 필요한 이유?  
    `시스템에 새로운 기능이 확장되거나 변경사항이 있는 경우 기존 기능들이 영향을 적게 받는 것`이 좋은 설계이기 때문  

#### `SRP 단일 책임 원칙` - Single Responsibility Principle   

  - `소프트웨어를 설계 시 객체(클래스)는 단 하나의 책임만 가질 수 있다.`
  
  - 하나의 책임?
    ```
    책임 like 기능 (이런 의미 정도로 해석하면 됨)
    
    새로운 기능이 확장 또는 변경사항이 생길 경우 파급효과가 적을 경우 하나의 책임을 가지고 있다고 볼 수 있음
    
    즉, 하나의 책임을 가진 프로그램은 '객체 간의 응집도는 높고 결합도가 낮은 프로그램'이라는 뜻으로 해석 가능
    ```
  
  - 예시
    ```java
    class Calculator {
      public void add(int a, int b){...}   // 더하기
      public void sub(int a, int b){...}   // 빼기
      public void mul(int a, int b){...}   // 곱하기
      public void div(int a, int b){...}   // 나누기
    }
    
    // 위의 Calculator 클래스는 사칙연산에 대한 기능만 가지고 있음
    // 이는 하나의 책임을 갖는다고 할 수 있음
    ```

#### `OCP 개방-폐쇄 원칙` - Open-Closed Principle

  - 소프트웨어가 기존의 코드를 변경하지 않고(Closed) 기능을 수정하거나 추가(Open)할 수 있다.  
    즉, `확장에는 열려있지만 변경에는 닫혀있어야 함`   
  
  - `설계시 변경되는 것이 무엇인지에 초점`을 맞춰야함  
    자주 변경되는 내용은 수정하기 쉽게 설계, 변경되지 않아야 하는 내용은 수정되는 내용에 영향을 받지않게 해야함  
    
  - 어떻게 변경하지 않고 기능을 확장하는가?  
    다형성을 활용하여 인터페이스를 구현한 새로운 클래스를 생성하여 기능 구현  
  
  - 예시
    ```java
    // Car 인터페이스(역할)
    public interface Car {
      public boolean isHybrid();
    }

    // Bus 구현 클래스
    public class Bus implements Car {
      @Override
      public boolean isHybrid() {
        return false;
      }
    }

    // Taxi 구현 클래스
    public class Taxi implements Car {
      @Override
      public boolean isHybrid() {
        return true;
      }
    }
    
    // Bus, Taxi가 하이브리드 차량인지 확인 하고 싶은 경우 
    // 기존 코드(Car interface)를 변경하지 않고 추가(구현 클래스를 추가)하여 확인 가능 
    Car bus = new Bus();
    Car taxi = new Taxi();
    
    bus.isHybrid(); // 결과 : false
    taxi.isHybrid(); // 결과 : true
    ```
  
  - 문제점 
    ```java
    public class MemberService {
      //private MemberRepository memberRepository = new MemoryMemberRepository();
       private MemberRepository memberRepository = new JdbcMemberRepository();
    }
    ```
    - 위와 같은 코드의 경우 MemberRepository 인터페이스를 상속 받아 구현한 새로운 클래스를 만들어 적용
      그러나, 새로운 객체를 변경하기 위해 MemberService의 코드를 변경해야하는 상황이 발생  
      분명 다형성을 활용하여 기능을 확장했지만 부득이하게 변경이 발생 됨
      이러한 상황을 해결하기 위해서 스프링이 DI 기술을 통해 해결해 줄 수 있음  

#### `LSP 리스코프 치환 원칙` - Liskov Substitution Principle

  - `객체는 프로그램의 정확성을 깨지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다`  
    => 클래스를 상속하는 자식 클래스들은 부모 클래스의 규약을 지켜야 한다.

  - 부모 클래스의 인스턴스 대신 자식 클래스의 인스턴스를 사용해도 문제가 없어야함을 의미  
    부모 클래스를 구현한 자식 클래스를 믿고 사용하기 위함
  
  - 상속 관계에서는 일반화 관계(is - a)가 성립해야함 (단어 교체를 통해 확인 가능)
    ```
    도형 클래스, 사각형 클래스(도형 클래스를 상속 받음)
    
    도형 클래스 {
      도형은 둘레를 가지고 있다.
      도형은 넓이를 기지고 있다.
      도형은 각을 가지고 있다.
    }
    
    사각형 클래스 extends 도형 클래스 {
      사각형은 둘레를 가지고 있다.
      사각형은 넓이를 기지고 있다.
      사각형은 각을 가지고 있다.
    }
    // 위 클래스는 일반화 관계가 성립하기에 LSP 만족한 설계라고 볼 수 있음
    
    원 클래스 extends 도형 클래스 {
      원은 둘레를 가지고 있다.
      원은 넓이를 기지고 있다.
      원은 각을 가지고 있다.
    }
    // 위 클래스에서 원은 각을 가지고 있다는 성립할 수 없으므로 LSP 만족할 수 있도록 수정이 필요함
    ```
  - 예시
    ```java
    
    // 부모 클래스
    public class Car {
      public void accel(int speed) {
        speed += 10;
      }
    }
    
    // 자식 클래스
    public class Santafe extends Car{
      @Override
      public void accel(int speed) {
        speed -= 20;
      }
    }
    
    // 위의 자식 클래스(Santafe)의 경우 컴파일시 문제가 생기지는 않으나,
    // 부모 클래스(Car)가 규정하고 있는 accel의 기능을 무시하는 경우이므로 
    // 이때 LSP에 위배되었다고 정의
    ```

#### `ISP 인터페이스 분리 원칙` - Interface Segregation Principle
  
  - `특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.`
  
  - 자신(구현 클래스)이 사용하지 않는 기능에는 영향을 받지 말아야한다.
  
  - 예시
    ```java
    interface People {
      public void cook();     //요리하기
      public void cleaning(); //청소하기

      public void work();     //작업하기
      public void submit();   //제출하기
    }
    
    // 일반적인 인터페이스(People | 위 코드)를 구체적인 여러 인터페이스(HouseKeeper, Worker | 아래 코드)로 나눠 설계해야함
    
    //가사도우미 인터페이스
    interface Housekeeper {
      public void cook();
      public void cleaning();
    }

    //직장인 인터페이스
    interface Worker {
      public void work();
      public void submit();
    }
    ```
  
#### `DIP 의존 관계 역전 원칙` - Dependency inversion Principle
  
  - `구체적인 것이 아니라 추상적인 것에 의존해야한다.`  
    즉, 구현체보다는 인터페이스나 추상 클래스에 의존하는 것이 좋다.
  
  - 의존 관계를 맺을 때 변화하기 쉬운 것(구체화 된 클래스) 보단 변화하기 어려운 것(추상클래스나 인터페이스)에 의존해야함
    위와 같이 설계시 기존 기능의 변경이나 새로운 요구사항을 통한 기능 확장이 되었을 때 유연한 변경이 가능  
  
  - 구조적 디자인에서 발생하던 `하위 레벨 모듈의 변경이 상위 레벨 모듈의 변경을 요구하는 위계 관계를 끊는` 의미의 역전  
    실제 사용 관계는 바뀌지 X, 추상을 매개로 메세지를 주고 받음으로써 관계를 최대한 느슨하게 만듦
    ![image](https://user-images.githubusercontent.com/65080004/146672525-01111dd0-e40b-494e-82e6-f9be1cea7bdb.png)  
  
#### 정리 
  
  - 객체 지향의 핵심은 `다형성`
  - 하지만 다형성만으로는 쉽게 부품을 바꾸듯 개발할 수 없음  
    - 왜?  
      구현 객체를 변경할 때 클라이언트 코드도 함께 변경되기 때문에  
  - 다형성 만으로는 OCP, DIP를 지킬 수 없다.  
  
</details>  

## Reference
 - [인프런 스프링 입문 - 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8#curriculum) 
 - [김영한 유튜브 좋은 객체 지향 프로그래밍이란](https://www.youtube.com/watch?v=lsPN-N2ze40) 
 - [JAVA 객체 지향 디자인 패턴 (정인상/채홍석 지음, 한빛미디어, 2014)]  
 - [zayson SOLID 원칙](https://velog.io/@zayson/Spring-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8-3-SOLID-%EC%9B%90%EC%B9%99)  
 - [Programming Note SOLID 원칙](https://dev-momo.tistory.com/entry/SOLID-%EC%9B%90%EC%B9%99)  
 - [keep going SOLID 원칙](https://velog.io/@hanblueblue/Java-SOLID-SRP-OCP-LSP-ISP-DIP)  
 - [dodeon 좋은 객체 지향 설계의 원칙](https://dodeon.gitbook.io/study/kimyounghan-spring-core-principle/01-oop-spring/oop-principle)  

***
[목록으로](https://github.com/youngho-j/TIL/blob/main/Spring/README.md)
