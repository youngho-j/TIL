# String str = new String(" ") / String str = " " 차이   
  - String
    * new String() 이용 
      ```java
      - String str = new String("str");
      - Heap area에 할당    
      - 같은 문자열이라도 다른 객체이기때문에 선언한 만큼 새로운 객체가 메모리에 올라감       
      ```
      
    * 리터럴 이용
      ```java
      - String str = "str";
      - String constant pool(상수 영역)에 할당
      - 내부적으로 String의 intern() 메소드 호출, 주어진 문자열이 String constant pool에 존재하는지 검색,    
        존재할 경우 해당 주소값을 할당 받아 반환, 없을 경우 String constant pool에 생성하고 새로운 주소값 반환   
        -> 즉, 메모리에는 하나만 올라감
      ```
      
  - 결론
     * 같은 값을 갖더라도 **메모리 상에서 처리되는 방식이 다름**
  
  - 더 알아보기
     * String constant pool은 Heap area에 포함된 공간!
     * String class의 .intern() 메소드를 사용시 heap area에 할당된 값을 String constant pool에 등록 가능
     * 사진
       <p align="center"><img src="/img/Java/String_differ_newString.png" width="60%" height="40%" title="String str = new String(" ") / String str = " " 차이"></img></p> 
  
## Reference   
  - [journaldev What is Java String pool?](https://www.journaldev.com/797/what-is-java-string-pool)
  - [기록은 기억을 이긴다 String 리터럴과 객체생성의 차이](https://qssdev.tistory.com/38)
  - [마이너의 일상 Java에서 String과 new String()의 차이는?](https://tomining.tistory.com/195)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
