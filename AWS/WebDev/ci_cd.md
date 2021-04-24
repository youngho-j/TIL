# CI & CD 내용 정리

## 목차
1. [CI & CD](#1-ci--cd)  
1-1. [CI](#1-1-ci)  
1-2. [CD](#1-2-cd)  
1-3. [주의할 점](#1-3-주의할-점)    
1-4. [앞으로의 전체 과정](#1-4-앞으로의-전체-과정)   
1-5. [Reference](#1-5-reference)  
2. [Travis CI 연동하기](#2-travis-ci-연동하기)  
2-1. [Travis CI](#2-1-travis-ci)  
2-2. [과정](#2-2-과정)  
2-3. [Reference](#2-3-reference)  
3. [Travis CI 와 AWS S3 연동하기](#3-travis-ci-와-aws-s3-연동하기)  
3-1. [AWS S3](#3-1-aws-s3)  
3-2. [Travis CI와 S3 연동](#3-2-travis-ci와-s3-연동)  
3-3. [AWS Key 발급](#3-3-aws-key-발급)  
3-4. [Travis CI에 키 등록](#3-4-travis-ci에-키-등록)  

***
### 1. CI & CD
  - #### 1-1. CI
    - CI(Continuous Integration - 지속적 통합)  
    - VCS(코드 버전 관리) 시스템에 PUSH가 되면 자동으로 테스트와 빌드가 수행되어 `안정적인 배포 파일을 만드는 과정`  
  - #### 1-2. CD
    - CD(Continuous Deployment - 지속적 배포)  
    - CI의 빌드 결과를 자동으로 운영 서버에 무중단 배포까지 진행되는 과정   

  - #### 1-3. 주의할 점
    - 단순히 CI 도구를 도입했다고 해서 CI를 하는 것은 아님  
    - `테스팅 자동화`가 중요!  
    - 지속적인 통합을 위해 프로젝트가 완전한 상태임을 보장하는 `테스트코드가 꼭 구현`되어야함  
  
  - #### 1-4. 앞으로의 전체 과정  
    ![image](https://user-images.githubusercontent.com/65080004/115816350-af85c900-a433-11eb-8c8a-1d31e50612e1.png)  

  - #### 1-5. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [기억보단 기록을 6. TravisCI & AWS CodeDeploy로 배포 자동화 구축하기](https://jojoldu.tistory.com/265)  

### 2. Travis CI 연동하기
  - #### 2-1. Travis CI
    - 깃허브에서 제공하는 무료 CI 서비스
    - 참고!
      ```
      Travis-ci.com으로 가입해서 사용해야함!
      Travis-ci.org 2020년에 Travis-ci.com으로 통합됨
      ```
      
  - #### 2-2. 과정 
    - 흐름
      ```
      1. Travis-ci.com에 GitHub 계정으로 가입 후 저장소 활성화
      
      2. 프로젝트 설정은 yml(YAML - 야믈) 파일로 설정함  
         `YAML`이란? JSON에서 괄호를 제거한 것  
      
      3. 프로젝트 내 build.gradle과 같은 위치에 yml 파일 생성 
      
      4. 코드 추가 (빌드가 실패하는 경우도 있으니, `chmod +x 파일명` 으로 권한을 추가해주면 됨)  
      
      5. master branch에 commit&push 후 CI 저장소 확인
      
      6. 완료 될 경우 등록한 이메일로 성공 여부 전달확인 가능
      ```

  - #### 2-3. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [기억보단 기록을 6. TravisCI & AWS CodeDeploy로 배포 자동화 구축하기](https://jojoldu.tistory.com/265)  

### 3. Travis CI 와 AWS S3 연동하기
  - #### 3-1. AWS S3
    - AWS에서 제공하는 `일종의 파일 서버`
    - 이미지 파일을 비롯한 정적 파일들을 관리 또는 배포 파일들을 관리하는 등의 기능 제공  
  
  - #### 3-2. Travis CI와 S3 연동
    - 왜 Travis CI와 CodeDeploy를 바로 연결하지 않는가?  
    - CodeDeply는 저장 기능이 없어 CodeDeploy가 배포 파일을 가져갈 수 있도록  
      보관할 공간이 필요  
    - 웬만하면 `빌드와 배포는 분리하는 것을 추천` - 빌드 없이 배포시 대응하기 어렵  
  
  - #### 3-3. AWS Key 발급
    - Key를 발급받는 이유?  
    - 일반적으로 AWS 서비스에 외부 서비스 접근불가!
    - 따라서, 접근 권한을 가진 Key를 생성하여 접근 해야함!
    - AWS에서는 `IAM(Identity and Access Management)` - 인증관련 기능(서비스의 접근 방식과 권한 관리)  
    - 과정
      ```
      1. aws 콘솔에서 iam 검색
      
      2. 우측 사용자 탭 클릭
      
      3. 사용자 이름 및 엑세스 유형(프로그래밍 방식), 권한 설정(기존 정책...) 선택
      
      4. 권한 설정 후 s3full / codedeployf 검색하여, 권한 추가
      
      5. 태그 key 부분에 Name 지정 후 값을 작성
      
      6. 설정 항목 확인 후 엑세스 키와 비밀 엑세스 키 기억해두기(Travis CI에서 사용될 키)
      ```
  
  - #### 3-4. Travis CI에 키 등록
    - 과정
      ```
      1. Travis CI 설정 화면으로 이동(settings)
      
      2. Environment Variables 하단에 IAM에서 발급받은 엑세스, 비밀 엑세스 키 등록
      
      3. 등록 시 입력한 이름을 쉘스크립트에서 사용하듯이 사용 가능 ($AWS_ACCESS_KEY, $AWS_SECRET_KEY) 
      ```

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
