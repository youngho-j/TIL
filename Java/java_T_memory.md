# 객체 지향 프로그램의 메모리 사용 방식 
## 목차

1. [메모리 사용 방식](#1-메모리-사용-방식)    
1-1. [프로그램이 메모리 사용하는 방식](#1-1-프로그램이-메모리-사용하는-방식)  
1-2. [객체 지향 프로그램(Java)의 메모리 사용 방식](#1-2-객체-지향-프로그램java의-메모리-사용-방식)    
1-3. [main() 메서드 실행 시 메모리 변화 과정](#1-3-main-메서드-실행-시-메모리-변화-과정)  
***
### 1. 메모리 사용 방식
  - #### 1-1. 프로그램이 메모리 사용하는 방식
    - 프로그램이 메모리 사용시 코드 실행 영역과 데이터 저장 영역으로 나누어 사용
      <table>
        <tr>
          <th>
            코드 실행 영역
          </th>
          <th>
            데이터 저장 영역
          </th>
        </tr>
      </table>  

  - #### 1-2. 객체 지향 프로그램(Java)의 메모리 사용 방식
    - 객체 지향 프로그램에서는 데이터 저장 영역 부분을 static, stack, heap 영역으로 분할하여 사용  
      세가지로 분할 된 영역을 `T 메모리 구조`라고 부름  
    
      <table>
        <tr>
          <th rowspan="2">
            코드 실행 영역
          </th>
          <th colspan="2">
            Static 영역
          </th>
        </tr>
        <tr>
          <th>
            Stack 영역
          </th>
          <th>
            Heap 영역
          </th>
        </tr>
      </table>
      
      ```
      Static 영역 - "클래스"들의 놀이터
      Stack 영역 - "메서드"들의 놀이터
      Heap 영역 - "객체"들의 놀이터
      ```

- #### 1-3. main() 메서드 실행 시 메모리 변화 과정
  - Test.java 파일 실행 시 메모리 변화
    ```java
    public class Test {
      public static void main(String[] args) {
        System.out.println("Test Start");
      }
    }
    ```
    1. JRE가 프로그램의 main() 메서드 존재를 확인함  
    
    2. JRE가 JVM 부팅  
    
    3. JVM이 목적파일(여기에선 Test.java)을 받아 실행  
    
    4. JVM이 java.lang 패키지를 static 영역에 올림  
       - java.lang 패키지는 모든 자바프로그램이 반드시 포함한다.  
         <p><img src="/img/Java/memory4.png" width="60%" height="60%" title="4번 과정 이미지"></img></p>  
    5. JVM은 개발자가 작성한 모든 클래스와 import 패키지를 static 영역에 올림  
         <p><img src="/img/Java/memory5.png" width="60%" height="60%" title="5번 과정 이미지"></img></p>  
       
    6. public static void main(String[] args) 실행 시 main() 메서드의 stack frame이 stack 영역에 할당  
       - stack frame은 여는 중괄호를 만날 때마다 하나씩 생성(즉, 메서드 실행, if문, 반복문, try~catch문 등도 생성됨)  
         단, 클래스를 정의하는 여는 중괄호 제외한다.   
         <p><img src="/img/Java/memory6.png" width="60%" height="60%" title="6번 과정 이미지"></img></p>  
    
    7. 메서드 인자 args에 저장할 변수 공간을 stack frame 맨 아래 할당  
         <p><img src="/img/Java/memory711.png" width="60%" height="60%" title="7번 과정 이미지"></img></p>  
       
    8. System.out.println("Test Start"); 실행  
    
    9. main() stack frame이 대기중으로 변경되고, println 메서드의 stack frame이 stack 영역 맨 위에 할당   
         <p><img src="/img/Java/memory9.png" width="60%" height="60%" title="9번 과정 이미지"></img></p>  

    10. 닫는 중괄호를 만나면 stack frame 소멸  
    
    11. main() 메서드 종료   
        - JRE는 JVM을 종료하고 JRE도 운영체제 상의 메모리에서 사라짐  
        - 메모리(스태틱 영역, 스택 영역, 힙 영역)도 사라짐  
          <p><img src="/img/Java/memory711.png" width="60%" height="60%" title="11번 과정 이미지"></img></p>  

## Reference   
  - [gaya309.log main() 메서드: 메서드 스택 프레임](https://velog.io/@gaya309/TIL-%EB%8B%A4%EC%8B%9C-%EB%B3%B4%EB%8A%94-main-%EB%A9%94%EC%84%9C%EB%93%9C-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%8A%A4%ED%83%9D-%ED%94%84%EB%A0%88%EC%9E%84#%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%B4-%EB%A9%94%EB%AA%A8%EB%A6%AC%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B0%A9%EC%8B%9D)  
  - [siyoon210 자바(JVM)의 메모리 사용 방식 (T 메모리 구조)](https://siyoon210.tistory.com/124) 
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
