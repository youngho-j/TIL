# 자바_입력관련 내용 정리
## 목차
1. [Java 인코딩](#1-java-인코딩)  
1-1. [처리방식](#1-1-처리방식)  
1-2. [인코딩 수행과정](#1-2-인코딩-수행과정)  
2. [입력방법](#2-1-입력방법)  
2-1. [Stream이란?](#2-1-stream이란)  
2-2. [InputStream과 System.in](#2-2-inputstream과-system-in)  
2-3. [Scanner(System.in)와 InputStreamReader(System.in)](#2-3-scannersystem-in와-inputstreamreaderSystem-in)  
2-4. [BufferedReader()](#2-4-bufferedreader)  
2-5. [정리](#2-5-정리)  
***
### 1. Java 인코딩
  - #### 1-1. 처리방식
    - Ex) String 처리시  
      ```
      내부(메모리 상) - UTF-16 BE 인코딩 처리
      송수신을 위해 직렬화 필요시 - 변형된 UTF 8 인코딩 처리
      문자열 입출력 - 사용자 지정 인코딩 값 or 운영체제 기본 인코딩 값으로 인코딩 처리
      ```
    
    - UTF-8과 UTF-16의 차이  
      `Byte 구성 방식`에서 차이  
        UTF - 8   
        ```
        문자의 영역에 따라 Byte 사용 개수가 다름
        Ex) 영어 - 1Byte / 한글 - 3Byte
        ```
        UTF - 16    
        ```
        거의 모든 문자가 2Byte로 구성
        참고) 4Byte로 구성되어 있는 경우 있긴함(surrogate)
        ```
  - #### 1-2. 인코딩 수행과정
    - Ex) encodingType = UTF-8
      ```
      1. 입력(UTF-8)
      2. 송수신(modified UTF-8)
      3. 자바 메모리(UTF-16 BE)
      4. 송수신(modified UTF-8)
      5. 출력(UTF-8)
      ```
### 2. 입력방법
  - #### 2-1. Stream이란?
    - A,B 수도관이 연결되어있고, 수도꼭지를 틀었을 때 A 에서 B로 이동하는 `물의 흐름`을 스트림이라고 할 수 있음  
    - `출발지와 도착지를 이어주는 빨대`   
    - Ex) 파일 데이터, HTTP 응답 데이터, 키보드 입력  
    - `단방향` 이므로 입출력이 동시에 발생 불가!  
  
  - #### 2-2. InputStream과 System.in
    - System 클래스의 in 필드는 InputStream 의 정적 필드  
      따라서 InputStream input = System.in; 으로 할당이 가능하다.
      
    - 해당 선언 후 read() 메서드 사용시 입력이 가능함. 주의할 점은 반드시 예외처리를 해줘야함(try ~ catch, throws)
      ```java
      import java.io.IOException;
      import java.io.InputStream;
 
      public class InputTest {
        public static void main(String[] args) throws IOException {
		      InputStream inputstream = System.in;
		      int a = inputstream.read();
		      System.out.println("출력 : " + a);
	      }
      }
      
      입력 : 91
      출력 : 57
      ```
    - 입력은 가능하지만 전혀 다른 값이 나오게 됨  
      왜? InputStream.read()의 특징을 보면 알 수 있음  
      1. 입력받은 데이터는 int 형으로 저장
      2. 저장 시 해당 문자의 시스템 or 운영체제의 인코딩 형식의 10진수로 변수에 저장됨
      3. `1byte만 읽음` - 중요!

    - 즉, InputStream은 바이트 단위로 데이터를 보내고, read()메소드는 1바이트 단위로 읽어 옴  
      따라서, 2byte 이상으로 구성되어 있는 인코딩 사용시 1byte 값만 읽어오고 나머지는 스트림에 남아있음 
      읽어들인 byte 값은 메모리에 UTF-16 BE에 대응되는 문자의 인코딩 방식으로 2진수 값이 저장
      출력시 메모리에 저장된 2진수에 대응되는 문자가 지정한 인코딩 타입으로 변환한 값이 출력됨   
      이렇게 바이트 단위로 주고 받는 스트림을 `바이트 스트림`이라고 함
      
    - 그렇다면 바이트 스트림은 여러개의 문자를 입력 받을때 어떻게 해야 하나?   
      바이트 배열 선언 후 read()메서드에 넣은 뒤 for문 돌려 출력 하면 됨  
      하지만, 결과는 위와 같이 10진수로 변환된 값 나옴  
      ```
      배열 입력 : a b c
      출력 : 97 98 99
      ```
   - 입력된 값을 그대로 출력하고 싶은 경우에는 어떻게 해야 하나?  
     출력시 char로 캐스팅 한 뒤 출력 하면 됨  
     
     주의! 한글은 캐스팅 안됨  
     왜? 아스키 코드 확장판에 한글이 없기 떄문에, 또한 UTF-8 사용시 한글은 3byte이기 때문에   
       
  - #### 2-3. Scanner(System.in)와 InputStreamReader(System.in)
    - 목표 : `어느 경로를 통해 입력을 받게 되는지를 보는 것`  
    - Ex) Scanner 
      ```java
      import java.io.IOException;
      import java.io.InputStream;
      import java.util.Scanner;
      
      public class InputTest {
        public static void main(String[] args) throws IOException {
		      InputStream inputstream = System.in;
		      Scanner sc = new Scanner(inputStream);
          
          int a = sc.nextInt();
		      System.out.println(a);
	      }
      }
      ```
    - 코드 실행 과정
      ```
      1. InputStream (바이트스트림) 을 통해 입력 받음
      2. Scanner 클래스의 오버로딩된 생성자 public Scanner(InputStream source)로 이동
      3. new InputStreamReader(source), WHITESPACE_PATTERN 를 this 즉, private Scanner(Readable source, Pattern pattern) 생성자로 보냄  
      4. 문자로 온전하게 받기 위해 중개자 역할을 하는 InputStreamReader(문자스트림) 을 통해 char 타입으로 데이터를 처리함
      5. 입력받은 문자는 입력 메소드( next(), nextInt() 등등.. ) 의 타입에 맞게 정규식을 검사함
      6. 정규식 문자열을 Pattern.compile() 이라는 메소드를 통해 Pattern 타입으로 변환함
      7. 반환된 Pattern 타입을 String으로 변환함
      8 .String 은 입력 메소드의 타입에 맞게 반환함 ( nextInt() - Integer.parseInt() / nextDouble() - Double.parseDouble() 등등.. )
      ```
    - 위의 코드 실행과정에서 nextInt() 사용시 정규식을 불필요할 정도로 많이 사용하기 떄문에 속도와 성능이 좋지 않다는 것을 알 수 있음

    - InputStreamReader?
      - InputStream의 특징을 해결하기 위해 확장 시킨 것  
      - `문자를 온전하게 읽어 들일 수 있음`  
      - 즉, InputStream 의 바이트 단위로 읽어 들이는 형식을 문자단위(character)로 데이터로 변환시키는 `중개자 역할`  
      - 참고 : 바이트 데이터를 문자 단위로 변환하는 것은 Charset이라는 클래스에서 담당  
        해당 클래스 덕분에 UTF-8에서 한글이 2byte로 변환되어 자바 메모리상에섯 char 타입에 한글이 대입 될 수 있음  
      - `문자스트림`이라고 함  
      - char 배열로 데이터를 받을 수 있음
    
    - Ex) InputStreamReader
      ```java
      import java.io.IOException;
      import java.io.InputStream;
      import java.io.InputStreamReader;
 
      public class Input_Test {
	      public static void main(String[] args) throws IOException {
		
		    InputStreamReader isr = new InputStreamReader(System.in);
			
		    int c = isr.read();
		
		    System.out.println("출력 : " + (char)c);
		    System.out.println("출력 : " + c);
	      } 
      }
      
      입력 : 가
      출력 : 가
      출력 : 44032
      ```
      
  - #### 2-4. BufferedReader()
    - 목표 : `어느 경로를 통해 입력을 받게 되는지를 보는 것`  
    - Ex) BufferedReader
      ```
      InputStream inputstream = System.in;
      InputStreamReader sr = new InputStreamReader(inputstream);
      BufferedReader br = new BufferedReader(sr);
      ```
    - 위 코드를 통해 알 수 있는 것
      ```
      1. 바이트 스트림인 InputStream 을 통해 바이트 단위로 데이터를 입력을 받는다.
      2. 입력 받은 데이터를 char 형태로 처리하기 위해 중개자 역할인 문자스트림 InputStreamReader를 사용한다.
      ```
    - 그렇다면 BufferedReader는 왜 사용하는가?  
      InputStreamReader는 문자를 처리하는 것이지 문자열을 처리하는 것은 아님  
      만약 문자열을 입력하고 싶으면 배열을 선언해서 사용해야함.  
      이러한 불편함을 해결하기 위해 Buffer(버퍼)를 통해 입력받은 문자를 쌓아둔 뒤 한 번에 문자열처럼 보내버리는 방법을 택함  
     
    - BufferedReader
      ```java
      BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
      
      System.in = InputStream  -> InputStreamReader -> BufferedReader

      byte 타입으로 읽어들이는 in을 char 타입으로 처리한 뒤 String, 즉 문자열로 저장할 수 있게 한다는 의미로 해석 가능
      ```
    - 특징
      1. 버퍼가 있는 스트림
      2. 별다른 정규식을 검사하지 않음
    
    - 정리  
      - 바이트 단위 [InputStream]로 문자를 입력받아 문자(character) [InputStreamReader]로 처리한 뒤  
        버퍼(buffer) [BufferedReader]에 담아두었다가 일정 조건이 되면 버퍼를 비우면서 데이터를 보내는 것  
      - 위의 특징 덕분에 입력 과정에서 Scanner에 비해 성능이 우수
      
  - #### 2-5. 정리  
    1. InputStream 은 바이트 단위로 데이터를 처리한다.   
       또한 System.in 의 타입도 InputStream 이다.  
    
    2. InputStreamReader 은 문자(character) 단위로 데이터를 처리할 수 있도록 돕는다.   
       InputStream 의 데이터를 문자로 변환하는 중개 역할을 한다.  
    
    3. BufferedReader 은 스트림에 버퍼를 두어 문자를 버퍼에 일정 정도 저장해둔 뒤 한 번에 보낸다.  

## Reference   
  - [Stranger's LAB 자바 입력 뜯어보기](https://st-lab.tistory.com/41)   
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
