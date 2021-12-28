# Lombok 

## 목차
1. [Lombok이란?](#1-lombokd이란)   
1-1. [장점](#1-1-장점)  
2. [Lombok 기능 및 예제](#2-lombok-기능-및-예제)  
2-1. [@Getter, @Setter](#2-1-getter-setter)   

참조 : [Reference](#reference)  
***

### 1. Lombok이란?
  - `어노테이션 기반으로 코드를 자동완성 해주는 라이브러리`  

#### 1-1. 장점
  ```
  - 어노테이션 기반의 코드 자동 생성을 통한 생산성 향상
  
  - 반복되는 코드를 줄여 가독성 및 유지보수성 향상
  
  - Getter, Setter 외에 빌더 패턴이나 로그 생성 등 다양한 방면으로 활용 가능
  ```
  
### 2. Lombok 기능 및 예제
#### 2-1. @Getter, @Setter
  - @Getter 객체 외부에서 객체의 데이터를 읽어오는 메서드 생성  
    ```
    '필드 값을 리턴하는 것'
    필드 이름이 foo이고, 필드 타입이 boolean이 아닌 경우 메소드 이름은 getFoo
    필드 이름이 foo이고, 필드 타입이 boolean인 경우 isFoo
    ```
    
  - @Setter 객체 외부에서 객체의 데이터에 접근할 수 있도록 하는 메서드 생성  
    ```
    '필드 값을 설정해주는 것'
    필드 이름이 foo인경우 void 리턴타입에 필드와 같은 파라미터를 가진 setFoo 라는 이름을 가진 메서드가 됨
    ```
  
  - 클래스에 적용시키는 경우 해당 클래스의 static이 아닌 모든 변수에서 getter 사용 가능
    ```java
    
    // Lombok 적용 
    @Getter
    public class People {
      private String name;
      private int age;
      private static birthday;
    }
    
    // People 객체 생성 후 name, age를 가져올 수 있는 getter 메서드 사용 가능 
    People people = new People();
    
    String name = people.getName();
    int age = people.getAge();
    ```
  
  - 멤버 변수에 적용시키는 경우 해당 변수만 사용가능
    ```
    
    // Lombok 적용
    public class People {
      private String name;
      @Setter
      private ing age;
    }
    
    // People 객체 생성 후 age 데이터에 접근할 수 있는 setter 메서드 사용 가능
    People people = new People();
    
    people.setAge(10);
    ```
    
  - 접근 제한자 설정 가능  
  
    |제한자 이름|설명|
    |:---:|:---:|
    |AccessLevel.PACKAGE	| package 한정자|
    |AccessLevel.PUBLIC	| public 한정자 (기본값)|
    |AccessLevel.PRIVATE	| private 한정자|
    |AccessLevel.PROTECTED	| protected 한정자|
    |AccessLevel.NONE	 | 해당 필드의 메소드 생성하지 않음|
      
    ```java
    
    // Lombok
    public class TestLombok {
      
      private String testCode1;
      
      @Getter(AccessLevel.NONE)
      private String testCode2;
      
      private static String testCode3;
    }  
    
    // 실제 적용된 자바 코드
    public class TestLombok {
      
      private String testCode1;
      private String testCode2;
      private static String testCode3;
      
      public TestLombok() {}
      
      public String getTestCode1() {
        return this.testCode1;
      }
    }
    ```
    
## Reference
 - [망나니개발자 Lombok이란? 및 Lombok 활용법](https://mangkyu.tistory.com/78)    
 - [딩규의 개발 블로그 Lombok 기능 정리](https://dingue.tistory.com/14)    
 - [live2skull 커피와 코딩사이 자바 -Lombok](https://blog.live2skull.kr/java/lombok/java-lombok/#2-equalsandhashcode%EB%A5%BC-%ED%95%A8%EB%B6%80%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4)  
 - [Lombok features](https://projectlombok.org/features/all)    
 - 
***
[목록으로](https://github.com/youngho-j/TIL/blob/main/Library/README.md)
