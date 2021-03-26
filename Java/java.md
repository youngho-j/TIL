# 자바
  - 자바의 특징
    * 이식성이 높다
      + 이식성? 서로 다른 실행 환경을 가진 **시스템 간 프로그램을 옮겨 실행** 할 수 있는 것
      + 예) 윈도우 환경에서 실행되는 프로그램이 리눅스에서 실행 가능 -> 이식성이 높다.
      + **JRE(java Runtime Environment)** 자바 실행 환경이 설치되어있는 모든 운영체제에서 실행 가능  
    
    * 객체 지향 언어
      + 객체 지향 프로그래밍(OOP : Object Oriented Programming)  
        : 프로그램 개발 기법  
        1. 부품에 해당하는 **객체를 먼저 만듦**  
        2. 객체들을 하나씩 **조립 및 연결**  
        3. 전체 프로그램 **완성**  
      + 객체를 만들기 위해 설계도(클래스) 작성, 객체를 연결하여 프로그램을 만들어 냄 
        -> 캡슐화, 상속, 다형성을 완벽히 지원함  
    
    * 함수적 스타일 코딩 지원
      + 람다식(Lambda Expressions) : Java 8부터 지원  
        컬렉션의 요소를 필터링, 매핑, 집계 처리하는데 쉬워지고, 코드 간결  
    
    * 메모리 자동 관리
      + C++ : 메모리에 생성된 객체를 제거 -> 코드 작성필요  
        (이러한 작업이 지속적으로 이루어지지 않으면 프로그램 다운 될 수도..)
      + 자바 : 개발자가 직접 메모리에 접근 불가( **자바가 직접 관리** )  
        예) 객체 생성 -> 자동적으로 메모리 영역 할당, 사용 하지 않을 경우 Garbage Collector 실행하여 객체 제거  
        
    * 다양한 애플리케이션 개발 가능
      + 다양한 운영체제에서 사용할 수 있는 개발 도구와 API를 묶어 Edition 형태로 정의
      + Java SE(Standard Edition) - 기본 에디션 : JVM + 도구, 라이브러리 API를 정의   
        JDK(Java Development Kit) : 자바 개발 키트, Java SE 구현체, 자바 프로그램을 개발하고 실행하기 위해 필요!
      + Java EE(Enterprise Edition) - 서버용 애플리케이션 개발 에디션   
        : 서버용 애플리케이션을 개발하기 위한 도구, 라이브러리 API 정의  
      
      + JDK(Java Development kit), JRE(Java Runtime Enviroment), JVM(Java Virtual Machine) 차이  
        - 요약  
          - JDK = JRE + @  
            ```
            JVM = 자바 소스코드로부터 만들어지는 자바 바이너리 파일(.class)을 실행
            JDK = 읽기/쓰기 전용
            JRE = 읽기 전용
            ```   
        - JVM(Java Virtual Machine)  
          - 자바 소스코드로부터 만들어지는 자바 바이너리 파일(.class)을 실행할 수 있음  
          - 플랫폼에 의존적이다. 즉 `리눅스의 JVM과 윈도우즈의 JVM은 다름`  
            단, 컴파일된 바이너리 코드는 어떤 JVM에서도 동작시킬 수 있다.  
          - 역할  
            ```
             - 바이너리 코드를 읽는다.  
             - 바이너리 코드를 검증한다.  
             - 바이너리 코드를 실행한다.  
             - 실행환경(Runtime Environment)의 규격을 제공한다. (필요한 라이브러리 및 기타파일)  
            ```  
            
        - JRE(Java Runtime Enviroment)  
          - 컴파일된 자바 프로그램을 실행시킬 수 있는 자바 환경  
          - JVM이 자바 프로그램을 동작시킬 때 필요한 라이브러리 파일들과 기타 파일들을 가지고 있음  
          - JVM의 실행환경을 구현했다고 할 수 있다  
          - 자바 프로그램을 실행시키기 위해선 JRE를 반드시 설치해야함  
          - 하지만 `자바 프로그래밍 도구는 포함되어있지 않음`  
        
        - JDK(Java Development kit)  
          - 자바 프로그래밍시 필요한 컴파일러 등 포함  
          - 개발을 위해 필요한 도구(javac, java등)들을 포함  
          - JDK를 설치하면 JRE도 같이 설치가 된다  
          - 즉 `JDK = JRE + @` 라고 생각하면 됨  
        
    * 멀티 스레드(Multi-Thread)를 쉽게 구현 가능
      + 스레드 생성 및 제어와 관련된 라이브러리 API 제공  
      
    * 동적 로딩(Dynamic Loading) 지원
      + 객체가 필요한 시점에 클래스를 동적 로딩해서 객체 생성 -> 유지보수를 쉽고 빠르게 진행 가능  
      
    * 오픈 소스 라이브러리 풍부   

## Reference   
  - 신용권, 이것이 자바다, 한빛미디어(2019)  
  - [gooGid JDK와 JRE의 차이점](https://goodgid.github.io/Java-JDK-JRE/)  
  - [점프 투 자바 JVM, JDK, JRE 차이](https://wikidocs.net/257)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
