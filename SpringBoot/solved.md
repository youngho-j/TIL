# SpringBoot 노트

## 목차
1. [테스트 코드 한글 깨짐 현상해결하기](#1-테스트-코드-한글-깨짐-현상해결하기)  
1-1. [원인](#1-1-원인)  
1-2. [해결방법](#1-2-해결방법)  
1-3. [Reference](#1-3-reference)  
2. [localhost:8080 입력시 비밀번호 입력 창 뜨는 경우 해결하기](#2-localhost8080-입력시-비밀번호-입력-창-뜨는-경우-해결하기)  
2-1. [원인](#2-1-원인)  
2-2. [해결방법](#2-2-해결방법)  
2-3. [Reference](#2-3-reference)  
***
### 1. 테스트 코드 한글 깨짐 현상해결하기
  - #### 1-1. 원인
    - IntelliJ 에서 소스 파일을 읽고, 바이트 코드를 만드는 과정에서 한글 문자열 깨짐  
  
  - #### 1-2. 해결방법
    ```
    1. 메뉴 탭 Help 클릭
    2. 드롭다운 메뉴 중 Edit Custom VM Options 클릭
    3. -Dfile.encoding=UTF-8 추가
    4. IntelliJ 끄고 다시 실행
    5. 테스트 실행 
    ```
  
  - #### 1-3. Reference
    - [다람쥐의 개발 일상 블로그 인텔리제이(Intellij) 소스파일 및 테스트 결과 한글 깨짐](https://itchipmunk.tistory.com/421)  

### 2. localhost:8080 입력시 비밀번호 입력 창 뜨는 경우 해결하기
   - #### 2-1. 원인
     - Oracle DB에서 이미 8080 포트를 사용하고 있어 Tomcat 포트와 겹쳐 해당 현상이 나타남  
   
   - #### 2-2. 해결방법
     - tomcat의 포트 번호 변경
       ```
       1. tomcat 설치 경로로 들어가 conf 폴더 클릭
       2. server.xml 파일 열기
       3. '<Connector port="8080" protocol="HTTP/1.1" ...>' 에서 port 부분을 변경
       4. 접속 시도
       ```
     - Oracle 포트 번호 변경
       ```
       1. window + r 로 실행창 띄우기
       2. cmd 클릭
       3. sqlplus sys as sysdba 입력 후 엔터
       4. 오라클 설치시 입력했던 비밀번호 입력 후 접속
       
       4-1. 비밀번호를 잊었을 경우
       4-2. cmd 창에서 sqlplus /nolog 입력
       4-3. conn /as sysdba
       4-4. alter user system identufied by 새로운 암호
       4-5. alter user sys identified by 새로운 암호
       4-6. conn 아이디/변경한 비밀번호
       4-7. show user 로 계정 확인

       5. exec dbms_xdb.sethttpport(바꿀포트번호);
       6. select dbms_xdb.gethttpport() from dual; 로 한번 더 확인
       ```

  - #### 2-3. Reference
    - [메자곰localhost:8080 사용자 비밀번호 입력이라고 뜰 경우](https://technote-mezza.tistory.com/27)  
    - [JustOne 오라클 관리자계정 비밀번호 잊어버렸을때](https://nhs0912.tistory.com/49)  
    - [sj입니다 오라클 포트번호 변경방법](https://javawin.tistory.com/24)  
  


