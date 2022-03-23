# String, StringBuffer, StringBuilder   
  - 공통점 : 문자열 저장, 관리
  - 차이점  
    1. String, StringBuilder, StringBuffer 차이  
       String : `Immutable`  
       StringBuilder, StringBuffer : `Mutable`  
       
    2. StringBuilder, StringBuffer 차이  
       문자열 연산 등으로 기존 객체의 공간이 부족해지는 경우 기존 버퍼의 크기를 늘리며 유연하게 동작하나,  
       StringBuilder : `동기화를 보장하지 않음`  
       StringBuffer : 각 메서드별 Synchronized Keyword가 존재하여, 멀티스레드 환경에서도 `동기화를 지원`  

  - String  
    - `Immutable(불변)`  
      ```
      Strings are constant; their values cannot be changed after they are created
      -> 문자열은 일정하며, 생성 후에는 값을 변경 할 수 없다.
         크기가 고정되어 내부의 문자열을 수정할 수 없음
      ```
    - 문자열을 조작하는 경우(단순할때) 유용
    - 동기화에 대해 신경 쓰지 않아도 되기 때문에(Thread-safe), 내부 데이터를 자유롭게 공유 가능
    - String str = new String() 객체 생성 방법
      ```java
      - String str = new String("str");
      
      - 위 방식으로 선언한 만큼 Heap Area에 할당    
      
      - 즉, 같은 문자열이라도 다른 객체이기때문에 선언한 만큼 새로운 객체가 메모리(Heap Area)에 올라간 뒤 그 객체를 참조하도록 함   
      ```
    - 문자열 리터럴 이용 객체 생성 방법
      ```java
      - String str = "str";
      
      - Heap Area 내부 String constant pool(상수 영역)에 할당
      
      - 내부적으로 String의 intern() 메소드 호출하여 주어진 문자열이 String constant pool에 존재하는지 검색      
        존재할 경우 해당 주소값을 할당 받아 반환  
        Ex) String str1 = "str";
            String str2 = "str";
            
            // "str" 이라는 문자열이 이미 String constant pool에 존재하므로, 생성하지 않고 str2는 "str"의 주소값을 참조 
            // 위 코드처럼 여러번 생성해도 실제 생성 String 객체는 하나 즉, 메모리에는 하나만 올라감        
        
        없을 경우 String constant pool에 생성하고 새로운 주소값 반환   
        Ex) String str1 = "str";
            str1 = str + "str2";
            
            // str + "str2" 이라는 문자열이 String constant pool에 존재하지 않으므로, 생성한 후 str1는 str +"str2"의 주소값을 참조
            // 기존에 생성되었던 "str" 값은 참조 해제 되어 GC의 메모리 해제를 기다림
      ```
  - StringBuilder  
    - `Mutable(변함)`  
      ```
      A mutable sequence of characters.
      -> 변경 가능한 문자 시퀀스
      ```
    - `동기화를 보장하지 않음`  
      ```
      This class provides an API compatible with StringBuffer, but with no guarantee of synchronization.
      -> 해당 클래스는 StringBuffer와 호환되는 API를 제공하지만, 동기화를 보장하지 않는다.
      ```
    - 일반적으로 단일 스레드에서 StringBuffer의 대체품으로 설계, StringBuffer보다 우선적으로 사용하는 것이 좋음  
  - StringBuffer
    - `Mutable(변함)`    
      ```
      A thread-safe, mutable sequence of characters
      -> 스레드로부터 안전하고, 변경 가능한 문자 시퀀스
      ```
    - `Thread-safety`  
      ```
      Thread-safety  
      : 멀티 스레드 프로그래밍에서 일반적으로 어떤 함수나 변수, 혹은 객체가 
      여러 스레드로부터 동시에 접근이 이루어져도 프로그램의 실행에 문제가 없음
      ```
  - 결론
    - `String`은 짧은 문자열을 더할 경우 사용하면 좋음
    
    - `StringBuffer`는 스레드 안전한 프로그램이 필요한 경우, 개발 중인 시스템의 부분이 스레드에 안전한지 모를 경우 사용하면 좋음

    - `StringBuilder`는 스레드 안전 여부가 전혀 관계 없는 프로그램을 개발 시 사용하면 좋음  
    
    - 성능비교 
      연산이 많을 경우 `StringBuilder > StringBuffer >>> String`  
  
## Reference   
  - [StringBuffer docs](https://docs.oracle.com/javase/7/docs/api/java/lang/StringBuffer.html)  
  - [StringBuilder docs](https://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html)  
  - [String docs](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html)  
  - [코딩팩토리 String, StringBuffer, StringBuilder의 차이점과 사용이유](https://coding-factory.tistory.com/546)  
  - [마이너의 일상 Java에서 String과 new String()의 차이는?](https://tomining.tistory.com/195)
  - [String intern 메서드](https://www.latera.kr/reference/java/2019-01-31-java-string/)  
  - [길은 가면, 뒤에있다 String, StringBuilder, StringBuffer 차이](https://12bme.tistory.com/42)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
