# Git CLI
## 목차
  1. [버전관리의 시작](#1-버전관리의-시작)  
  1-1. [저장소 만드는 법](#1-1-저장소-만드는-법)  
  1-2. [명령어](#1-2-명령어)  
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
## Reference   
  - [생활코딩 GIT CLI](https://opentutorials.org/course/3839/22591) 
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
