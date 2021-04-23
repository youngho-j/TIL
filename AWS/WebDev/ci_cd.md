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

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/AWS/EC2/README.md "Go README.md")
