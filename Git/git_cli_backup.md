# Git CLI Backup
## 목차
  1. [수업의 목표와 용어정리](#1-수업의-목표와-용어정리)  
  1-1. [목표](#1-1-목표)  
  1-2. [용어](#1-2-용어)  
  2. [Git hosting](#2-Git-hosting)  
  2-1. [정리](#2-1-정리)  
  3. [저장소 생성](#3-저장소-생성)  
  3-1. [정리](#3-1-정리)  
  4. [공부 방향](#4-공부-방향)  
  4-1. [정리](#4-1-정리)  
  5. [원격 저장소와 연결](#5-원격-저장소와-연결)  
  5-1. [정리](#5-1-정리)  
  5-2. [명령어](#5-2-명령어)  
***
### 1. 수업의 목표와 용어정리
  - #### 1-1. 목표  
    - git hosting service를 통한 backup

  - #### 1-2. 용어  
    * Local Repository  
    
    * Remote Repository  
    
    * Push  
    
    * Pull  
    
    * CLONE  
    
    * work-flow 이미지  
    <p align="center"><img src="/img/Git/basic-remote-workflow.png" width="70%" height="60%" title=git workflow 이미지"></img></p>

### 2. Git hosting
  - #### 2-1. 정리
    * GitHub과 GitLab을 사용해서 진행

    * GitHub
      ```
      Framework is open-source 
      [서비스 자체가 오픈소스라서 서버에 직접설치가 가능한가?]
      No
      
      Open-source repositories
      [오픈소스 프로젝트가 무료인가?]
      Yes
      
      Space(GB)
      [용량]
      Unlimited
      
      Free private repositories
      [비공개 저장소를 무료제공하는가? (매우중요)]  
      No
      ```
    * GitLab
      ```
      Framework is open-source
      [서비스 자체가 오픈소스라서 서버에 직접설치가 가능한가?]
      Yes

      Open-source repositories
      [오픈소스 프로젝트가 무료인가?]
      Yes

      Space(GB)
      [용량]
      Unlimited

      Free private repositories
      [비공개 저장소를 무료제공하는가? (매우중요)]
      Unlimited projects, unlimited collaborators
      ```
### 3. 저장소 생성
  - #### 3-1. 정리
    * 진행과정
      1. GitHub, GitLab 홈페이지 들어가기  
          [GitHub](https://github.com/) / [GitLab](https://about.gitlab.com/)    
       
      2. 회원 가입 후 저장소 생성  
          GitHub    
          `New repository로 생성`      
          
          GitLab  
          `New project로 생성(Blank project)`  
      
### 4. 공부 방향
  - #### 4-1. 정리
    * 내용 정리
      1. 궁금증  
          `어떻게 지역저장소와 원격저장소를 연결할것인가?`  
          `어떻게 원격저장소에서 지역저장소로 가져올수 있나?`  
     
      2. 그럼 어떻게 버전을 어떻게 주고 받을 것인가?  
          `통신을 사용해서`  
            
          HTTP   
          - 보안으로 조금 부족하고 불편할 수 있음, 쉽게 할 수 있음  
            [우리가 이 강의에서 배울것]    
            
          SSH 
          - 보안적으로 훨씬 강력하고 훨씬 편리함 근데 배울 내용이 많음  
   
### 5. 원격 저장소와 연결
  - #### 5-1. 정리
    * 진행과정
      1. 연결하고자하는 지역저장소로 이동  
        
      2. GitHub 또는 GitLab 원격저장소에 접속  
          GitHub / GitLab  
          ```
          ... or push an exostong repository from the command line  
          이미 존재하고 있는 저장소를 CLI를 사용하여 업로드 하는 방법  
          ```  
      3. 원격저장소와 지역저장소 연결  
          `git remote add [https 주소에 해당되는 원격저장소 별명] [https 주소 복사]`  
            
          참고  
          ```
          원격 저장소 별명은 보통 기본적인 원격저장소는 origin(관습적으로 정해짐)  
          하나의 지역저장소에는 여러개의 원격저장소가 연결될 수 있음  
          각각의 원격저장소마다 별명을 붙여 쉽게 접근할 수 있도록 함, 알리아스 너낌  
          ```    
      4. 원격 저장소 연결확인  
          `git remote`  
          : 등록된 원격저장소 별명 출력  
            
          `git remote -v`  
          : 등록된 원격저장소 별명, https 주소 출력  
        
  - #### 5-2. 명령어
    * git remote
      ```
      프로젝트의 리모트(원격) 저장소를 관리하는 명령어
      
      git remote add [https 주소에 해당되는 원격저장소 별명] [https 주소 복사] : 지역 저장소와 원격 저장소 연결 
      git remote : 등록된 원격저장소 별명 출력  
      git remote -v : 등록된 원격저장소 별명, https 주소 출력  
      ```  
## Reference   
  - [생활코딩 GIT CLI](https://opentutorials.org/course/3841)
  - [kbss27-wiki git workflow](https://kbss27.github.io/2017/09/15/gitworkflow/) 
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
