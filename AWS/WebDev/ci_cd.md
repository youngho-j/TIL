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
3-7. [Reference](#3-7-reference)  
4. [Travis CI와 AWS S3, CodeDeploy 연동하기](#4-travis-ci와-aws-s3-codedeploy-연동하기)  
4-1. [EC2에 IAM 역할 추가하기](#4-1-ec2에-iam-역할-추가하기)  
4-2. [Codedeploy 에이전트 설치](#4-2-codedeploy-에이전트-설치)  
4-3. [CodeDeploy를 위한 권한 생성](#4-3-codedeploy를-위한-권한-생성)  
4-4. [CodeDeploy 생성](#4-4-codedeploy-생성)  
4-5. [Travis, S3, CodeDeploy 연동](#4-5-travis-s3-codedeploy-연동)  
4-6. [Reference](#4-6-reference)  
5. [배포 자동화 구성](#5-배포-자동화-구성)  
5-1. [현재 구현 상황](#5-1-현재-구현-상황)  
5-2. [deploy.sh 파일 추가](#5-2-deploysh-파일-추가)  
5-3. [.travis.yml 파일 수정](#5-3-travisyml-파일-수정)  
5-4. [appspec.yml 파일 수정](#5-4-appspecyml-파일-수정)  
5-5. [설정 완료 후 GitHub로 Commit & PUSH](#5-5-설정-완료-후-github로-commit--push)  
5-6. [CodeDeploy 로그 확인](#5-6-codedeploy-로그-확인)  
5-7. [Travis CI 배포 자동화 마무리](#5-7-travis-ci-배포-자동화-마무리)  
5-8. [Reference](#5-8-reference)  

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

  - #### 3-7. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [기억보단 기록을 6. TravisCI & AWS CodeDeploy로 배포 자동화 구축하기](https://jojoldu.tistory.com/265)  
  
### 4. Travis CI와 AWS S3, CodeDeploy 연동하기
  - #### 4-1. EC2에 IAM 역할 추가하기
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
      
  - #### 4-2. CodeDeploy 에이전트 설치
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

  - #### 4-3. CodeDeploy를 위한 권한 생성
    - 권한 생성을 하는 이유?
    - Codedeploy에서 EC2에 접근하기 위해 권한이 필요함
    - 과정
      ```
      1. AWS 콘솔에서 IAM 검색

      2. 좌측 역할 탭에서 역할 만들기 클릭
      
      3. AWS 서비스 중 CodeDeploy 선택(권한이 하나 밖에 없음 - AWSCodeDeployRole)
      
      4. 태그 추가 키 - Name, 값은 본인이 알아볼 수 있도록 작성
      ```
      
   - #### 4-4. CodeDeploy 생성
    - CodeDeploy - AWS의 배포 서비스 / 대체제가 없음
    - 과정
      ```
      1. AWS 콘솔에서 CodeDeploy 검색
      
      2. 애플리케이션 생성 버튼 클릭
      
      3. 애플리케이션 이름, 컴퓨팅 플랫폼(EC2/온프레미스) 선택
      
      4. 애플리케이션에서 배포 그룹 생성하기 버튼 클릭
      
      5. 배포 그룹 이름 지정, 서비스 역할 선택(CodeDeploy IAM 선택)
      
      6. 배포 유형은 현재 위치 선택 (배포할 서비스 2대 이상이면 블루/그린 선택)
      
      7. 환경 구성에서는 Amazon EC2 인스턴스 체크
      
      8. 태그 그룹에서는 키에 Name 값에 사용하는 EC 인스턴스 이름 작성
      
      9. 배포 구성에는 CodeDeployDefaultAllAtOnce (한번에 전체 배포)
      
      10. 로드 밸런싱 비활성화 
      ```
  - #### 4-5. Travis, S3, CodeDeploy 연동
    - 1. EC2 설정
         - 넘겨받을 zip 파일을 저장할 디렉토리 생성
         - 과정
           ```
           1. EC2 접속
           
           2. S3에서 넘겨 받은 zip 파일을 저장할 디렉토리 생성
           
           3. mkdir ~/app/step2 && mkdir ~/app/step2/zip (&& 옵션은 연속해서 명령어 사용가능하도록 함)
           ```
    - 2. Travis CI 설정
         - .travis.yml 파일로 설정
         - Build 완료시 S3로 zip 파일 전송
         - TravisCI가 CodeDeploy도 실행시키도록 설정 코드 추가
         - 코드(codedeploy 실행 코드 추가)
           ```
           deploy:
           ~
             - provider: codedeploy
               access_key_id: $AWS_ACCESS_KEY #Travis repo setting에 설정된 값
               secret_access_key: $AWS_SECRET_KEY #Travis repo setting에 설정된 값

               bucket: springboot-build #s3 버킷
               key: springboot-webservice.zip #빌드파일을 압축해서 전달

               bundle_type: zip #압축확장자
               applicationn: springboot-webservice # 웹 콘솔에서 등록한 CodeDeploy 애플리케이션

               deplyment_group: springboot-webservice-group # 웹 콘솔에서 등록한 CodeDeploy 배포 그룹

               region: ap-northeast-2
               wait-until-deployed: true
           ```

    - 3. CodeDeploy 설정
         - appspec.yml 파일로 설정
         - 받은 zip 파일을 /home/ec2-user/app/step2/zip/(EC2)에 복사 한 뒤 압축을 풀 예정
         - 코드
           ```
           # AWS CodeDeploy 설정
           # version - CodeDeploy 버전 / 0.0 외 다른 버전 사용시 오류 발생
           version: 0.0
           os : linux
           files :
           # CodeDeploy에서 전달해준 파일 중(여기선 전체) destination으로 이동시킬 대상 지정
            - source : /
              destination: /home/ec2-user/app/step2/zip/
              overwrite : yes

           # CodeDeploy에서 EC2 서버로 넘겨준 파일들을 모두 ec2-user 권한을 갖도록 한다.
           permissions:
            - object: /
              pattern: "**"
              owner: ec2-user
              group: ec2-user

           # 배포 단계에서 실행할 명령어 지정
           hooks:
            ApplicationStart:
              - location : deploy.sh
                timeout: 60
                runas: ec2-user
           ```
     - 4. 연동 확인
          - 과정
            ```
            1. 프로젝트 Commit & PUSH
            
            2. Travis 콘솔로 이동하여 배포 수행 확인
            
            3. 성공시 EC2에 접속하여 'cd /home/ec2-user/app/stp2/zip' 디렉토리 경로로 이동
            
            4. 'll' 명령어로 파일 목록 확인
            
            5. 파일이 복제된 것을 확인하면 연동이 완료된것을 알 수 있음
            ```
            
  - #### 4-6. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [기억보단 기록을 6. TravisCI & AWS CodeDeploy로 배포 자동화 구축하기](https://jojoldu.tistory.com/265)  

### 5. 배포 자동화 구성
  - #### 5-1. 현재 구현 상황
    - Travis CI, S3, CodeDeploy 연동까지 구현
    - 구현된 것을 기반으로 `Jar 배포하여 실행`하는 것이 목표!
  
  - #### 5-2. deploy.sh 파일 추가
    - EC2에 CodeDeploy로 받은 파일을 실행시키는 배포 스크립트(deploy.sh) 생성
    - 과정
      ```
      1. step2 환경에서 실행될 deploy.sh 생성(프로젝트 우클릭 scripts 디렉토리 생성 후 그 안에 생성)  
      2. git pull을 통해 직접 빌드했던 부분 제거(Travis CI가 빌드를 대신 하므로)  
      3. Jar 파일에 실행 권한이 없으므로 nohup으로 실행할 수 있도록 권한 부여(chmod +x $JAR_NAME)
      4. $JAR_NAME > $REPOSITORY/nohup.out 2>&1 &  
         nohup 실행시 CodeDeploy는 무한 대기 / nohup.out 파일을 표준 입출력용으로 별도 사용
         이렇게 사용하지 않을 경우 nohup.out 파일이 생성되지 않고, CodeDeploy 로그에 표준 입출력이 표시됨!
      ```
  - #### 5-3. .travis.yml 파일 수정
    - 프로젝트의 모든 파일을 zip으로 만들때 실제 필요한 파일은 `Jar, appspec.yml, 배포관련 스크립트들` 뿐임
    - 따라서 이외는 포함시키지 않도록 코드를 작성
    - 코드
      ```
      before_deploy:
        # 존재하지 않는 중간의 before-deploy 디렉토리를 생성
        # 왜 디렉토리를 생성하는가? 
        # Travis CI는 S3로 특정파일만 업로드가 안됨.. '디렉토리 단위로만 업로드가 가능'
        - mkdir -p before-deploy
        
        # before-deploy에 파일 복사
        - cp scripts/*.sh before-deploy/
        - cp appspec.yml before-deploy/
        - cp build/libs/*.jar before-deploy/
        
        # before-deploy로 이동 후 전체 압축
        - cd before-deploy && zip -r before-deploy *

        # 상위 디렉토리로 이동 후 deploy 디렉토리 생성
        - cd ../ && mkdir -p deploy
        
        # before-deploy.zip을 deploy 디렉토리로 이동
        - mv before-deploy/before-deploy.zip deploy/springboot-webservice.zip
      ```
      
  - #### 5-4. appspec.yml 파일 수정
    - CodeDeploy 명령 담당
    - location, timeout, runas의 들여쓰기 주의! 잘못되면 배포 실패함
    - 코드
      ```
      ~
      # CodeDeploy에서 EC2 서버로 넘겨준 파일들을 모두 ec2-user 권한을 갖도록 한다.
      permissions:
        - object: /
          pattern: "**"
          owner: ec2-user
          group: ec2-user

      # 배포 단계(ApplicationStrat)에서 실행할 명령어 지정
      # ApplicationStart 단계에서 deploy.sh를 ec2-user 권한으로 실행
      # timeout - 무한정 기다릴 수 없으므로 지정
      hooks:
        ApplicationStart:
          - location : deploy.sh
            timeout: 60
            runas: ec2-user
      ```
  - #### 5-5. 설정 완료 후 GitHub로 Commit & PUSH
    - 성공시 문구
      ```
      ~
      Logging in with Access Key : ~
      ~
      Deployment successful.
      ~ 
      Done. Your ~ with 0. 
      ```

  - #### 5-6. CodeDeploy 로그 확인
    - AWS가 지원하는 서비스에서 오류 발생시 로그 찾는 방법을 모르면 해결 어려움
    - CodeDeploy에 관한 로그는 `cd /opt/codedeploy-agent/deployment-root`에 있음(EC2에서 접근)
    - `ll` 명령어로 확인 가능 
    - 최상단 숫자, 영어 대시(-)가 있는 디렉토리 명 -> CodeDeploy ID  
      cd로 해당 디렉토리로 이동시 `배포한 단위별로 배포 파일 확인 가능`  
      배포파일이 정상적으로 들어 왔는지 확인 가능  
    - deployment-logs -> CodeDeploy 로그 파일  
      배포 내용 중 표준 입/출력 내용은 모두 여기에 있으며, 작성한 echo 내용도 모두 표기됨  
    
  - #### 5-7. Travis CI 배포 자동화 마무리
    - 현재 `Master 브랜치에 PUSH시 자동으로 EC2에 배포`됨  
    - 하지만, `배포하는 동안` 스프링 부트 프로젝트는 종료 상태가 됨 즉, `서비스 이용 불가`
    - 그렇다면 어떻게 배포하는 동안 서비스를 중지시키지 않고 서비스를 이용할 수 있을까?
    - 서비스 중단 없는 배포 -> `무중단 배포` 방법으로 진행

  - #### 5-8. Reference
    - 스프링 부트와 AWS로 혼자 구현하는 웹 서비스 - 이동욱 저  
    - [기억보단 기록을 6. TravisCI & AWS CodeDeploy로 배포 자동화 구축하기](https://jojoldu.tistory.com/265)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
