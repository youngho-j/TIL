# EC2 관련 내용 정리

## 목차
1. [EC2에 프로젝트 클론 후 테스트 검증시 denied 해결 방법](#1-ec2에-프로젝트-클론-후-테스트-검증시-denied-해결-방법)  
1-1. [EC2에 프로젝트 clone](#1-1-ec2에-프로젝트-clone)  
1-2. [프로젝트 코드 검증](#1-2-프로젝트-코드-검증)  
1-3. [Reference](#1-3-reference)  

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

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
