# 자바 가상 기계(JVM)
  - 자바 프로그램을 이루고 있는 바이트 코드를 해석하고 실행할 수 있는 가상의 운영체제
    * 바이트 코드는 모든 JVM에서 동일한 실행 결과 보장, but JVM은 운영체제에 종속적(운영체제에 맞는 JVM 설치 필요)   
   <p align="center"> <img src="/img/Java/javaExecution.png" width="50%" height="40%" title="자바실행단계사진"></img></p>   
    
  ```    
  1. .java 파일(소스파일) 작성    
  2. 컴파일러(javac.exe)로 컴파일
  3. .class 파일(바이트 코드 파일) 생성
  4. JVM 구동 명령어(java.exe)에 의해 해석, 운영체제에 맞는 기계어로 번역   
  ```
  
## Reference   
  - 신용권, 이것이 자바다, 한빛미디어(2019)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
