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
3-5. [S3 버킷 생성](#3-5-s3-버킷-생성)  
3-6. [.travis.yml 코드 추가](#3-6-travisyml-코드-추가)   
3-7. [EC2에 IAM 역할 추가하기](#3-7-ec2에-iam-역할-추가하기)  
3-8. [Codedeploy 에이전트 설치](#3-8-codedeploy-에이전트-설치)  

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

  - #### 3-5. S3 버킷 생성
    - S3(Simple Storage Service) - 일종의 파일 서버
    - `파일들을 저장하고 접근 권한을 관리, 검색 등을 지원`하는 파일서버의 역할  
    - 보통 게시글 작성시 첨부파일 등록을 구현시 많이 이용
    - 여기서는 Build 파일을 저장하기 위해 사용
    - 과정
      ```
      1. AWS 콘솔에서 S3 검색 후 버킷 만들기 클릭
      
      2. 버킷명 작성(저장하고자 하는 것을 떠올릴 수 있도록 연관지어 짓는 것이 나중에 알아보기 편함)  
         ex) build 파일 저장, springboot-build 등  
      
      3. 퍼블릭 액세스 설정 - 꼭 모든 차단으로 설정해야함  
         왜? 실제 서비스를 한다고 했을때 퍼블릭으로 설정시 누구나 다 내려받기 가능하므로 코드, 설정값, 주요 키값들이 유출될 수 있음  
         
         그럼 모든 차단인데 S3 서버에 어떻게 접근 할 수 있나?  
         아까 IAM 사용자로 등록을 해놓았으므로, 해당 키를 사용하여 접근이 가능
         
      4. 생성
      ```  
  
  - #### 3-6. .travis.yml 코드 추가
    - Travis CI에서 빌드하여 만든 Jar 파일을 S3로 전달하는 코드 추가
    - before_deploy 코드를 통해 deploy 명령어 실행 전 수행할 코드 추가  
      참고! CodeDeploy는 `Jar 파일 인식 못함` 따라서, Jar + 기타 설정 파일을 모아 압축  
    - deploy 코드를 통해 `외부 서비스와 연동될 행위들을 선언`  
    - 깃허브에 PUSH 후 빌드 성공시 S3 버킷에 업로드 성공을 확인하면 연동이 잘 되었는지 확인 가능

  - #### 3-7. EC2에 IAM 역할 추가하기
    - 해당 작업을 하는 이유? 
    - 배포 대상인 `EC2가 CodeDeploy를 연동 받을 수 있도록 하기 위해`  
    - 과정
      ```
      1. AWS 콘솔에서 IAM 검색
      
      2. 좌측 역할 탭 클릭 후 역할 만들기 클릭
         왜 사용자가 아닌 역할로 만드는가? EC2 즉, AWS 서비스에서만 사용할 것이기 떄문에 역할로 처리  
      
      3. AWS 서비스의 EC2 선택
      
      4. 정책에서 EC2RoleForA 검색하여 AmazonEc2RoleforAWS-CodeDeploy 선택
      
      5. 키는 Name 값은 원하는 이름으로 작성(알아볼 수 있도록)
      
      6. 최종 확인 후 완료
      
      7. 역할을 EC2 서비스에 등록

      8. EC2 검색 후 좌측 인스턴스 탭 클릭하여 이동

      9. 해당 인스턴스 우클릭 -> 보안 -> IAM 역할 수정 클릭

      10. 선택 완료 후 상단 인스턴스 상태 클릭하여 인스턴스 재부팅
      ```
      
    - IAM 역할과 사용자의 차이  
      |역할|사용자|  
      |---|---|  
      | - AWS 서비스에만 할당 할 수 있는 권한| - AWS 서비스 외에 사용할 수 있는 권한|  
      | - EC2, CodeDeploy 등| - 로컬 PC, IDC 서버 등|  
      
  - #### 3-8. CodeDeploy 에이전트 설치
    - 설치 하는 이유?
    - `CodeDeploy 요청을 받기 위해`
    - 과정
      ```
      1. EC2 접속 - (windows의 경우 putty를 통해 접속)
      
      2. aws s3 cp s3://aws-codedeploy-ap-northeast-2/latest/install .--region ap-northeast-2 명령어 실행  
         성공시 download ~ to ./install 이라는 결과 뜸
         참고! 설치 중 /usr/bin/env:ruby: ~ 에러 뜰 경우 sudo tum install ruby 명령어로 ruby 언어를 설치해 주면 됨 
      
      3. 실행 권한 추가 chmod +x ./install
      
      4. 설치 sudo ./install auto
      
      5. Agent 정상 실행 확인 sudo service codeploy-agent status
         The AWS CodeDeploy agent is running as PID ~ 메세지 출력시 정상  
      ```

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
