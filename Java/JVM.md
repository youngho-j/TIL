# 자바 가상 기계(JVM)
  - 자바 프로그램을 이루고 있는 바이트 코드를 해석하고 실행할 수 있는 가상의 운영체제
    * 바이트 코드는 모든 JVM에서 동일한 실행 결과 보장, but JVM은 운영체제에 종속적(운영체제에 맞는 JVM 설치 필요)   
   <p align="center"> <img src="/img/Java/javaExecution.png" width="50%" height="40%" title="자바실행단계사진"></img></p>   
    
    1. .java 파일(소스파일) 작성    
    2. 컴파일러(javac.exe)로 컴파일
    3. .class 파일(바이트 코드 파일) 생성
    4. JVM 구동 명령어(java.exe)에 의해 해석, 운영체제에 맞는 기계어로 번역   
  
  - JVM의 메모리 구조 (5가지)
    1. method Area (메소드 영역)  
       ```
       클래스 변수의 이름, 타입, 접근제어자 등과 같은 `클래스와 관련된 정보를 저장` 
       그외에도 `static 변수, 인터페이스 등을 저장`  
       
       모든 스레드에서 공유  
       
       JVM 시작시 생성되고 프로그램 종료까지 유지  
       
       즉, 클래스 데이터를 위한 공간
       ```
       
    2. Heap Area (힙 영역) 
       ```
       new를 통해서 생성된 객체와 배열의 인스턴스를 저장 (method Area에 올라온 클래스들만 객체로 생성 가능)
       
       힙영역에서 생성된 객체는 스택 영역의 변수나 다른 객체의 필드에서 참조 
       
       명시적으로 null, 참조되지 않는 객체는 GC의 대상이 됩니다.
       
       객체를 위한 공간
       ```
       
       - Heap 영역은 크게 Young Generation, Old Generation 로 나눌 수 있음(Java8 부터 변경됨)  
         Young Generation
           ```
           새롭게 생성한 객체들이 위치 
           
           대부분의 객체는 금방 접근 불가능한 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라진다.
           
           Eden 1개와 Survivor1,2로 구성
           
           Eden은 Object가 heap에 최초로 할당되는 장소
           영역이 꽉차면 Object의 참조 여부에 따라 Survivor영역으로 넘기게 됨
           Survivor영역에서는 각 영역이 채워지게 되면, 살아남은 객체는 비워진 Survivor로 이동하게 됨  
           이때 참조가 없는 객체들은 Minor GC로 수집 됨 따라서, 항상 Survivor1과 2중 한 곳은 비어있는 상태가 됨 
           (Minor GC는 Eden, Survivor에서 발생하는 GC)
           ```
         
         Old Generation
           ```
           Young 영역에서 계속 사용되어 살아남은 객체가 복사되는 영역
           Young 영역보다 크게 할당되며, Major GC가 이루어지며, Minor GC보다 횟수가 적음 
           (Major GC는 Old, Permanent 영역에서 발생하는 GC)
           ```
       
    3. Stack Area (스택 영역) 
       ```
       메소드가 실행 시 스택 영역에 메소드에 대한 영역이 1개 생성
       
       지역변수, 매개변수, 리턴값 등을 저장  
       
       메소드가 호출될 때마다 프레임이라고 불리는 영역으로 할당되며 프레임별로 관리
       
       primitive 타입은 바로 스택영역에 저장, 그 외에는 힙영역이나 메소드 영역의 객체 주소를 저장
       ```
    4. PC register 
       ```
       스레드가 시작될 때 생성, 스레드마다 하나씩 존재 
       
       현재 스레드가 실행되는 부분의 주소와 명령을 저장
       ```
    
    5. Native Method Stack 
       ```
       자바 외의 언어로 작성된 코드를 위한 메모리 영역
       
       JNI (Java Native Interface)에 의해 실행
       ```
       
## Reference   
  - 신용권, 이것이 자바다, 한빛미디어(2019)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
