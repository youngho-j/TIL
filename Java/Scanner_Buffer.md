# Scanner, Buffer
  - Buffer
    - `임시 저장 공간`  
    - 예시
      ```java
      Scanner sc = new Scanner(System.in);
      
      String str = sc.nextLine();
      
      1. str 변수에 사용자 입력 값을 저장 선언
      2. sc.nextLine()을 통해 사용자 입력 값을 받음  
         (입력값은 완료시까지 임시로 버퍼에 저장됨)
      3. 모든 입력 완료시(Enter 키 입력시) 버퍼에 있는 값을 가져와 변수에 저장
      ```

  - Scanner  
    - 기본적인 데이터 타입을 Scanner 클래스의 메서드를 사용하여 입력 받을 수 있음
      ```java
      import java.util.Scanner;
      
      Scanner sc = new Scanner(System.in);
      
      String str1 = sc.next();
      String str2 = sc.nextLine();
      
      int intValue = sc.nextInt();
      ```
    - 패키지 import 필요
    - 공백(whiteSpace) or 개행(줄 바꿈)을 기준으로 읽음
    - 메서드
      - next()
        ```java
        import java.util.Scanner;
        
        Scanner sc = new Scanner(System.in);
        
        // 다음 토큰을(공백 전까지 입력받은 문자열) 문자열로 리턴
        String intValue = sc.next();
        
        예시 : 사용자 입력값 1 9 가정시
        1. 모든 입력이 완료되기전까지 다른 작업 처리
        2. Enter 입력시 공백 전까지 입력받은 문자열을 가져옴
        3. 변수에 저장 (intValue = 1)
        4. buffer에는  ' 9\n' 값이 남아있게됨  
        ```
      - nextInt()  
        ```java
        import java.util.Scanner;
        
        Scanner sc = new Scanner(System.in);
        
        //버퍼에 남아있는 '연속된 숫자만 리턴'
        int intValue = sc.nextInt();
        
        예시 : 사용자 입력값 119 가정시
        1. 모든 입력이 완료되기전까지 다른 작업 처리
        2. Enter 입력시 버퍼에 있는 연속된 번호만 가져옴
        3. 변수에 저장 (intValue = 119)
        4. buffer에는 Enter에 해당하는 값인 '\n' 만 남아있게됨  
           (해당 메서드 사용 후 nextLine시 실제 출력은 '\n' 만 적용됨)
        ```
      - nextLine()
        ```java
        import java.util.Scanner;
        
        Scanner sc = new Scanner(System.in);
        
        // '\n'(엔터) 값을 만나기 전까지의 값을 리턴, '\n'값도 제거
        String strValue = sc.nextLine();
        예시 : 사용자 입력값 '가위 바위 보' 가정시
        1. 모든 입력이 완료되기전까지 다른 작업 처리
        2. Enter 입력시 버퍼에 있는 \n을 만날 때까지의 모든 값을 가져옴
        3. 변수에 저장 (strValue = "가위 바위 보")
        4. '\n' 값 제거
        5. buffer는 비어있게 됨  
        ```

## Reference   
  - [Scanner docs](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)  
  - [Space_Jin 사용자 입출력과 버퍼](https://reinvestment.tistory.com/44)  
  - [st-lab 스캐너클래스와 입력](https://st-lab.tistory.com/92)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")