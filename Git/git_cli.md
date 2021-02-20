# Git CLI
## 목차
  1. [버전관리의 시작](#1-버전관리의-시작)  
  1-1. [저장소 만드는 법](#1-1-저장소-만드는-법)  
  1-2. [명령어](#1-2-명령어)  
  2. [버전의 생성](#2-버전의-생성)  
  2-1. [버전 만들어보기](#2-1-버전-만들어보기)   
  2-2. [여러개의 파일을 버전으로 만들기](#2-2-여러개의-파일을-버전으로-만들기)  
  2-3. [명령어](#2-3-명령어)  
***
### 1. 버전관리의 시작
  - #### 1-1. 저장소 만드는 법
    1. 원하는 디렉토리 위치에 폴더 생성  
        - 순서  
        pwd → cd → mkdir  
        
    2. 폴더 내부로 이동하여 git init을 통해 버전관리 시작 요청  
        - 순서  
        cd → git init .  
        
    3. 폴더 내부에 .git 폴더 생성 확인  
        - 순서  
        ls -al  
        - 절대로 .git 디렉토리를 지우면 안됨!!  
  
  - #### 1-2. 명령어  
    * pwd 
      ```
      현재 위치를 보여주는 명령어
      Ex) pwd  
      /c/Users/.../foldername
      ```
    * cd [이동할 디렉토리]
      ```
      디렉토리로 위치로 이동하게 해주는 명령어
      Ex) cd j:
      J 드라이브로 이동 후 pwd 입력 시 아래와 같이 나옴
      → /j
      
      상위 디렉토리로 이동
      Ex) cd ..
      ```
    * mkdir [폴더명]
      ```
      현재 위치에서 폴더를 생성해주는 명령어
      Ex) mkdir test → test라는 이름을 가진 폴더 생성
      ```
    * ls -al
      ```
      현재 디렉토리의 목록을 보여주는 명령어
      -al이라는 옵션은 모든 목록을 의미
      ```
    * git init 
      ```
      버전관리를 시작해달라는 명령어
      init - Initialize 초기화의 약자
      (공백). → 현재 디렉토리를 의미
      Ex) git init .
      ```
### 2. 버전의 생성
  - #### 2-1. 버전 만들어보기  
    <p align="center"><img src="/img/Git/git_3step.png" width="70%" height="60%" title="Git 3단계 이미지"></img></p>
    1. Working tree(Working Directory)  
        - 만들고 수정한 파일들이 있는 곳   
          즉, 아직 버전으로 만들어지기 전 단계
    
    2. Staging Area(Index)  
        - 버전을 만들려고 할 때 버전으로 만들고 싶은 파일을 올리는 곳  
        - Working tree 와 Repository 사이에 존재하는 공간
    
    3. Repository(.git directory)  
        - 만들어진 버전이 저장되는 곳  
        - .git 디렉토리를 repository로 봐도 무방함  
  
  - #### 2-2. 여러개의 파일을 버전으로 만들기
    - hello1.txt를 수정, hello2.txt 생성 했을때 어떤 일이 발생하는가?
        1. git status 명령어 실행  
        2. 기존에 있던 파일을 수정한 hello1.txt는 Changes not staged for commit  
           즉, 관리하고 있지만 스테이지 위에 올라가 있지 않음  
        3. 새로만든 hello2.txt는 untracked files 즉, 없는 상태로 봄   
           또한 스테이지 위에 올라가 있지 않음  
    - 결론  
      ```
      git은 모든 파일을 자동으로 추적 관리 하지 않는다.  
      백업 또는 협업 하고 싶지 않은 파일은 Untracked 상태로 두면 됨  
      관리를 하고 싶을 경우 git에게 알려줘야한다. (git add 명령어 사용) 
      ```
    - 각각의 버전마다 어떤 파일이 있는지 확인하고 싶은 경우?
        git log --stat 명령어를 사용하면 됨
    
  - #### 2-3. 명령어
    * nano [파일명]
      ```
      기본 에디터인 nano를 사용하여 파일을 생성하는 명령어
      
      작성 순서
      1. 작성하고자 하는 내용을 적음
      2. 에디터 나가기 : ^X → Ctrl + X
         에디터 하단에 다 적혀 있음
      3. 나가기를 누르면 저장할 것인지 묻는 메세지 나옴
      4. 파일 이름 확인 후 엔터 입력하면 파일 만들어짐
      
      참고
      git config --global core.editor "vim"
      ↑ 편집에디터를 nano에서 vim으로 변경하는 명령어
      ```
    * git status
      ```
      working tree status
      현재 상태가 어떤지 보는 명령어
      
      commits(버전이 있는지), Untracked files(추적되지 않는 파일), Changes to be committed(버전이 되기 위해 올라온 파일목록), .. 등의 상태 출력
      ```
    * git add [파일명]
      ```
      add to staging area
      이 파일을 버전으로 만들기 위해 스테이징에 추가하는 명령어
      버전관리가 되고 있는 파일, 아닌 파일 상관없이 stage에 올리기 위해 사용
      ```
    * git commit
      ```
      create version
      버전을 만드는 명령어
     
      참고
      git commit만 작성할 경우 에디터가 나오고 수정이 가능하지만 
      git commit -m "커밋내용"를 사용할 경우 에디터를 거치지 않고 바로 버전생성
      ```
    * git log
      ```
      show version
      버전들에 대한 로그(역사, 설명)를 보는 명령어
      작성자, 작성일자, 버전의 고유 아이디 값 등을 보여줌
      
      --stat 옵션
      git log --stat
      각 버전별 연관된 파일과 추가된 라인(줄), 추가된 파일을 알 수 있음
      ```
## Reference   
  - [생활코딩 GIT CLI](https://opentutorials.org/course/3839/22591)
  - [ian의 개발일기장](https://ian90.tistory.com/82) 
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")