# Lombok 

## 목차
1. [Lombok이란?](#1-lombokd이란)   
1-1. [장점](#1-1-장점)  
2. [Lombok 기능 및 예제](#2-lombok-기능-및-예제)  
2-1. [@Getter, @Setter](#2-1-getter-setter)   
2-2. [@EqualsAndHashCode](#2-2-equalsandhashcode)  

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
  
  - 필드 내 변수에 적용시키는 경우 해당 변수만 사용가능
    ```java
    
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

#### 2-2. @EqualsAndHashCode
  
  - non-static and non-transient fields에 equals, hashCode 메서드를 자동으로 생성
    
    참고. transient : Serialize(직렬화)하는 과정에 제외하고 싶은 경우 선언하는 키워드  
          Ex) private transient String name;  
          // 직렬화시 name이 직렬화 대상에서 제외(field는 유지)하여 직렬화 하기때문에 역직렬화 결과는 null로 대입  
  
  - equals, hashCode?
    ```
    - equals : 두 객체의 내용이 같은지, 동등성(equality)을 비교하는 연산자
    
    - hashCode : 두 객체가 같은 객체인지, 동일성(identity)을 비교하는 연산자
    ```
  
  - equals 예시
    ```java
    @Test
    public void 같은_값인_경우_equals_테스트() {

      LombokTest test = new LombokTest("1", "2");
      LombokTest test2 = new LombokTest("1", "2");

      assertTrue(test.equals(test2)); // 결과 : true
    }

    @Test
    public void 다른_값인_경우_equals_테스트() throws Exception {

      LombokTest test = new LombokTest("1", "3");
      LombokTest test2 = new LombokTest("1", "2");

      assertFalse(test.equals(test2)); // 결과 : false
    }
    ```
    
  - HashCode 예시
    ```java
    @Test
    public void 같은_필드_값을_갖는_객체인_경우_hashCode_테스트() throws Exception {
      LombokTest test = new LombokTest("1", "2");
      LombokTest test2 = new LombokTest("1", "2");

      System.out.println("test : " + test.hashCode());   // hashCode : 6422
      System.out.println("test2 : " + test2.hashCode()); // hashCode : 6422

      assertEquals(test.hashCode(), test2.hashCode());
    }

    @Test
    public void 다른_필드_값을_갖는_객체인_경우_hashCode_테스트() throws Exception {
      LombokTest test = new LombokTest("1", "2");  
      LombokTest test2 = new LombokTest("1", "3");

      System.out.println("test : " + test.hashCode());   // hashCode : 6422
      System.out.println("test2 : " + test2.hashCode()); // hashCode : 6423

      assertNotEquals(test.hashCode(), test2.hashCode());
    }

    @Test
    public void 객체의_필드값을_변경한_경우_hashCode_테스트() throws Exception {
      LombokTest test = new LombokTest("1", "2");  

      System.out.println("test : " + test.hashCode());   // hashCode : 6422

      Set<LombokTest> list = new HashSet<>();

      list.add(test);
      System.out.println("변경 전 : " + list.contains(test)); // true
      // 참고 - Set class contain 메서드 : 특정 요소를 보관하였는지 판단하는 메서드 
      assertTrue(list.contains(test));

      test.setTest1("3");
      System.out.println("test : " + test.hashCode()); // hashCode : 6540
      System.out.println("변경 후 : " + list.contains(test)); // false
      assertFalse(list.contains(test));

    }

    @Test
    public void 객체의_필드값을_변경한_경우_hashCode_테스트2() throws Exception {
      LombokTest test = new LombokTest("1", "한글");  
      System.out.println("변경전 test : " + test.hashCode());   // hashCode : 1744136

      LombokTest test2 = new LombokTest("1", "한글3");  
      System.out.println("변경전 test2 : " + test2.hashCode()); // hashCode : 53877107

      test.setTest2("한글4");
      System.out.println("변경후 test : " + test.hashCode());   // hashCode : 53877108

      test2.setTest2("한글4");
      System.out.println("변경후 test2 : " + test2.hashCode()); // hashCode : 53877108

      assertEquals(test.hashCode(), test2.hashCode());
    }
    ```
  - 속성  
    ** of, exclude 속성 보다는 @EqualsAndHashCode(onlyExplicitlyIncluded = true)를 적용하여 각 필드별로 적용하는게 좋음  
       (앞의 두속성은 deprecated 예정)  
       
    `callSuper`
    ```java
    Class Level
     - @EqualsAndHashCode(callSuper = true) : 부모 클래스의 필드까지 포함

       // 예시
       @EqualsAndHashCode(callSuper = true)
       public class Employee extends Citizen {

          private String name;
          private int salary;
       }
    
     - @EqualsAndHashCode(callSuper = false) : 기본값(callSuper = false 작성하지 않아도 적용됨), 자신의 필드 값들만 포함
    ```
    
    `exclude`  
    ```java 
    ** Class, Field 어느 방법을 사용하던 결과는 유사함
    
    Class Level
     - @EqualsAndHashCode(exclude = "파라미터명") : 해당 파라미터를 제외
     
     - @EqualsAndHashCode(exclude = {"파라미터명1", 파라미터명2}) : 지정된 파라미터들을 제외
       
       // 예시
       @EqualsAndHashCode(exclude = {"age", "salary"})
       public class Employee {

         private String name; // name에 대한 Eqauls, HashCode 메서드 생성
         
         private int age;
         
         private int salary;
       }
       
    Field Level
     - @EqualsAndHashCode.Exclude
       private int age
       참고. 클래스에 @EqualsAndHashCode 적용 후 클래스 내 필드 위에 @EqualsAndHashCode.Exclude를 적용해야함
       
       // 예시
       @EqualsAndHashCode
       public class Employee {
          private String name;
          
          @EqualsAndHashCode.Exclude
          private int age;
          
          @EqualsAndHashCode.Exclude
          private int salary;
       }
    ```
    
    `include`  
    ```java
    Field Level
     - @EqualsAndHashCode.Include  
       private String name;
       참고. 클래스에 @EqualsAndHashCode(onlyExplicitlyIncluded = true) 적용 후 클래스 내 필드 위에 @EqualsAndHashCode.Include를 적용해야함  
             이 경우 @EqualsAndHashCode.Include 가 적용된 필드 값에 대한 eqauls, hashCode 메서드 생성
             
       // 예시
       @EqualsAndHashCode(onlyExplicitlyIncluded = true)
       public class Employee {

          @EqualsAndHashCode.Include
          private String name;
       
          @EqualsAndHashCode.Include
          private int age;
          
          private int salary;
        } //name, age 필드에 대한 equals, hashCode 메서드 생성
        
    Method Level
     - @EqualsAndHashCode.Include  
       public boolean canDrink() {
         return age > 18;
       }
       참고. 클래스 내 메서드 위에 @EqualsAndHashCode.Include를 적용해야함  
             기존 JavaBean style의 getter 메서드가 아니며, 지원 프로퍼티가 존재하지 않음  
             ** 지원 프로퍼티? 클래스의 필드와 접근자 메서드(getter/setter)가 맞는지 추후 알아볼것.. 
       
       // 예시
       @EqualsAndHashCode
       public class Employee {

          private String name;
          private int age;
          private int salary;

          @EqualsAndHashCode.Include
          public boolean canDrink() {
              return age > 18;
          }
       } // 전체 필드 값과 메서드에 대한 equals, hashCode 메서드 생성
       
    Class Level
     - @EqualsAndHashCode(of = "파라미터")
     
     - @EqualsAndHashCode(of = {"파라미터", "파라미터1"})
       
       // 예시  
       @EqualsAndHashCode(of = {"name", "age"})
       public class Employee {

          private String name;
          private int age;
          private int salary;
       } // name, age 필드에 대한 equals, hashCode 메서드 생성
       
       참고. 기능은 @EqualsAndHashCode(onlyExplicitlyIncluded = true)과 유사함, 추후 deprecated 예정  
    ```
## Reference
 - [망나니개발자 Lombok이란? 및 Lombok 활용법](https://mangkyu.tistory.com/78)    
 - [딩규의 개발 블로그 Lombok 기능 정리](https://dingue.tistory.com/14)    
 - [live2skull 커피와 코딩사이 자바 -Lombok](https://blog.live2skull.kr/java/lombok/java-lombok/#2-equalsandhashcode%EB%A5%BC-%ED%95%A8%EB%B6%80%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EC%A7%80-%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4)  
 - [Lombok features](https://projectlombok.org/features/all)    
 - [seek 블로그 프로젝트롬복_@EqualsAndHashCode](https://blog.naver.com/PostView.nhn?blogId=dktmrorl&logNo=222359154544&categoryNo=0&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)  
 - [기록하는 동구 Lombok 자주쓰이는 어노테이션](https://donggu1105.tistory.com/99)  
 - [날아올라 Lombok 사용상 주의점](https://javaengine.tistory.com/entry/Lombok-%EC%82%AC%EC%9A%A9%EC%83%81-%EC%A3%BC%EC%9D%98%EC%A0%90Pitfall)  
 - [Java By Examples EqaulsAndHashCode](http://www.javabyexamples.com/delombok-equalsandhashcode)  
 - [](https://javabydeveloper.com/lombok-equalsandhashcode-examples/#6-41-include-fieldsmethods-)  
 - [Nesoy Blog Java transient이란?](https://nesoy.github.io/articles/2018-06/Java-transient)  
 - [디빌리 Kotlin 기초강의#5-2 자바의 프로퍼티](https://manorgass.tistory.com/80)  
***

[목록으로](https://github.com/youngho-j/TIL/blob/main/Library/README.md)
