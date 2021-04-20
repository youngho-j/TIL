# EC2 관련 내용 정리

## 목차
1. [EC2에 프로젝트 클론 후 테스트 검증시 denied 해결 방법](#1-ec2에-프로젝트-클론-후-테스트-검증시-denied-해결-방법)  
1-1. [EC2에 프로젝트 clone](#1-1-ec2에-프로젝트-clone)  
1-2. [프로젝트 코드 검증](#1-2-프로젝트-코드-검증)  
1-3. [Reference](#1-3-reference)  
2. [EC2 프로젝트 배포시 Error: Unable to access jarfile 해결하기](#2-ec2-프로젝트-배포시-error-unable-to-access-jarfile-해결하기)  
2-1. [1차 시도](#2-1-1차-시도)  
2-2. [2차 시도](#2-2-2차-시도)  
2-3. [Reference](#2-3-reference)  
3. [EC2 소셜 로그인 기능 추가 중 발생한 오류 해결하기](#3-ec2-소셜-로그인-기능-추가-중-발생한-오류-해결하기)  
3-1. [AWS 보안 그룹 변경 후 EC2 도메인으로 접속하기](#3-1-aws-보안-그룹-변경-후-ec2-도메인으로-접속하기)    
3-2. [구글, 네이버 서비스에 도메인 등록 후 소셜로그인 하기](#3-2-구글-네이버-서비스에-도메인-등록-후-소셜로그인-하기)    
3-3. [Reference](#3-3-reference)  

***
### 1. EC2에 프로젝트 클론 후 테스트 검증시 denied 해결 방법
  - #### 1-1. EC2에 프로젝트 clone
    ```
    1. 윈도우 환경의 경우 putty를 통해 EC2에 접속 

    2. git 설치
       `sudo yum install git` 명령어를 통해 설치
    
    3. 설치 완료 후 git version 확인 
       `git --version`
       
    4. 프로젝트를 저장할 디렉토리 생성
       `mkdir ~/app && mkdir ~/app/step1`  
    
    5. 생성된 디렉토리로 이동
       `cd ~/app/step1`
       
    6. 프로젝트를 내려받고자 하는 원격 저장소의 https 주소를 복사하여 clone 진행
       `git clone (복사한 주소)`  
    
    7. clone 작업이 완료되면 파일 확인
       `ll` - git bash의 ls -al과 같음
    ```
  - #### 1-2. 프로젝트 코드 검증 
    - `./gradlew test` 명령어 사용하여 코드 검증  
    
      ```
      참고!
      Gradle을 설치하지 않았는데 어떻게 Gradle Task를 실행 할 수 있는가?
     
      프로젝트 내부에 포함된 gradlew 파일 때문에 
      환경 또는 버전이 다른 경우에도 해당 프로젝트에 한해 gradle을 쓸 수 있도록 지원
     
      gradlew - gradle을 쓸 수 있도록 지원하는 Wrapper 파일
      ```
     
    - 테스트 실패  
      ![image](https://user-images.githubusercontent.com/65080004/114984055-4995c080-9ecc-11eb-98a4-e0994bc143d4.png)  
     
      원인 : 실행 권한이 없음
     
      해결 방법 : 'chmod +x ./gradlew' 명령어를 통해 실행 권한을 주면 됨! 
   
    - 테스트 통과  
      ![image](https://user-images.githubusercontent.com/65080004/114984167-6a5e1600-9ecc-11eb-8aee-87afe81c099c.png)  

  - #### 1-3. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  

### 2. EC2 프로젝트 배포시 Error: Unable to access jarfile 해결하기
  - #### 2-1. 1차 시도
    - './deploy.sh' 명령어를 통해 실행시 출력문이 두번 출력되고, pid가 출력되지 않는 경우가 발생 
      ```
      설정한 properties 파일과 프로젝트내 파일이 잘 못 된거 아닌가 생각하고, 파일을 살펴보았으나 다른 오타는 없었음

      쉘 스크립트 파일인 deploy.sh 파일을 열어보았을 때도 오타는 보이지 않았음, 스크립트 실행시 생성되는 nohup.out을 살펴보았으나 

      pid가 출력되지 않았고, 에러로 추측되는 부분은 콘솔에서 아래 코드 말고는 없었음

      Deprecated Gradle features were used in this build, making it incompatible with Gradle 5.0.
      Use '--warning-mode all' to show the individual deprecation warnings.
      See https://docs.gradle.org/4.10.2/userguide/command_line_interface.html#sec:command_line_warnings

      해결 : deploy.sh파일을 여러번 살펴보다가 방향키로 내리다 보니 중복된 코드가 붙여져 있었음, 해당 파일 생성 당시 오류가나서 Edit모드로   
       
            수정시 붙여넣기가 중복되어 두번 출력이 된듯, 중복되는 내용을 지우고 실행하니 두번 출력과 pid가 출력되는 부분은 해결됐으나,
            
            curl 명령어로 실행시 실행 안됨
      ```
  - #### 2-2. 2차 시도
    - Build successful이 뜨나 nohup.out vim 창에 Error: Unable to access jarfile 에러 발생
      ```
      빌드 성공 후 nohup.out 파일에 Error: Unable to access jarfile /home/ec2-user/app/application-oauth-db.properties 에러 발생 결과 출력
      
      해당 파일의 위치 및 파일 내용 오타를 검토했으나 해결되지 않음, deploy.sh nohup java 내용을 수정(이어붙이기, 띄어쓰기 검사 등)해보았으나 실패
      
      해결 : shell script에 Bash 명령어를 아래와 같이 수정하여 성공, 명령어 작성 당시 공백이 포함되어 적용이 안된 듯
             (`\` - 명령어를 한줄에 다 쓸 수 없어 다음줄로 이어 적을 때 첫줄의 마지막에 붙여주는 명령어, 사용시 색이 변해야 적용된 것, \ 다음에 공백이 오면 안됨)
           nohup java -jar \
            -Dspring.config.location=classpath:/application.properties,/home/ec2-user/app/application-oauth.properties,/home/ec2-user/app/application-real-
            db.properties,classpath:/application-real.properties \
            -Dspring.profiles.active=real \
            $REPOSITORY/$JAR_NAME 2>&1 &

      ```
  - #### 2-3. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [jojoldu 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 repo issue](https://github.com/jojoldu/freelec-springboot2-webservice/issues)  
    - [개발자스럽다 Bash 입문자를 위한 핵심 요약](https://blog.gaerae.com/2015/01/bash-hello-world.html)  

### 3. EC2 소셜 로그인 기능 추가 중 발생한 오류 해결하기
  - #### 3-1. AWS 보안 그룹 변경 후 EC2 도메인으로 접속하기  
    ```
    1. AWS 접속 후 EC2 네트워크 및 보안 탭에서 보안 그룹탭으로 이동
    
    2. EC2 8080 포트 열기  
    
    3. 퍼블릭 DNS에 ':8080' 붙여서 브라우저에서 접속
    
    이 단계까지는 쉽게 마무리 가능했음.. 문제는 다음 도메인 등록에서 시작.. 
    ```
  
  - #### 3-2. 구글, 네이버 서비스에 도메인 등록 후 소셜로그인 하기
    ```
    1. 구글에 도메인 등록하기
    
    1-1. 구글 웹 콘솔 접속 후 api 및 서비스 탭에 OAuth 동의 화면 클릭
    
    1-2. 앱 수정 버튼 클릭
    
    1-3. 승인된 도메인에 'http://' 없이 퍼블릭 DNS 등록
    
    1-4. api 및 서비스 탭에 사용자 인증 정보 탭 클릭
    
    1-5. OAuth 2.0 클라이언트 ID 클릭 후   
         승인된 리디렉션 URI에 'http:// + (퍼블릭 DNS) + :8080/login/oauth2/code/goole' 추가하여 퍼블릭 DNS 등록  
    
    1-6. EC2 DNS 주소로 이동시 화면 정상 출력 확인 
    
    1-7. 구글 로그인 버튼 클릭시 화면 멈춰있는 현상 발생
    
    1-8. EC2에서 다시 빌드 후 접속 후 F12로 확인해보니 500 에러 
    
    1-9. 지금까지 했던 작업 오타 체크 및 비슷한 현상 검색.. 길었다.. ㅠ
    
    1-10. 다시 빌드 후 nohup.out에 BadSQL 에러 확인.. (드디어 빛을 봄 ㅠ)
    
    1-11. RDS에 쿼리를 이용하여 누락된 SESSION_ATTRIBUTE 테이블과 오타난 인덱스 제거 후 재등록
          (ALTER TABLE 테이블명 DROP INDEX 인덱스명;)  
    
    1-12. 정상 실행 확인(드디어 완료!)
    
    2. 네이버에 도메인 등록하기  
    
    2-1. 네이버 개발자 센터 접속 후 상단 Application 탭 클릭
    
    2-2. Client ID 클릭 후 API 설정 탭 클릭
          
    2-3. 로그인 오픈 API 서비스 환경에서  
         서비스 URL 등록(http:// + 퍼블릭DNS), 
         Callback URL(http:// + 퍼블릭DNS + :8080/login/oauth2/code/naver) 수정 및 추가  
         
    2-4. 정상 실행 확인(마무리)
    ```

  - #### 3-3. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [jojoldu 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 repo issue](https://github.com/jojoldu/freelec-springboot2-webservice/issues)  
    - [It is my Style MySQL인덱스 생성, 조회, 삭제](https://creds.tistory.com/163)  
    - [기억보단 기록을 인덱스 정리 및 팁](https://jojoldu.tistory.com/243)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
