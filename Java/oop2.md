# 객체지향개념2
## 목차

1. [상속](#1-상속)   
1-1. [상속이란?](#1-1-상속이란)  
1-2. [상속관계](#1-2-상속관계)  
1-3. [포함관계](#1-3-포함관계)  
1-4. [클래스 간 관계 결정하기](#1-4-클래스-간-관계-결정하기)  
1-5. [단일상속](#1-5-단일상속)  
1-6. [Object 클래스](#1-6-object클래스)  
2. [오버라이딩](#2-오버라이딩)  
2-1. [오버라이딩이란?](#2-1-오버라이딩이란)  
2-2. [조건(규칙)](#2-2-조건규칙)  
2-3. [참조변수 super](#2-3-참조변수-super)  
2-4. [부모의 생성자 super()](#2-4-부모의-생성자-super)  
3. [package와 import](#3-package와-import)  
3-1. [패키지](#3-1-패키지)  
3-2. [패키지의 선언](#3-2-패키지의-선언)  
3-3. [클래스패스 설정](#3-3-클래스패스-설정)  
3-4. [import문](#3-4-import문)  
3-5. [import문 선언](#3-5-import문-선언)  
4. [제어자(modifiers)](#4-제어자modifiers)  
4-1. [제어자란?](#4-1-제어자란)    
4-2. [static - 클래스의, 공통적인](#4-2-static---클래스의-공통적인)  
4-3. [final - 마지막의, 변경될 수 없는](#4-3-final---마지막의-변경될-수-없는)  

***
### 1. 상속
  - #### 1-1. 상속이란?
    - 기존클래스를 재사용해서 새로운 클래스를 작성하는 것  
    - 두 클래스를 부모와 자식으로 관계를 맺어주는 것  
    - 자식은 부모의 모든 멤버를 상속받는다. (생성자, 초기화 블럭 제외)  
    - 자식의 변경은 부모에 영향을 미치지 않는다.  
    - 자식의 멤버개수는 조상보다 적을 수 없다.(같거나 많음)  
  
  - #### 1-2. 상속관계
    - 공통부분은 부모에서 관리하고 개별부분은 자식에서 관리  
    - 부모의 변경은 자식에게 영향을 미치지만, 자식의 변경은 조상에 아무런 영향을 끼치지 않음  
  
  - #### 1-3. 포함관계
    - 클래스의 멤버로 다른 클래스 타입의 참조변수를 선언하는 것  
    - 작은 단위의 클래스를 만들고 이들은 조합해서 클래스를 만든다.  
  
  - #### 1-4. 클래스 간 관계 결정하기 
    - 상속 vs 포함
      가능한 많은 관계를 맺어주어 재사용성을 높이고, 관리하기 쉽게 한다.
      ```
      1. 상속관계
         ~ 는 ~ 이다. (~ is a ~ .)
         
         class Circle {
           Point p = new Point(); // 원점의 x,y좌표를 가진 클래스
           int r;
         }
         
         class Point {
           int x; // x 좌표
           int y; // y 좌표
         }
 
      2. 포함관계 
         ~ 는 ~ 를 가지고 있다. (~ has a ~ .)
        
        대부분의 경우 포함이라고 보면 된다.
      ```
  
  - #### 1-5. 단일상속
    - Java는 단일상속만을 허용한다.  
    - 비중이 높은 클래스 하나만 상속관계로, 나머지는 포함관계로 한다.  

  - #### 1-6. Object클래스
    - 모든 클래스의 조상, 부모가 없는 클래스는 자동으로 Object 클래스를 상속 받는다.  
    - 모든 클래스는 Object클래스에 정의된 11개의 메서드를 상속받는다.  

### 2. 오버라이딩
  - #### 2-1. 오버라이딩이란?
    - 상속받은 부모의 `메서드`를 자신에 맞게 변경하는 것
      ```java
      class Point {
        int x;
        int y;
        
        String getLocation() {
          return "x : " + x + "y : " + y;
        }
      }
      
      class Point3D extends Point {
        int z;
        String getLocation() {
          return "x : " + x + "y : " + y + "z : " + z;
        }
      }
      ```
    
  - #### 2-2. 조건(규칙)
    - 오버라이딩의 조건  
      ```
      1. 선언부가 부모와 일치
      2. 접근제어자를 부모클래스보다 좁은 범위로 변경할 수 없음
      3. 예외는 부모메서드보다 많이 선언할 수 없다. 
      ```
    
    - 참고  
      <table>
        <tr>
          <th>
            오버로딩
          </th>
          <th>
            new
          </th>
          <th>
            - 자식에 없는 새로운 메서드를 정의<br>
            - 이름이 같고 매개변수가 다른경우
          </th>
        </tr>
        <tr>
          <th>
            오버라이딩
          </th>
          <th>
            change / modify
          </th>
          <th>
            - 상속받은 메서드의 내용을 변경하는 것<br>
            - 가져다가 쓴다.
          </th>
        </tr>
      </table>

  - #### 2-3. 참조변수 super 
    - 객체 자신을 가리키는 참조변수
    
    - 인스턴스 메서드(생성자) 내에서만 존재
    
    - 부모의 멤버와 자신의 멤버를 구별하는데 사용
    
    - 참조변수 this와 역할이 비슷 

    참고
    <table>
      <tr>
        <th>
          this
        </th>
        <th>
          인스턴스 변수와 지역변수의 구별시 사용
        </th>
      </tr>
      <tr>
        <th>
          super
        </th>
        <th>
          부모의 멤버와 자신의 멤버를 구별시 사용
        </th>
      </tr>
    </table>
  
  - #### 2-4. 부모의 생성자 super()
    - 부모의 생성자를 호출시 사용  
      왜? 생성자와 초기화 블럭은 상속이 안되므로.. 
    
    - 부모의 멤버는 부모의 생성자를 호출해서 초기화 해야함  
      왜? 자식의 생성자는 자신이 선언한 변수만 초기화가 가능하므로..
    
    - 자식의 생성자의 첫줄에 반드시 부모의 생성자를 호출해야한다.  
      왜? 부모의 멤버들도 초기화되어야 하기 때문에  
    
    - Object 클래스를 제외한 모든 클래스의 생성자 첫줄에는  
      반드시 같은 클래스의 다른 생성자 또는 부모의 생성자를 호출해야함   
      호출하지 않으면, 컴파일러가 자동으로 삽입..

### 3. package와 import
  - #### 3-1. 패키지
    - 서로 관련된 클래스와 인터페이스의 묶음  
    
    - 클래스파일 = (*.class)    
      패키지 = 폴더  
      서브패키지 = (패키지명).(서브패키지명)  
    
    - 클래스의 실제이름은 패키지명이 포함된 것  
      Ex) String class → java.lang.String
      
  - #### 3-2. 패키지의 선언
    - 소스파일 첫 번째 문장(주석제외)으로 단 한번 선언  
      Package (패키지명);
      
    - 같은 소스파일의 클래스들은 모두 같은 패키지에 속하게 됨  
  
  - #### 3-3. 클래스패스 설정
    - 클래스파일(*.class) 위치를 찾는 경로
    
    - 환경변수로 관리하며, 경로간 구분은 `;` 사용, 환경변수에 패키지 루트를 등록 필요

  - #### 3-4. import문
    - 컴파일러에게 클래스가 속한 패키지를 알려줌  
    
    - import문 사용하면 클래스 사용시 패키지명 생략 가능  
      Ex) import java.util.*;  
    
  - #### 3-5. import문 선언
    - 소스파일 구성 순서  
      ```java
      1. package문
      2. import문
      3. 클래스 선언

      Ex)
      package com.javachobo.book;
      
      import java.util.*;
      
      public class Test {
        public static void main(String[] args) {
          Date today = new Date();        
        }
      }
      ```  
    - 선언 방법  
      `import 패키지명.클래스명;`  
      참고 : 컴파일시 처리되므로 성능에 영향 미치지 않음
      
      이름이 같은 클래스가 속한 두패키지를 선언하는 경우
      ```java
      import java.sql.*;  //java.sql.Date;
      import java.util.*; //java.util.Date;
      
      public class Test {
        public static void main(String[] args) {
          // 클래스 앞에 패키지명을 붙여줘야함 
         java.util.Date today = new java.util.Date();
        }
      }
      ```
      
   - static import문  
     static 멤버(static 메서드, cv)를 사용시 클래스 이름 생략가능하게 해줌.  
     ```java
     import static java.lang.Integer;
     import static java.lang.Math.random; 
     import static java.lang.System.out; // out.println(random()); 처럼 사용가능
     import static java.lang.Math.PI; // cv도 대상 out.println(PI); 처럼 사용가능
     import static java.lang.Math.*; // 권장되지 않음
     ```  

### 4. 제어자(modifiers)
  - #### 4-1. 제어자란?  
    - 클래스와 변수, 메서드의 선언부에 사용되어 부가적인 의미를 부여  
    - 하나의 대상에 여러 제어자를 같이 사용 가능(단, 접근제어자는 단 하나만 사용 가능)  
    - 분류
      ```
      접근 제어자 - public, protected, default, private
      
      그 외 - static, final, abstract, native, transient, sychronized, volailo, strictfp
      ```  
  - #### 4-2. static - 클래스의, 공통적인  
    - 사용 가능 한 곳 : 멤버변수, 메서드, 초기화 블럭(static {})에서 사용 가능  
      ```java
      class StaticTest {
        // 모든 인스턴스에 공통적으로 사용되는 클래스변수가 됨
        // 인스턴스를 생성하지 않고도 사용 가능
        // 클래스가 메모리에 로드될 때 생성
        static int width = 200;  // 멤버 변수
        static int height = 120;
        
        static { // 클래스 초기화 블럭
        // static 변수의 복잡한 초기화 수행
        }
       
        // 인스턴스 생성하지 않고 호출 가능
        // static 메서드 내에서는 인스턴스 멤버들을 직접 사용 불가
        static int max(int a, int b) {
          return a > b ? a : b;
        }
      }
      ```
 
  - #### 4-3. final - 마지막의, 변경될 수 없는  
    - 사용 가능 한 곳 : 클래스, 메서드 멤버변수, 지역변수
       ```java
       // 변경, 확장 될수 없는 클래스가 됨 -> final로 지정된 클래스는 다른 클래스의 부모가 될 수 없음
       final class FinalTest {
         // 값을 변경할 수 없는 상수가 됨
         final int MAX_SIZE = 10;  // 멤버 변수
       
         static { // 클래스 초기화 블럭
         // static 변수의 복잡한 초기화 수행
         }
       
         // 변경 될 수 없는 메서드, 오버라이딩을 통해 재정이 불가!
         final void getMaxSize() {
           // 값을 변경할 수 없는 상수가 됨
           final int LV = MAX_SIZE; //지역 변수
           return MAX_SIZE;
         }
       }
       ```
    - 참고 : 대표적인 final 클래스는 String, Math 클래스  
  
    - 생성자를 이용한 final 멤버변수 초기화  
      - 보통은 선언과 초기화를 동시에 하지만,   
        인스턴스마다 고정값을 갖는 인스턴수 변수의 경우 `생성자에서 단 한번 초기화`  
        (카드의 무늬와 숫자는 한번 결정되면 바뀌지 않아야 하는 경우)  
      ```java
      class Card {
        final int NUMBER;
        final String KIND;
        static int width = 200;
        static int height = 120;
        
        Card(String kind, int num) {
          KIND = kind;
          NUMBER = num;
        }
        
        Card() {
          // 같은 클래스의 다른 생성자를 호출 시 사용 this() 생성자
          this("HEART", 1);
        }
        
        public String toString() {
          return "" + KIND + " " + NUMBER;
        }
      }
      
      public static void main(String[] args) {
        Card c = new Card("HEART", 10);
      }
      ```

## Reference   
  - [남궁성 자바의 정석 기초편](https://youtube.com/playlist?list=PLW2UjW795-f6xWA2_MUhEVgPauhGl3xIp)  
  - [남궁성 객체지향 개념](https://codechobo.tistory.com/25?category=645496) 
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")

