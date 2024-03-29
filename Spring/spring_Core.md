# 스프링 핵심원리 - 기본편

## 목차  
1. [객체 지향 설계와 스프링](#1-객체-지향-설계와-스프링)  
1-1. [스프링의 탄생](#1-1-스프링의-탄생)  
1-2. [스프링이란?](#1-2-스프링이란)  
1-3. [좋은 객체 지향 프로그래밍?](#1-3-좋은-객체-지향-프로그래밍)  
1-4. [스프링과 객체 지향](#1-4-스프링과-객체-지향)  
1-5. [좋은 객체 지향 설계의 원칙](#1-5-좋은-객체-지향-설계의-원칙)  
1-6. [객체 지향 설계와 스프링](#1-6-객체-지향-설계와-스프링)  

2. [스프링 핵심 원리 이해 - 예제 만들기](#2-스프링-핵심-원리-이해---예제-만들기)    
2-1. [프로젝트 생성](#2-1-프로젝트-생성)   
2-2. [비즈니스 요구사항](#2-2-비즈니스-요구사항)  
2-3. [회원 도메인 설계](#2-3-회원-도메인-설계)  
2-4. [회원 도메인 개발](#2-4-회원-도메인-개발)  
2-5. [회원 도메인 테스트](#2-5-회원-도메인-테스트)  
2-6. [회원 도메인 설계의 문제점](#2-6-회원-도메인-설계의-문제점)  
2-7. [주문과 할인 도메인 설계](#2-7-주문과-할인-도메인-설계)  
2-8. [주문과 할인 도메인 개발](#2-8-주문과-할인-도메인-개발)  
2-9. [주문과 할인 도메인 테스트](#2-9-주문과-할인-도메인-테스트)   

3. [스프링 핵심 원리 이해 - 객체지향 원리 적용](#3-스프링-핵심-원리-이해---객체지향-원리-적용)  
3-1. [새로운 할인 정책 개발 및 적용](#3-1-새로운-할인-정책-개발-및-적용)  
3-2. [OCP, DIP 원칙을 지키기 위한 방법](#3-2-ocp-dip-원칙을-지키기-위한-방법)  
3-3. [AppConfig 리팩토링](#3-3-appconfig-리팩토링)  
3-4. [새로운 할인 정책 적용](#3-4-새로운-할인-정책-적용)  
3-5. [지금까지의 흐름 정리](#3-5-지금까지의-흐름-정리)  
3-6. [IoC, DI, 그리고 컨테이너](#3-6-ioc-di-그리고-컨테이너)  
3-7. [스프링으로 전환하기](#3-7-스프링으로-전환하기)  

4. [스프링 컨테이너와 스프링 빈](#4-스프링-컨테이너와-스프링-빈)  
4-1. [스프링 컨테이너](#4-1-스프링-컨테이너)  
4-2. [스프링 컨테이너에 등록된 빈 조회](#4-2-스프링-컨테이너에-등록된-빈-조회)  
4-3. [스프링 빈 조회 - 기본](#4-3-스프링-빈-조회---기본)  
4-4. [스프링 빈 조회 - 동일 타입이 둘 이상](#4-4-스프링-빈-조회---동일-타입이-둘-이상)  
4-5. [스프링 빈 조회 - 상속관계](#4-5-스프링-빈-조회---상속관계)  
4-6. [Beanfactory와 ApplicationContext](#4-6-beanfactory와-applicationcontext)  

## Reference  
[스프링 핵심원리 기본편](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8)  

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
      > 운전자는 자동차 모델(자동차 구현)이 바뀌어도 운전이 가능함  
      > 왜? 자동차의 역할을 충실히 수행하기 때문에  
      
      > 역할과 구현을 분리한 이유?  
      > 운전자(클라이언트)를 위해  
    
      > 클라이언트는 자동차 내부 구조를 몰라도 자동차 운전이 가능함  
      > 즉, 클라이언트에 영향을 주지 않고 새로운 기능을 제공할 수 있다.   
      > 이것이 가능한 이유는 역할과 구현이 분리되어 있기 때문이다. 
    
      > 공연무대(로미오와 줄리엣)  
      > 로미오 역할 - 배우(대체 가능)  
      > 줄리엣 역할 - 배우(대체 가능)  

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

  - 소프트웨어를 설계 시 객체(클래스)는 `하나의 책임`만 가져야 한다
  
  - 하나의 책임?
     - 모호함.. 크거나 작을 수 있고, 문맥과 상황에 따라 달라질 수 있음  
     
     - 책임 like 기능 (이런 의미 정도로 해석하면 됨)
     
     - `중요한 기준은 변경`  
       변경시 파급효과가 적을 경우 하나의 책임을 가지고 있다고 볼 수 있음
     
     - 하나의 책임을 가진 프로그램은 '객체 간의 응집도는 높고 결합도가 낮은 프로그램'이라는 뜻으로 해석 가능  
  
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
    
  - 어떻게 `변경하지 않고 기능을 확장`하는가? (= 어떻게 다형성을 사용하는가?)    
    인터페이스를 구현한 새로운 클래스를 생성하여 기능 구현  
  
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

  - 객체는 프로그램의 정확성을 깨지 않으면서 `하위 타입의 인스턴스로 바꿀 수 있어야 한다.`  
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

  - 특정 클라이언트를 위한 `인터페이스 여러 개`가 범용 인터페이스 하나보다 낫다.
  
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

  - 구체적인 것이 아니라 `추상적인 것에 의존해야한다.`  
    즉, 구현체보다는 인터페이스나 추상 클래스에 의존하는 것이 좋음
  
  - 구현이 아닌 `역할(Role)에 의존하게 해야함`
  
  - 의존 관계를 맺을 때 변화하기 쉬운 것(구체화 된 클래스) 보단 변화하기 어려운 것(추상클래스나 인터페이스)에 의존해야함
    위와 같이 설계시 기존 기능의 변경이나 새로운 요구사항을 통한 기능 확장이 되었을 때 유연한 변경이 가능  


#### 정리 

  - 객체 지향의 핵심은 `다형성`
  - 하지만 다형성만으로는 쉽게 부품을 바꾸듯 개발할 수 없음  
    - 왜?  
      구현 객체를 변경할 때 클라이언트 코드도 함께 변경되기 때문에  
  - 다형성 만으로는 OCP, DIP를 지킬 수 없다.  

#### Reference  
  - [zayson SOLID 원칙](https://velog.io/@zayson/Spring-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-%EA%B8%B0%EB%B3%B8%ED%8E%B8-3-SOLID-%EC%9B%90%EC%B9%99)  
  - [Programming Note SOLID 원칙](https://dev-momo.tistory.com/entry/SOLID-%EC%9B%90%EC%B9%99)  
  - [keep going SOLID 원칙](https://velog.io/@hanblueblue/Java-SOLID-SRP-OCP-LSP-ISP-DIP)  
  - [dodeon 좋은 객체 지향 설계의 원칙](https://dodeon.gitbook.io/study/kimyounghan-spring-core-principle/01-oop-spring/oop-principle)  

</details>  

### 1-6. 객체 지향 설계와 스프링  
<details> 
  <summary>자세히</summary>  

#### 스프링과 객체 지향  
  - 스프링은 DI와 DI 컨테이너를 통해 다형성, OCP, DIP를 가능하도록 지원  
    - DI(Dependency Injection): 의존관계, 의존성 주입  
      각 클래스간의 의존관계를 빈(Bean)설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 것  
      
    - DI 컨테이너 [= 빈 팩토리(BeanFactory)]  
      [DI 컨테이너 추가 정보](https://dog-developers.tistory.com/12)  
    
    - 클라이언트 코드의 변경 없이 기능 확장이 가능해짐  

#### 내용 정리 
 - 모든 설계에 `역할`과 `구현`을 분리  

 - 애플리케이션 설계시 공연을 설계하듯 배역(역할)만 만들어두고,  
   배우(구현)는 언제든 `유연하게 변경`할 수 있도록 만드는 것이 좋은 객체 지향 설계  

 - 이상적으로는 모든 설계에 인터페이스를 부여하는게 좋음  
   - 하지만, 추상화하는 비용이 발생  
   - 따라서 기능 확장의 가능성이 없다면 구체 클래스를 직접 사용하거나  
   - 향후 필요시 리팩토링을 통해 인터페이스를 도입하는 것도 방법이 될 수 있다.  

#### Reference  
  - [개키우는 개발자 IoC 컨테이너와 DI](https://dog-developers.tistory.com/12)  
  - [lychee 객체 지향 설계와 스프링](https://velog.io/@lychee/%EC%8A%A4%ED%94%84%EB%A7%81-%ED%95%B5%EC%8B%AC-%EC%9B%90%EB%A6%AC-01.-%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%EC%84%A4%EA%B3%84%EC%99%80-%EC%8A%A4%ED%94%84%EB%A7%81#srp-%EB%8B%A8%EC%9D%BC-%EC%B1%85%EC%9E%84-%EC%9B%90%EC%B9%99-single-reponsibility-principle)  
    
## Reference
  - [인프런 스프링 입문 - 김영한](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8#curriculum) 
  - [김영한 유튜브 좋은 객체 지향 프로그래밍이란](https://www.youtube.com/watch?v=lsPN-N2ze40) 
  - [JAVA 객체 지향 디자인 패턴 (정인상/채홍석 지음, 한빛미디어, 2014)]  

</details> 

### 2. 스프링 핵심 원리 이해 - 예제 만들기  
### 2-1. 프로젝트 생성  
<details>
  <summary>자세히</summary>  

#### 스프링 부트 프로젝트 생성    
  1. [스프링 부트 스타터 사이트](https://start.spring.io/) 에서 생성 
  
  2. 프로젝트 설정  

    - Project : Gradle Project 선택   
    - Language : Java   
    - Spring Boot : 2.3.x 버전 선택   
      없을 경우 제일 낮은 버전을 선택(생성 후 변경 가능)  
    - Project Metadata  
      - Group : hello 작성
      - Artifact : core 작성
      - Packaging : Jar 선택  
      - Java : 11
      - Dependencies : 선택하지 않음
      - GENERATE를 눌러 zip 파일 생성  

  3. 원하는 폴더에 생성한 zip 파일 압축 해제  
  
  4. IntelliJ open을 통해 폴더 경로까지 이동  
  
  5. build.gradle을 open  
     초기 실행시 파일 설정으로인해 로딩시간이 김  
  
  6. build.gradle 아래와 같은 코드로 수정 (수정부분만 올림) 
     ```gradle
     plugins {
      id 'org.springframework.boot' version '2.3.3.RELEASE'
      id 'io.spring.dependency-management' version '1.0.9.RELEASE'
      id 'java'
     }
     
     ```

    ...
     
     dependencies {
          implementation 'org.springframework.boot:spring-boot-starter'
          testImplementation('org.springframework.boot:spring-boot-starter-test') {
              exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
          }
     }
      
     ...
     ```

  7. Load Gradle change 버튼 클릭하여 Gradle 로딩  
     Problems에 오류가 있을 경우 Reload All Gradle Project를 통해 다시 한번 리로드  
     참고, Gradle 탭은 우측 상단에 위치  
  
  8. 설정 완료 

#### 실행속도 빠르게 설정하기  
  - 최근 IntelliJ 버전은 Gradle을 통해서 실행 하는 것이 기본 설정  
    실행속도가 느림  
  
  - 다음과 같이 변경하여 실행속도 향상  
    1. File 탭에서 Settings 클릭 (Mac의 Preferences와 같음)   
    
    2. gradle 검색 시 (Build, Execution, Deployment / Build Tools / Gradle)이 검색됨  
       (Mac : Preferences → Build, Execution, Deployment → Build Tools → Gradle)  
    
    3. Gradle projects의 설정을 아래와 같이 변경  
       - Build and run using  
         : Gradle → `IntelliJ IDEA`  
       - Run tests using  
         : Gradle → `IntelliJ IDEA`  
    
    4. 설정 저장  

</details>  

### 2-2. 비즈니스 요구사항  
<details>
  <summary>자세히</summary>  

#### 회원  
  - 회원 가입, 조회 가능  
  - 회원 등급 존재(일반, VIP)  
  - 회원 데이터는 자체 DB를 구축할 수 있고, 외부 시스템과 연동할 수 있음 (미확정)  

#### 주문과 할인 정책
  - 회원은 상품 주문 가능
  - 회원 등급에 따라 할인 정책을 적용할 수 있음
  - 할인 정책은 모든 VIP는 1000원을 할인해주는 고정 금액 할인을 적용해달라.  
      (추후 변경 될 수 있음)  
  - 할인 정책은 변경 가능성이 높음  
      회사의 기본 할인 정책을 아직 정하지 못했고, 오픈 직전까지 고민을 미루고 싶다.  
      최악의 경우 할인을 적용하지 않을 수도 있다. (미확정)  

#### 정리
  - 요구사항에서 회원 데이터, 할인 정책 부분은 현재 결정하기 어려운 부분  
  - 그렇다고 결정되기까지 무기한 기다릴 수는 없음  
  - 객체 지향 설계 방법을 통해 인터페이스를 생성하여  
      구현체를 언제든 갈아끼울 수 있도록 설계하면 개발이 가능

</details>   

### 2-3. 회원 도메인 설계  
<details>
  <summary>자세히</summary>  

#### 회원 도메인 요구사항
  - 회원 가입, 조회 가능  
  - 회원 등급 존재(일반, VIP)  
  - 회원 데이터는 자체 DB를 구축할 수 있고, 외부 시스템과 연동할 수 있음 (미확정)   

#### 회원 도메인 협력 관계  
  ![image](https://user-images.githubusercontent.com/65080004/168537018-75379a60-81ff-4c50-bf47-9db27b53626b.png)  
  - 회원 DB를 자체 구축 할 수도 있고, 외부 시스템과 연동할 수 있으므로, 데이터 접근 계층을 따로 만들어둠  
  - 회원 저장소 인터페이스(역할)를 두고, 구현은 메모리, DB, 외부 저장소로 분리  

#### 회원 클래스 다이어 그램  
  ![image](https://user-images.githubusercontent.com/65080004/168537413-356f97d1-0be3-4522-bf3b-2235698877e0.png)  
  - MemberService(회원 서비스 역할)는 인터페이스로 생성,  
      역할의 구현체인 MemberServiceImpl을 따로 생성  
      
  - MemberRepository(회원 저장소 역할)는 인터페이스로 생성,  
      역할의 구현체인 Memory와 DB를 따로 생성   

#### 회원 객체 다이어그램  
  ![image](https://user-images.githubusercontent.com/65080004/168537942-5234364f-6106-4112-9687-83b8c05dece6.png)  
  - 실제 서버에서의 인스턴스 간 참조 관계  
  - 회원 서비스 주소 값 :  MemberServiceImpl  
  - 회원 저장소 주소 값 : MemoryMemberRepository  

</details> 

### 2-4. 회원 도메인 개발  
<details>
  <summary>자세히</summary>  

#### 회원 엔티티  
  - 회원 등급  
     ```java
     package hello.core.member;

     public enum Grade {
       BASIC,
       VIP
     }
     ```

  - 회원 엔티티  
     ```java
     package hello.core.member;

     public class Member {

       private Long id;
       private String name;
       private Grade grade;

       ...
       // 생성자 및 Getter, Setter 추가
     }   
     ```
     - Entity : 실체, 객체라는 의미를 가지며, 실무에선 엔티티라고 부름  

#### 회원 서비스  
  - 회원 서비스 인터페이스  
    - 회원 가입, 조회 두가지 기능  
      1. void join(Member member)  
      2. Member findMember(Long memberId)  

    - 이상적으로는 모든 설계에 인터페이스를 부여하면 좋음  
       - 하지만 모든 설계에 인터페이스를 도입하면 추상화라는 비용이 발생  
       - 따라서 기능을 확장할 가능성이 없다면, 구체 클래스를 직접 사용하거나  
       - 향후 필요시 리팩토링을 통해 인터페이스를 도입하면 됨  
    - 현재 코드에선 `역할과 구현을 분리하는 것에 초점`을 맞추어  
     MemberService도 역할(Interface)과 구현(Impl)로 분리했다.  

  - 회원 서비스 구현체  
     ```java
     package hello.core.member;

     public class MemberServiceImpl implements  MemberService{

       private final MemberRepository memberRepository 
                              = new MemoryMemberRepository();
       회원 서비스 인터페이스 Override 메서드 작성
     }
     ```
     - 인터페이스의 구현객체가 한개일 경우  
      구현 클래스이름을 `인터페이스명Impl`이라고 짓는다.   

#### 회원 저장소
  - 회원 저장소 인터페이스  
    - 저장, 아이디 검색 메서드  
      1. void save(Member member);  
      2. Member findById(Long memberId);  
    
    - 데이터 베이스가 미정이지만, 개발을 진행해야함으로 단순하게 구현  
   
  - 회원 저장소 구현체  
     ```java
     package hello.core.member;

     import java.util.HashMap;
     import java.util.Map;

     public class MemoryMemberRepository implements  MemberRepository{

       private  static Map<Long, Member> store = new HashMap<>();

       // 회원 저장소 인터페이스 Override 메서드 작성
     }
     ```
     - HashMap은 동시성 이슈가 발생할 수 있어, 실무에서는 ConcurrentHashMap을 사용함  
     

</details>

### 2-5. 회원 도메인 테스트  
<details>
  <summary>자세히</summary>  

#### 회원 도메인 테스트  
  - 회원 가입 테스트  
    - org.assertj.core.api.Assertions 클래스  
      - Assertions.assertThat(객체1).isEqaulsTo(객체2)  
      - assertThat()으로 비교할 대상(객체1)을 설정하고  
       iisEqualTo()로 사용자가 생각하는 값(객체2)을 비교하여 맞는지 검사하는 테스트  

</details>

### 2-6. 회원 도메인 설계의 문제점     
<details>
  <summary>자세히</summary>  

#### 문제점  
  ```java
  public class MemberServiceImpl implements MemberService {

    private final MemberRepository memberRepository = new MemoryMemberRepository();
		...
  }
  ```
  - 위의 MemberServiceImpl 코드를 보면  
     - MemberRepository와 MemoryMemberRepository를 모두 의존  
     - 즉, 의존관계가 인터페이스(추상화) 뿐만 아니라 구현(구체화)까지 모두 의존  
     - 변경이 발생되었을때 문제가 되며, DIP를 위반  

</details>

### 2-7. 주문과 할인 도메인 설계     
<details>
  <summary>자세히</summary>  

#### 주문과 할인 정책 요구사항
  - 회원은 상품 주문 가능

  - 회원 등급에 따라 할인 정책을 적용할 수 있음

  - 할인 정책은 모든 VIP는 1000원을 할인해주는 고정 금액 할인을 적용해달라  
      (추후 변경 될 수 있음)  
      
  - 할인 정책은 변경 가능성이 높음  
      회사의 기본 할인 정책을 아직 정하지 못했고, 오픈 직전까지 고민을 미루고 싶다.  
      최악의 경우 할인을 적용하지 않을 수도 있다. (미확정)  

#### 주문 도메인 협력, 역할, 책임  
  ![image](https://user-images.githubusercontent.com/65080004/168757778-fc4c1806-23c5-4388-b246-7d74a5576a34.png)  
  1. 주문 생성 : 클라이언트는 주문 서비스에 주문 생성을 요청  
  2. 회원 조회 : 할인을 적용하기 위해 회원 등급이 필요  
	  → 주문 서비스는 회원 저장소에서 회원을 조회한다.  
  3. 할인 적용 : 주문 서비스는 회원 등급에 따른 할인 여부를 할인 정책에 위임  
  4. 주문 결과 반환 : 주문 서비스는 할인 결과를 포함한 주문 결과를 반환

#### 주문 도메인 전체 
  ![image](https://user-images.githubusercontent.com/65080004/168758947-0eb0193e-f479-489f-afaa-5696ea9db4db.png)  
  - 역할과 구현을 분리하여 자유롭게 구현 객체를 조립할 수 있도록 설계  
      → 저장소와 할인 정책 유연하게 변경 가능  

#### 주문 도메인 클래스 다이어그램  
  ![image](https://user-images.githubusercontent.com/65080004/168759340-95051c87-f2f6-4f1a-a5c6-4aed91c2f71f.png)  

#### 주문 도메인 객체 다이어그램  
  ![image](https://user-images.githubusercontent.com/65080004/168759719-f32ee338-ee76-4b43-8a61-61009e7b0ccf.png)  
  - 회원을 메모리에서 조회하고, 정액 할인 정책을 적용해도 주문 서비스를 변경하지 않아도 됨  
      역할들의 협력관계를 그대로 재사용 할 수 있음  

  ![image](https://user-images.githubusercontent.com/65080004/168760088-a604dfb4-94e2-409d-85ec-73292a9f92be.png)  
  - 회원을 실제 DB에서 조회하고, 정률 할인 정책을 지원해도 주문 서비스를 변경하지 않아도 됨  
      협력 관계를 그대로 재사용 할 수 있음  

  - 역할과 구현이 분리되어있기 때문에 회원 저장소, 할인 정책의 구현체가 변경되어도 MemberService의 변경이 없음  

</details>

### 2-8. 주문과 할인 도메인 개발     
<details>
  <summary>자세히</summary>  

#### 할인 정책  
  - 할인 정책 인터페이스  
    - 할인 금액 리턴 메서드 작성  
      - int discount(Member member, int price);
    
  - 정액 할인 정책 구현체  
    ```java
    package hello.core.discount;

    import hello.core.member.Grade;
    import hello.core.member.Member;

    public class FixDiscountPolicy implements DiscountPolicy {

      private int discountFixAmount = 1000;  // 1000원 할인

      // 할인 정책 인터페이스 메서드 Override
    }
    ```
    - 할인에 관련된 기능을 가지고 있음  
    - Grade가 VIP인 경우 1000원 할인 적용

#### 주문 엔티티  
  - 주문 엔티티
    ```java
    package hello.core.Order;

    public class Order {

      private Long memberId;
      private String iteamName;
      private int itemPrice;
      private int discountPrice;

      // 생성자, Getter, Setter, ToString 메서드 생성
    }
    ```

#### 주문 서비스  
  - 주문 서비스 인터페이스  
    - 주문 생성 메서드 작성  
      - Order createOrder(Long memberId, String itemName, int itemPrice)
  
  - 주문 서비스 구현체  
    ```java
    package hello.core.Order;

    public class OrderServiceImpl implements OrderService {

      private final MemberRepository memberRepository 
                                     = new MemoryMemberRepository();
      private final DiscountPolicy discountPolicy 
                                    = new FixDiscountPolicy();

      // 주문 서비스 인터페이스 메서드 Override
      
    }
    ```
    - MemoryMemberRepository와 FixDiscountPolicy를 구현체로 생성
    - 주문 생성 요청이 오면,  
      1. 회원 정보 조회  
      2. 할인 정책 적용
      3. 주문 객체 생성하여 반환  

#### 주문 서비스 구현체의 문제점  
  - DIP 원칙 위반 
    ```java
    public class OrderServiceImpl implements OrderService {

      private final MemberRepository memberRepository 
                                     = new MemoryMemberRepository();
      private final DiscountPolicy discountPolicy 
                                    = new FixDiscountPolicy();
      ...
    }
    ```
    - 구현체인 MemoryMemberRepository, FixDiscountPolicy에 의존하기 때문에 `DIP 위반`  
	

</details>

### 2-9. 주문과 할인 도메인 테스트     
<details>
  <summary>자세히</summary>  

#### 주문과 할인 정책 테스트
  - 주문 서비스 테스트  
    - 주문 생성 메서드 테스트 코드 작성  
    - 단위 테스트가 중요함!  
      `단위 테스트` : 스프링 및 컨테이너의 도움 없이 순수하게 자바 코드를 테스트  
</details>  

### 3. 스프링 핵심 원리 이해 - 객체지향 원리 적용  
### 3-1. 새로운 할인 정책 개발 및 적용  
<details>
  <summary>자세히</summary>  

#### 할인 정책 확장  
  - 기존 사용하던 고정 금액 할인이 아닌 주문금액당 할인하는 정률(%) 할인 정책으로 변경하고 싶다. 
    
    - 객체 지향 설계 원칙을 준수한다면 유연하게 설계를 변경 가능  
    
  - 정률 할인 정책 클래스 추가  
    - 기대한 의존 관계  
      ![image](https://user-images.githubusercontent.com/65080004/170213433-bac110ea-4248-4178-9cee-05f1f3a8da6e.png)  
    - FixDiscountPolicy와 마찬가지로 기존 DiscountPolicy를 상속받아 생성  
        ```java
        public class RateDiscountPolicy implements DiscountPolicy {

          private int discountPercent = 10;

          @Override
          public int discount(Member member, int price) {
            // 정률 할인 코드 작성
          }  
        }
        ```
    - 반드시 실패, 성공 테스트 코드를 작성하여 테스트 해볼 것! 
  
  - 정책 적용 및 문제점
    - 적용시 클라이언트(OrderServiceImpl) 코드  
        ```java
        public class OrderServiceImpl implements OrderService {

          private final MemberRepository memberRepository = new MemoryMemberRepository();
          // private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
          private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
          
          ...
        }
        ```
    
    - 문제점  
        - 잘 지켜진 것 같은데 뭔가 이상하다..  
          1. OrderServiceImpl 클래스에서 추상(인터페이스) 뿐만 아니라 구체화된 클래스에 의존하는 것을 볼 수 있음  
             ![image](https://user-images.githubusercontent.com/65080004/170219524-df16697d-7f09-43c6-8821-886e91e35c9a.png)  
             즉, `DIP 위반`    
             참고, 해당 클래스에 코드로 기재되어 있는 경우 의존이라고 표현한다.  
          2. 기능을 확장하여 생성한 RateDiscountPolicy를 적용시 OrderServiceImpl에 코드 변경이 일어나게 됨  
             ![image](https://user-images.githubusercontent.com/65080004/170219612-11afe262-da5d-4316-9546-16bb3dda80db.png)  
             즉, `OCP 위반`    
    
    - 해결 방법
        - 추상(인터페이스)에만 의존하도록 변경  
          - OrderServiceImpl의 코드를 아래처럼 수정  
            ```java
            // 변경 전  
            private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
            
            // 변경 후
            private final DiscountPolicy discountPolicy;
            ```
          - 수정 후 구현체가 존재하지 않아 실행시 NPE(null pointer exception) 가 발생  
        - OrderServiceImpl에 DiscountPolicy의 구현체를 생성하고 주입해줄 무언가가 필요함  
</details>  

### 3-2. OCP, DIP 원칙을 지키기 위한 방법  
<details>
  <summary>자세히</summary>  

#### 관심사의 분리  
  - 관심사?  
      - 클래스의 책임, 역할이라고 생각하면 됨  
      - 그렇다면, OrderServiceImpl 클래스는 어떤 역할을 하고 있는가?  
      - 객체의 `실행`과 `객체의 생성과 연결`이라는 두 가지 역할을 동시에 하고 있음  
      - 두 가지 역할 중 한 가지 역할을 담당할 클래스가 추가적으로 필요  
  
  - AppConfig의 등장  
      - `객체의 생성과 연결` 역할을 수행하기 위해 추가 되는 클래스  
        > AppConfig : Application + Config(구성, 설정)  
        > 애플리케이션의 전체 동작 방식을 구성, 설정 한다는 의미
      - 애플리케이션의 전체 동작 방식을 구성(config)하기 위해,  
        `구현 객체를 생성하고, 연결하는 책임`을 가지는 별도의 설정 클래스  
      - 코드  
        ```java
        public class AppConfig {

          public MemberService memberService() {
            return new MemberServiceImpl(new MemoryMemberRepository());
          }

          public OrderService orderService() {
            return new OrderServiceImpl(new MemoryMemberRepository(), new RateDiscountPolicy());
          }

        }
        ```
        - 애플리케이션의 실제 동작에 필요한 `구현 객체를 생성`  
          - MemberServiceImpl  
          - MemoryMemberRepository  
          - OrderServiceImpl  
          - FixDiscountPolicy  
        
        - 생성한 객체 인스턴스(..Service)의 참조(레퍼런스)를 `생성자를 통해서 주입(연결)`  
          - MemberServiceImpl → MemoryMemberRepository  
          - OrderServiceImpl → MemoryMemberRepository , RateDiscountPolicy  
      
  - MemberServiceImpl 변경점  
      ```java
      public class MemberServiceImpl implements MemberService {

        private final MemberRepository memberRepository;

        public MemberServiceImpl(MemberRepository memberRepository) {
          this.memberRepository = memberRepository;
        }
		    ...
      }
      ```
      - 생성자 주입을 받을 수 있도록 생성자를 통해 MemberRepository 인터페이스를 주입 받을 수 있도록 설정 변경   
      - MemberServiceImpl은 MemberRepository에 의존하기 때문에 `DIP`를 만족하게 됨  
      - MemberServiceImpl은 생성자를 통해 어떤 구현 객체가 들어올지(주입 될 지)는 알 수 없음   
      - 생성자를 통해서 어떤 구현 객체를 주입할지는 오직 외부(AppConfig)에서 결정  
      - MemberServiceImpl은 `실행` 에만 집중하면 됨  
      
      - 클래스 다이어그램  
        ![image](https://user-images.githubusercontent.com/65080004/170268915-c1d69aed-7745-4296-8467-09181bbfac81.png)  
        - `객체의 생성과 연결`은 `AppConfig`가 담당  
        - MemberServiceImpl 은 MemberRepository 인 추상에만 의존하게 되어 `DIP 만족`  
        - 객체를 생성하고 연결하는 역할과 실행하는 역할이 명확히 분리되어 `관심사의 분리`가 이루어짐  
        - 클라이언트인 memberServiceImpl 입장에서 의존관계를 마치 외부에서 주입해주는 것으로 보여    
          `DI(Dependency Injection) - 의존관계 주입 or 의존성 주입`이라고 함  
  
  - OrderServiceImpl 변경점  
      ```java
      public class OrderServiceImpl implements OrderService {

        private final MemberRepository memberRepository;
        private final DiscountPolicy discountPolicy;

        public OrderServiceImpl(MemberRepository memberRepository, DiscountPolicy discountPolicy) {
          this.memberRepository = memberRepository;
          this.discountPolicy = discountPolicy;
        }
		    ...
      }
      ```
      - 생성자 주입을 받을 수 있도록 생성자를 통해  
        MemberRepository 인터페이스, DiscountPolicy 인터페이스를 주입 받을 수 있도록 설정 변경  
      - OrderServiceImpl은 MemberRepository, DiscountPolicy에 의존하기 때문에 `DIP`를 만족하게 됨  
      - OrderServiceImpl은 생성자를 통해 어떤 구현 객체가 들어올지(주입 될 지)는 알 수 없음   
      - 생성자를 통해서 어떤 구현 객체를 주입할지는 오직 외부(AppConfig)에서 결정  
      - OrderServiceImpl은 `실행` 에만 집중하면 됨  
      
  - AppConfig 적용 여부 확인을 위한 실행  
      - MemberApp  
        ```java
        public static void main(String[] args) {
        
          AppConfig appConfig = new AppConfig();
          MemberService memberService = appConfig.memberService();
          ...
        
        }
        ```
      - OrderApp  
        ```java
        public static void main(String[] args) {
            
          AppConfig appConfig = new AppConfig();
          MemberService memberService = appConfig.memberService();
          OrderService orderService = appConfig.orderService();
          ...
        
        }
        ```
  
  - Junit 테스트 코드 수정  
      - MemberServiceTest  
        ```java
        class MemberServiceTest {

          MemberService memberService;

          @BeforeEach // 각 테스트 실행 전 호출
          void beforeEach() {
            AppConfig appConfig = new AppConfig();
            memberService = appConfig.memberService();
          }
          ...
        }
        ```
      
      - OrderServiceTest  
        ```java
        class OrderServiceTest {

          MemberService memberService;
          OrderService orderService;

          @BeforeEach // 각 테스트 실행 전 호출
          void beforeEach() {
            AppConfig appConfig = new AppConfig();
            memberService = appConfig.memberService();
            orderService = appConfig.orderService();
          }
          ...
        }
        ```

  - 정리  
      - AppConfig를 통해 관심사를 확실히 분리함  
      - DIP, OCP, SRP 만족  
        - DIP : MemberService, OrderService 인터페이스에만 의존  
        - OCP : 코드 변경시 AppConfig을 수정하므로 MeberServiceImpl, OrderServiceImpl를 수정하지 않아도 됨  
        - SRP : AppConfig에서 객체 생성/연결 역할, MeberServiceImpl, OrderServiceImpl은 실행 역할로 단일 책임만 가짐  
      - 배역, 배우를 생각 해보기
      - AppConfig는 구체 클래스를 선택하고 연결하는 역할  
        즉, 공연 기획자의 역할

</details>  

### 3-3. AppConfig 리팩토링  
<details>
  <summary>자세히</summary>  

#### AppConfig의 문제점  
  - 중복 존재  
      - new MemoryMemberRepository() 코드 중복  
      - 현재는 Service가 적어 큰 문제가 없어보이나, Service가 늘어나 100곳이 된다고 했을때  
        100곳에서 MemoryMemberRepository가 쓰인다면? ... 어휴  
  
  - 역할에 따른 구현 파악이 어려움  
      ```java
      public class AppConfig {

        public MemberService memberService() {
          return new MemberServiceImpl(new MemoryMemberRepository());
        }

        public OrderService orderService() {
          return new OrderServiceImpl(new MemoryMemberRepository(), new FixDiscountPolicy());
        }

      }
      ```
      - MemberService와 OrderService 역할은 파악할 수 있음
      - MemberRepository와 DiscountPolicy의 역할은 파악이 힘듦  
        아 객체 생성시 필요한 구현체구나 정도로 생각... 

#### AppConfig의 리팩토링  
  - 리팩토링 후 코드  
      ```java
      public class AppConfig {

        public MemberService memberService() {
          return new MemberServiceImpl(MemberRepository());
        }

        private MemberRepository MemberRepository() {
          return new MemoryMemberRepository();
        }

        public OrderService orderService() {
          return new OrderServiceImpl(MemberRepository(), DiscountPolicy());
        }

        private DiscountPolicy DiscountPolicy() {
          return new FixDiscountPolicy();
        }
      }
      ```
      - 중복 제거 
        - 중복되는 new MemoryMemberRepository()를 메서드로 추출  
        - MemberRepository() `메서드 명을 통해 역할이 보임`  
        - MemoryMemberRepository를 다른 구현체로 변경하고 싶을 경우 MemberRepository()의 리턴값을 변경하면 됨  
        - 단축키 : `ctrl + alt + M` (윈도우)  
       
      - 역할에 따른 구현 파악이 가능하도록 수정  
        - `역할(메소드명)` 과 `구현 클래스(리턴값)` 이 한눈에 보임 
        - 메소드 명을 보면 역할에 따른 구현 파악이 쉬움
        - 애플리케이션 전체 구성이 어떻게 되어있는지 빠르게 파악 가능   

</details>  

### 3-4. 새로운 할인 정책 적용   
<details>
  <summary>자세히</summary>  

#### 현재 구조  
  - 사용 영역 + 구성 영역으로 분리됨  
      ![image](https://user-images.githubusercontent.com/65080004/170415346-a560ef30-296c-422a-a03c-f123567f76d6.png)  
      - 새로운 할인 정책으로 변경한다면 어느 부분을 변경해야 하는가?  
        AppConfig의 DiscountPolicy() 메서드의 구현 부분만 변경해주면 됨  
      - 위와 같이 변경한다면 구성 영역만 영향을 받고, 사용 영역은 영향을 받지 않음  

</details>  

### 3-5. 지금까지의 흐름 정리
<details>
  <summary>자세히</summary>  

#### 새로운 할인 정책 개발 및 적용  
  - 다형성 덕분에 새로운 할인 정책 코드를 추가 개발하는 것 자체는 아무런 문제가 없었음
  - 하지만, 새로운 할인 정책 코드 적용시, `클라이언트 코드`인 주문 서비스 구현체도 변경이 일어남  
    → `OCP 위반`  
  - 주문 서비스가 인터페이스인 DiscountPolicy와 구체 클래스인 FixDiscountPolicy도 함께 의존함  
    → `DIP 위반`  

#### OCP, DIP 원칙을 지키기 위한 방법  
  - 관심사의 분리  
      - 애플리케이션을 하나의 공연으로 생각
      - 기존에는 클라이언트가 의존하는 서버 구현 객체를 직접 생성하고, 실행
      - AppConfig(공연 기획자 역할)를 생성하여 `다양한 책임을 분리`  
      - AppConfig는 애플리케이션의 전체 동작 방식을 구성(config)하기 위해,  
        `구현 객체를 생성하고, 연결하는 책임`을 가짐  
      - 클라이언트 객체는 자신의 역할을 실행하는 것만 집중, 권한이 줄어듦(책임이 명확해짐)  

#### AppConfig 리팩토링
  - 구성 정보에서 역할과 구현을 명확하게 분리
  - 역할이 무엇인지 한눈에 알 수 있음
  - 중복 제거  

#### 새로운 할인 정책 적용
  - 정액 → 정률 할인 정책으로 변경
  - AppConfig를 통해 애플리케이션이 크게 `사용 영역`과, 객체를 생성하고 `구성(Configuration)하는 영역`으로 `분리`  
  - `할인 정책을 변경`해도 AppConfig가 있는 `구성 영역만 변경`하면 됨, `사용 영역은 변경할 필요가 없음`  

</details>

### 3-6. IoC, DI, 그리고 컨테이너
<details>
  <summary>자세히</summary>  

#### IoC (Inversion of Control) - 제어의 역전  
  - `프로그램의 제어 흐름`을 직접 제어하는 것이 아니라 `외부에서 관리`하는 것  
      1. AppConfig 적용 전
         - `구현 객체`가 `프로그램 제어 흐름`을 `스스로 제어`  
           클라이언트 구현 객체가 스스로 필요한 서버 구현 객체를 생성, 연결, 실행함  
      2. AppConfig 적용 후 
         - `구현 객체`는 `자신의 로직을 실행`하는 역할만 담당, `프로그램의 제어 흐름`은 `AppConfig`가 담당함  
           OrderServiceImpl은 필요한 인터페이스를 호출하지만 어떤 구현 객체들이 실행될지 모름  
           왜? 프로그램에 대한 제어 흐름에 대한 권한은 모두 AppConfig가 가지고 있기 때문  
           OrderServiceImpl도 AppConfig가 생성함 (OrderService 인터페이스의 다른 구현 객체를 생성하고 실행 가능) 
  
#### 프레임워크 vs 라이브러리
  - 구분시 중요한 요소는 `제어의 역전`이다!
      1. 프레임 워크  
         - 내가 `제어 흐름을 갖고 있지 않다.`  
         - 내가 작성한 코드를 제어하고 대신 실행  
         - Ex) Junit  
           MemberServiceTest의 @Test join()과 같은 테스트를 실행하고 제어하는 권한은 JUnit 즉, 테스트 프레임워크가 갖고 있음  
      2. 라이브러리  
         - 내가 `제어 흐름을 갖고 있다.`
         - 내가 작성한 코드가 직접 제어의 흐름을 담당  
  
#### DI (Dependency InJection) - 의존관계 주입  
  
  - 의존관계?  
    1. 정적인 클래스 의존관계
    2. 동적인 객체(인스턴스) 의존관계(실행 시점에 결정됨)  
  
    로 분리하여 생각해야 함  
  
  - 정적인 클래스 의존 관계  
      ![image](https://user-images.githubusercontent.com/65080004/170662761-d88ed91f-4104-4bf4-9f7a-fadd9d4c72f5.png)  
      - 클래스가 사용하는 import 코드만 보고 쉽게 판단 가능  
      - 애플리케이션을 실행하지 않아도 분석이 가능  
      ```java
      import hello.core.discount.DiscountPolicy;
      import hello.core.member.Member;
      import hello.core.member.MemberRepository;

      public class OrderServiceImpl implements OrderService {
        ...
      }
      ```
      - 위의 코드에서 OrderServiceImpl 은 MemberRepository , DiscountPolicy 에 의존한다는 것을 알 수 있음  
        그러나 이러한 정적인 클래스 의존관계 만으로는 실제 어떤 객체가 OrderServiceImpl 에 주입 될지 알 수 없음
  
  - 동적인 객체(인스턴스) 의존관계  
      ![image](https://user-images.githubusercontent.com/65080004/170663752-3440c0fe-0489-40b2-85b4-7fa2c68fbb3a.png)  
      - 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계  
  
  - 의존관계 주입  
      - 애플리케이션 `실행 시점(런타임)`에 `외부`에서 `실제 구현 객체를 생성`하고  
        클라이언트에 전달해서 클라이언트와 서버에 `실제의 의존 관계가 연결`되는 것  
      - 객체 인스턴스를 생성하고, 그 참조값을 전달해서 연결됨  
      - 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있음  
      - `정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스 의존관계를 쉽게 변경할 수 있음`  
  
#### `IoC 컨테이너 (DI 컨테이너)`  
  - AppConfig 처럼 `객체를 생성하고 관리`하면서 `의존관계를 연결`해 주는 것  
  - 의존관계 주입에 초점을 맞추어 최근에는 주로 DI 컨테이너라 함  
  - 또는 어샘블러, 오브젝트 팩토리 등으로 불리기도 함  
  
</details>  
  
### 3-7. 스프링으로 전환하기
<details>
  <summary>자세히</summary>  

#### 순수 자바 코드 → 스프링  
  1. AppConfig 클래스 수정  
     ```java
     package hello.core;

       ...
       import org.springframework.context.annotation.Bean;
       import org.springframework.context.annotation.Configuration;

       @Configuration
       public class AppConfig {
          
         @Bean
         public MemberService memberService() {
           return new MemberServiceImpl(memberRepository());
         }
         
         @Bean
         public MemberRepository memberRepository() {
           return new MemoryMemberRepository();
         }

         @Bean
         public OrderService orderService() {
           return new OrderServiceImpl(memberRepository(), discountPolicy());
         }

         @Bean
         public DiscountPolicy discountPolicy() {
           return new RateDiscountPolicy();
         }
     }
     ```  
     - 기존 private 접근자를 사용하던 메서드 public으로 변경  
       
     - @Configuration: 어플리케이션 설정(구성) 정보를 만들기 위한 어노테이션  
       스프링 컨테이너가 해당 어노테이션이 붙은 클래스를 구성 정보로 사용함   
       
     - @Bean: 스프링 빈으로 등록  
       구성 정보 클래스에서 해당 어노테이션이 붙은 메서드를 모두 호출하여 반환된 객체를 `스프링 컨테이너에 등록함`  
       등록된 객체를 `스프링 빈` 이라고함  
  
  2. MemberApp, OrderApp 수정  
     - MemberApp & OrderApp  
         ```java
         public class MemberApp {

           public static void main(String[] args) {
             ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
             MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
             ...
           }
         }
         
         public class OrderApp {

           public static void main(String[] args) {
             ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
             MemberService memberService = applicationContext.getBean("memberService", MemberService.class);
             OrderService orderService = applicationContext.getBean("orderService", OrderService.class);
             ...
           }
         }
         ```
         - ApplicationContext : `스프링 컨테이너`  
           ApplicaionContext가 AppConfig에 있는 환경설정 정보를 갖고 @Bean으로 등록된 객체들을 관리  
         - applicationContext.getBean(빈 이름, 객체 타입.class) : 스프링 컨테이너에서 해당 조건의 스프링 빈을 조회  
           
  - 스프링 컨테이너  
    - `ApplicationContext` = 스프링 컨테이너  
      스프링 빈을 생성하고 관리하는 컨테이너  
    - `@Configuration` 이 붙은 AppConfig 를 설정(구성) 정보로 사용,  
      설정 정보에서 `@Bean` 이 적용된 메서드를 모두 호출하여 반환된 객체를 스프링 컨테이너에 등록함  
      스프링 컨테이너에 등록된 객체를 `스프링 빈`이라고 함  
    - 스프링 빈은 @Bean 이 붙은 메서드의 명을 스프링 빈의 이름으로 사용(기본값 default)  
    - 스프링 컨테이너를 통해서 필요한 스프링 빈(객체)를 조회함  
      `applicationContext.getBean(빈 이름, 객체 타입.class)` 메서드를 사용하면 됨  
  
  - 정리  
    - 기존 : 직접 자바코드로 모든 것(객체 생성, DI 등)을 했음  
    - 수정 : `스프링 컨테이너`에 `객체를 스프링 빈으로 등록`하고,  
            스프링 컨테이너에서 `스프링 빈을 찾아서 사용`하도록 변경  
      
    - 이렇게 스프링 컨테이너를 사용하면 뭐가 좋은지는 다음 시간에 설명   
  
</details>	

### 4. 스프링 컨테이너와 스프링 빈  
### 4-1. 스프링 컨테이너   
<details>
  <summary>자세히</summary>  

#### 스프링 컨테이너  
  ```java
  ApplicaionContext applicationContext = 
		new AnnotationConfigApplicaionContext(AppConfig.class);
  ```  
  - `ApplicationContext` = `스프링 컨테이너` 라고 함  
      > 참고  
      > 더 정확히는 스프링 컨테이너를 부를 때 `BeanFactory` , `ApplicationContext` 로 구분해서 이야기 함  
      > 하지만 BeanFactory 를 직접 사용하는 경우는 거의 없으므로 일반적으로 ApplicationContext 를 스프링 컨테이너라 함  
  
  - `ApplicationContext`는 인터페이스  
    `AnnotationConfigApplicaionContext`는? ApplicationContext 구현체
  - 생성 방법  
    1. XML을 기반으로 생성  
    2. 어노테이션 기반의 자바 설정 클래스로 생성  
       - 예시  
         1. new AnnotationConfigApplicationContext(AppConfig.class);  
         2. 매개변수로 AppConfig class를 넣어줌  
         3. 해당 클래스는 ApplicationContext 인터페이스의 구현체  
         
#### 스프링 컨테이너 생성 과정 
  1. 스프링 컨테이너 생성  
       ![image](https://user-images.githubusercontent.com/65080004/170874573-c113e5a1-c481-45dc-ab17-a11831f56761.png)  
       - `구성 정보`를 기재하고, 해당 `구현체`를 이용해 `스프링 컨테이너`를 생성  
         - `new AnnotationConfigApplicationContext(AppConfig.class)`  
           스프링 컨테이너 생성할 때는 구성 정보를 파라미터 값으로 넘겨주어야 함  
         - 구성 정보 : 여기서는 `AppConfig.class`  
         - 구현체 : ApplicationContext 인터페이스의 구현체인 `AnnotationConfigApplicationContext`  
  2. 스프링 빈 등록  
       ![image](https://user-images.githubusercontent.com/65080004/170874352-8aa6c2c0-1754-4070-9194-045751437d3d.png)  
       - 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록함  
       - 빈이름  
         - 기본적으로 메서드 이름을 사용하고, 아래와 같이 어노테이션 옵션을 통해 빈 이름을 직접 부여 가능  
           `@Bean(name="member")`  
         - 주의  
           `빈 이름은 항상 다른 이름을 부여해야 함`  
           왜? 같은 이름을 부여하게 되면 다른 빈이 무시되거나, 기존 빈을 덮어버리는 등 설정에 따로 오류가 발생할 수 있어서  
  3. 스프링 빈 의존관계 설정 - 준비  
       ![image](https://user-images.githubusercontent.com/65080004/170874326-fb9768dd-4e3b-4e90-a7f4-ee230082a03c.png)  
  4. 스프링 빈 의존관계 설정 - 완료  
       ![image](https://user-images.githubusercontent.com/65080004/170874260-783f4687-de5e-4667-8376-79030b6f91e1.png)  
       - 스프링 컨테이너는 설정 정보를 참고해서 의존 관계를 주입(DI)함  
         단순히 자바 코드를 호출하는 것 같지만 차이가 있음, 이는 추후 설명 예정  
  - 참고  
      - 스프링은 `빈을 생성`하고, `의존관계를 주입`하는 `단계가 나누어져 있음`  
        그런데 예제처럼 `자바코드로 스프링 빈을 등록`하면 `생성자를 호출하면서 의존관계 주입도 한번에 처리`된다  
        위의 1 ~ 4 과정은 이해하기 쉽게 나누어 설명한 것  
  - 생성 과정 정리  
      1. 스프링 컨테이너 생성  
      2. 구성(설정) 정보(AppConfig)를 참고하여 스프링 빈 등록  
      3. 의존관계 설정  
  
</details>
  
### 4-2. 스프링 컨테이너에 등록된 빈 조회   
<details>
  <summary>자세히</summary>  

#### 컨테이너에 등록된 모든 빈 조회 테스트 코드  
  - 컨테이너에 실제 스프링 빈들이 잘 등록 되었는지 확인하기 위해 ApplicationContextInfoTest 작성  
      - 컨테이너에 등록된 모든 빈 출력하기  
        ```java
        public class ApplicationContextInfoTest {

          AnnotationConfigApplicationContext ac 
              = new AnnotationConfigApplicationContext(AppConfig.class);

          @Test
          @DisplayName("컨테이너에 등록된 모든 빈 출력하기")
          void findAllBean() {
              String[] beanDefinitionNames = ac.getBeanDefinitionNames();
              for (String beanDefinitionName : beanDefinitionNames) {
                  Object bean = ac.getBean(beanDefinitionName);
                  System.out.println("beanDefinitionName = " + beanDefinitionName + ", object = " + bean);
              }
          }
          ...
        }
        ``` 
        - 테스트 실행시 스프링에 등록된 모든 빈 정보를 출력할 수 있음  
        - ac.getBeanDefinitionNames() : 스프링에 등록된 모든 빈 이름을 String 배열로 리턴  
        - ac.getBean(빈 이름) : 빈 이름(String Type)으로 빈 객체(인스턴스)를 조회  
    
    - 애플리케이션 빈 출력하기  
      ```java
      public class ApplicationContextInfoTest {
        ...
        @Test
        @DisplayName("애플리케이션 빈 출력하기")
        void findApplicationBean() {
          
          String[] beanDefinitionNames = ac.getBeanDefinitionNames();
            
          for (String beanDefinitionName : beanDefinitionNames) {
          
            BeanDefinition beanDefinition = ac.getBeanDefinition(beanDefinitionName);
            
            if (beanDefinition.getRole() == BeanDefinition.ROLE_APPLICATION) {
                Object bean = ac.getBean(beanDefinitionName);
                System.out.println("beanDefinitionName = " + beanDefinitionName + ", object = " + bean);
            }
          }
        }
        ...
      }  
      ```
      - 스프링이 내부에서 사용하는 빈을 제외하고, 내가 등록한 빈만 출력  
      - ac.getBeanDefinition(빈이름) : 해당 빈이름에 해당하는 빈에 대한 meta 정보를 얻음  
      - `beanDefinition.getRole()` 로 스프링이 내부에서 사용하는 빈 구분  
        ROLE_APPLICATION : 일반적으로 사용자가 정의한 빈  
        ROLE_INFRASTRUCTURE : 스프링이 내부에서 사용하는 빈  

</details>

### 4-3. 스프링 빈 조회 - 기본   
<details>
  <summary>자세히</summary>  

#### 가장 기본적인 조회 방법  
  1. ac.getBean(빈 이름, 빈 타입) : `빈 이름 & 빈 타입(인터페이스 또는 수퍼 클래스)`으로 빈 조회  
  2. ac.getBean(빈 타입) : `빈 타입`으로만 빈 조회  
  3. ac.getBean(빈 이름) : `빈 이름`으로 빈 조회(리턴시 Object 타입)  
  - 조회 대상 스프링 빈이 없으면 `NoSuchBeanDefinitionException` 예외 발생  

#### 예제 코드  
  ```java
  public class ApplicationContextBasicFindTest {

    AnnotationConfigApplicationContext ac 
      = new AnnotationConfigApplicationContext(AppConfig.class);
    ...
  
  }    
  ```

  - findBeanByNameAndType : 빈 이름 & 빈 타입으로 빈 조회
      ```java
      @Test
      @DisplayName("빈 이름과 타입으로 조회하기")
      void findBeanByNameAndType() {
          MemberService memberService =
                  ac.getBean("memberService", MemberService.class);

          assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
      }
      ```  
      - 빈 이름이 `memberService`이고, 빈 타입이 `MemberService.class` 인 빈을 조회  
      - 조회한 빈의 인스턴스 타입이 MemberServiceImpl이 맞는지 검증  

  - findBeanByType : 빈 타입으로 빈 조회
      ```java  
      @Test
      @DisplayName("빈 타입으로 조회하기")
      void findBeanByType() {
          MemberService memberService =
                  ac.getBean(MemberService.class);

          assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
      }
      ```  
      - 빈 타입이 `MemberService.class` 인 빈을 조회  
      - 조회한 빈의 인스턴스 타입이 MemberServiceImpl이 맞는지 검증  

  - findBeanByDetailType : 빈 이름 & 빈 구체 타입으로 빈 조회 
      ```java
      @Test
      @DisplayName("빈 구체 타입으로 조회하기")
      void findBeanByDetailType() {
          MemberService memberService =
                  ac.getBean("memberService", MemberServiceImpl.class);

          assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
      }  
      ```
      - 빈 이름이 `memberService`이고, 빈 타입이 `MemberServiceImpl.class` 인 빈을 조회  
      - 조회한 빈의 인스턴스 타입이 MemberServiceImpl이 맞는지 검증  
      - 구체 타입으로 조회가 가능하지만, `다형성을 사용하는 추상타입으로 조회하는 것을 권장`  
  
  - findBeanFail : 빈 이름과 빈 타입으로 빈 조회시 조회되지 않는 경우  
      ```java
      @Test
      @DisplayName("빈 이름과 타입으로 조회시 실패")
      void findBeanFail() {
          assertThrows(NoSuchBeanDefinitionException.class,
                  () -> ac.getBean("foo", MemberService.class));
      }
      ```
      - 빈 조회가 실패하는 경우도 테스트하는 것이 좋음  
      - 빈 이름이 `foo`이고, 빈 타입이 `MemberService.class` 인 빈을 조회  
      - 조회된 빈이 없으므로 `NoSuchBeanDefinitionException` 예외를 발생시키는지 검증  

</details>

### 4-4. 스프링 빈 조회 - 동일 타입이 둘 이상   
<details>
  <summary>자세히</summary>  

#### 동일 타입이 둘 이상인 스프링 빈 조회
  - ac.getBean(빈 타입)으로 조회시, 같은 타입의 스프링 빈이 둘 이상인 경우 `NoUniqueBeanDefinitionException` 발생  
  - Exception 해결 방법  
    1. `ac.getBean(빈 이름, 빈 타입)` 으로 `1개의 빈 조회`  
    2. `ac.getBeansOfType()` 으로 `해당 타입의 모든 빈을 조회`  

#### 예제 코드  
  ```java
  public class ApplicationContextSameBeanFindTest {

    AnnotationConfigApplicationContext ac 
      = new AnnotationConfigApplicationContext(SameBeanConfig.class);
    
    ...
  
  }    
  ```
  
  - SameBeanConfig : 설정 정보 클래스  
      - 테스트 내에서만 사용하기 위해 만들 클래스이므로, static으로 선언  
      - [static class 참고](https://johngrib.github.io/wiki/java-inner-class-may-be-static/)  

  - findBeanByTypeDuplicate : 빈 타입으로 빈 조회시 같은 타입이 둘 이상 존재할 경우 중복 오류가 발생  
      ```java
      @Test
      @DisplayName("타입으로 빈 조회시 같은 타입이 둘 이상 존재시, 중복 오류 발생")
      void findBeanByTypeDuplicate() {
          assertThrows(NoUniqueBeanDefinitionException.class,
                  () -> ac.getBean(MemberRepository.class));
      }
      ```
      - MemberRepository 타입인 빈을 조회  
      - MemberRepository 타입인 빈이 2개이므로 NoUniqueBeanDefinitionException 발생  

  - findBeanByTypeAddName : 같은 타입이 2개 이상이어도 타입과 이름을 조건으로 설정하여 검색하면 조회 성공  
      ```java
      @Test
      @DisplayName("타입으로 빈 조회시 같은 타입이 둘 이상 존재시, 빈 이름을 지정하면 오류 발생 안함")
      void findBeanByTypeAddName() {
          MemberRepository memberRepository =
                  ac.getBean("memberRepository1", MemberRepository.class);
          assertThat(memberRepository).isInstanceOf(MemberRepository.class);
      }
      ```  
      - 빈 이름이 memberRepository1이고, MemberRepository 타입인 빈을 조회  
      - 조회된 빈의 객체 타입이 memberRepository 인지 검증  

  - findAllBeanByType : 특정 타입을 가진 모든 빈 조회
      ```java 
      @Test
      @DisplayName("특정 타입의 빈 모두 조회하기")
      void findAllBeanByType() {
          Map<String, MemberRepository> beansOfType =
                  ac.getBeansOfType(MemberRepository.class);

          for(String beanName : beansOfType.keySet()) {
              System.out.println("key = " + beanName + " value = " + beansOfType.get(beanName));
          }

          assertThat(beansOfType.size()).isEqualTo(2);
      }
      ```
      - `ac.getBeansOfType(타입)`을 사용하여 MemberRepository타입인 모든 빈을 조회  
      - Map으로 반환된 모든 빈의 개수가 2개가 맞는지 검증  

</details>

### 4-5. 스프링 빈 조회 - 상속관계  
<details>
  <summary>자세히</summary>  

#### 상속관계인 스프링 빈 조회
  - `부모 타입을 조회`하면 `자식 타입도 함께 조회`됨!  
    Ex) Object 타입으로 조회하면?  
    Object는 모든 자바 객체의 최상위 클래스 이므로 `모든 스프링 빈이 조회`됨  

#### 예제 코드  
  ```java
  public class ApplicationContextExtendsFindTest {

    AnnotationConfigApplicationContext ac 
      = new AnnotationConfigApplicationContext(TestConfig.class);
    
    ...
  
  }    
  ```

  - TestConfig : 설정 정보 클래스  
      - 테스트 내에서만 사용하기 위해 만들 클래스이므로, static으로 선언  

  - findBeanByParentTypeWithTwoChildType : 부모 타입으로 조회시, 자식이 둘 이상인 경우 중복 오류가 발생  
      ```java
      @Test
      @DisplayName("부모 타입으로 조회시, 자식 타입이 둘 이상 존재할 경우 중복 오류 발생 테스트")
      void findBeanByParentTypeWithTwoChildType() {
          assertThrows(NoUniqueBeanDefinitionException.class,
                  () -> ac.getBean(DiscountPolicy.class));
      }
      ```    
      - DiscountPolicy 타입인 빈을 조회  
      - 부모 타입이 DiscountPolicy 인 빈이 2개이므로 NoUniqueBeanDefinitionException 발생   

  - findBeanByParentTypeAndNameWithTwoChildType : 부모 타입과 빈 이름으로 조회시, 자식이 둘 이상인 경우에도 오류 발생하지 않음  
      ```java
      @Test
      @DisplayName("부모 타입으로 조회시, 자식 타입이 둘 이상 존재할 경우 오류가 발생하지 않도록 빈 이름 지정")
      void findBeanByParentTypeAndNameWithTwoChildType() {
          DiscountPolicy rateDiscountPolicy =
                  ac.getBean("rateDiscountPolicy", DiscountPolicy.class);

          assertThat(rateDiscountPolicy).isInstanceOf(RateDiscountPolicy.class);
      }
      ```    
      - 빈 이름이 rateDiscountPolicy이고, DiscountPolicy 타입인 빈을 조회  
      - 조회한 빈의 객체 타입이 RateDiscountPolicy 인지 검증  

  - findBeanBySubType : 특정 하위 타입으로 조회
      ```java
      @Test
      @DisplayName("특정 하위 타입으로 조회 - 좋지 않은 방법임")
      void findBeanBySubType() {
          RateDiscountPolicy bean = ac.getBean(RateDiscountPolicy.class);
          assertThat(bean).isInstanceOf(RateDiscountPolicy.class);
      }
      ```
      - RateDiscountPolicy 타입인 빈을 조회  
      - 조회한 빈의 객체 타입이 RateDiscountPolicy 인지 검증  
      - `특정 하위 타입으로 조회하는 것은 좋지 않은 방식`  

  - findAllBeanByParentType : 부모 타입으로 `부모타입 + 하위 타입의 빈` 조회 
      ```java
      @Test
      @DisplayName("부모 타입으로 모든 빈 조회")
      void findAllBeanByParentType() {

          Map<String, DiscountPolicy> beansOfType =
                  ac.getBeansOfType(DiscountPolicy.class);

          for(String key : beansOfType.keySet()) {
              System.out.println("key : " + key + " value : " + beansOfType.get(key));
          }

          assertThat(beansOfType.size()).isEqualTo(2);
      }
      ```  
      - `ac.getBeansOfType(부모타입)`을 사용하여 DiscountPolicy타입인 모든 빈을 조회  
      - Map으로 반환된 모든 빈의 개수가 2개가 맞는지 검증  

  - findAllObjectBeanByParentType : Object 타입으로 모든 빈 조회
      ```java
      @Test
      @DisplayName("Object(부모) 타입의 모든 빈을 조회")
      void findAllObjectBeanByParentType() {

          Map<String, Object> beansOfType = ac.getBeansOfType(Object.class);

          for(String key : beansOfType.keySet()) {
              System.out.println("key : " + key + " value : " + beansOfType.get(key));
          }
      }
      ```
      - `ac.getBeansOfType(Object)`을 사용하여 모든 빈을 조회  
      - Object는 최상위 클래스이므로 모든 빈이 조회됨  
      - Map으로 반환된 모든 빈 정보 출력   

#### 스프링 빈 조회 내용 정리
  1. 스프링 빈 이름 조회  
       - getBeanDefinitionNames() : ApplicationContext(스프링 컨테이너)에 등록된 모든 스프링 빈 이름 조회  

  2. 스프링 빈 객체 조회
       -  `부모 타입으로 조회`하면 `자식 타입까지 조회 됨!`  
       - 구체 타입으로 조회하는 것은 변경시 유연성이 떨어지므로 좋지 않은 방식  
       - Object 타입으로 조회하면 모든 스프링 빈이 조회 됨  
       - getBean(타입) : ApplicationContext(스프링 컨테이너)에 등록된 해당 타입의 스프링 빈 객체 조회  
         - NoSuchBeanDefinitionException : 조회 대상이 스프링 빈이 없을 경우 발생하는 예외  
         - NoUniqueBeanDefinitionException : 같은 타입의 스프링 빈이 2개 이상일 경우 발생하는 중복 예외  
       - getBean(빈 이름, 타입) : ApplicationContext(스프링 컨테이너)에 등록된 (빈 이름, 타입)의 스프링 빈 객체 조회  
         - NoSuchBeanDefinitionException : 조회 대상이 스프링 빈이 없을 경우 발생하는 예외  
         - 동일한 타입이 2개 이상이거나 부모 타입의 자식 타입이 2개 이상일 때, 빈 이름으로 조회해야 중복 예외를 막을 수 있음  
       - getBeansOfType(타입) : ApplicationContext(스프링 컨테이너)에 등록된 해당 타입의 모든 스프링 빈 객체 조회  
  
  3. 지금까지 해당 기능을 공부한 이유
       - 실제 개발할 때는 ApplicationContext에서 스프링 빈을 조회할 일은 거의 없음  
       - 하지만, 
       1) 스프링 빈 조회는 `기본기능`
       2) 순수 자바 어플리케이션에서 스프링 컨테이너를 생성해서 사용해야 하는 경우,  
       사용할 수 있음  
       3) `부모 타입으로 조회시 어디까지 조회가 되는 것인지에 대한 이해`가 있어야  
            `자동 의존 관계 주입`에 대해 문제없이 잘 해결 할 수 있기 때문  

</details>

### 4-6. BeanFactory와 ApplicationContext  
<details>
  <summary>자세히</summary>  

#### BeanFactory와 ApplicationContext 관계
   ![image](https://user-images.githubusercontent.com/65080004/172099625-ddf3ca50-2a66-474f-92ba-592b5905a458.png)  
   - BeanFactory  
       - 스프링 컨테이너의 최상위 인터페이스
       - 스프링 빈을 관리하고 조회하는 역할 담당
       - getBean() 메서드 제공
       - 앞서 사용했던 대부분의 기능은 해당 인터페이스가 제공하는 기능임

   - ApplicationContext
       - BeanFactory 기능을 모두 상속받아서 제공함  
       - 빈을 관리하고 검색하는 기능을 BeanFactory가 제공해주는데,  
         그렇다면 둘의 차이가 뭘까?  
       - 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능 뿐만 아니라,  
         수 많은 부가기능이 필요함  
       - 추가적으로 제공하는 부가 기능은 무엇이 있는가? 
   
   - ApplicationContext가 제공하는 부가 기능  
       - ApplicationContext의 관계  
         ![image](https://user-images.githubusercontent.com/65080004/172100100-d57ce6da-6ea9-4bcf-9fbe-43b136c6a0d9.png)  
         - 메세지소스를 활용한 국제화 기능  
           - Ex) 접속 지역에 따른 언어로 변경, 한국에서 들어올 경우 한국어로 출력
         - 환경변수  
           - 로컬, 개발, 운영등을 구분하여 처리  
         - 애플리케이션 이벤트  
           - 이벤트를 발행하고 구독하는 모델을 편리하게 지원  
         - 편리한 리소스 조회  
           - 파일, 클래스패스, 외부 등에서 리소스를 편리하게 조회 

   - BeanFactory와 ApplicationContext 정리  
       - ApplicationContext는 BeanFactory의 기능을 상속 받음  
       - ApplicationContext는 `빈 관리기능 + 편리한 부가 기능을 제공`  
       - BeanFactory를 직접 사용할 일은 거의 없음  
         주로 부가기능이 포함된 ApplicationContext를 사용  
       - BeanFactory나 ApplicationContext를 스프링 컨테이너라고 함   

</details>  

***
[목록으로](https://github.com/youngho-j/TIL/blob/main/Spring/README.md)  
