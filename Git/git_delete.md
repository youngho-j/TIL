# GIT CLI 삭제관련 내용

## 목차
1. [.gitignore 설정방법](#1-gitignore-설정방법)  
1-1. [.gitignore](#1-1-gitignore)  
1-2. [.gitignore 설정하기](#1-2-gitignore-설정하기)  
2. [.gitignore 설정하지 않고 push 한 경우 원격저장소에 잘못 올라간 파일 삭제방법](#2-원격저장소에-잘못-올라간-파일-삭제-방법)   
2-1. [과정 정리](#2-1-과정-정리)    

***
### 1. .gitignore 설정방법
 - #### 1-1. .gitignore  
   - Git 버전 관리에서 제외할 파일 목록을 지정하는 파일  
 - #### 1-2. .gitignore 설정하기  
   1. .git 파일이 있는 최상위 경로로 이동  
      ```
      cd (최상위 경로)
      ```
           
   2. .gitignore 파일 생성  
      ```
      touch .gitignore or nano .gitignore
        
      touch로 파일 생성시 수정을 따로 해줘야함
      ```
           
   3. .gitignore 파일 내용 채우기  
       - [GitHub gitignore repo](https://github.com/github/gitignore)를 참고  
       - [gitignore.io](https://www.toptal.com/developers/gitignore)를 참고 (소스 복사후 붙여 넣으면 됨)   
         
### 2. 원격저장소에 잘못 올라간 파일 삭제 방법
 - #### 2-1. 과정 정리  
   1. 원격 저장소에서 파일 삭제하기  
         git rm --cached [file name]
         ```
         --cached 옵션을 통해 원격 저장소에 있는 파일 삭제
         로컬 저장소에 있는 파일은 삭제 되지 않음
         
         Ex) git rm --cached test1.class
         ```
            
         git rm --cached -r [폴더이름]
         ```
         지정한 폴더와 폴더 하위의 모든 파일 삭제

         Ex) git rm --cached -r bin/
         ```   
         참고  
           
         git rm [file name]  
         ```
         원격 저장소와 로컬 저장소에 있는 파일 삭제
         
         Ex) git rm test1.java
         ```
   2. .gitignore 파일 설정하기
         .git 파일이 있는 최상위 경로로 이동  
         ```
         cd (최상위 경로)
         ```
           
         .gitignore 파일 생성  
         ```
         touch .gitignore or nano .gitignore
         
         touch로 파일 생성시 수정을 따로 해줘야함
         ```
           
         .gitignore 파일 내용 채우기  
          - [GitHub gitignore repo](https://github.com/github/gitignore)를 참고  
          - [gitignore.io](https://www.toptal.com/developers/gitignore)를 참고 (소스 복사후 붙여 넣으면 됨)   
         
   3. 원격 저장소에 저장하기  
         commit, push 수행
         ```
         git commit -m "[커밋 메세지]"
         
         git push
         ```
## Reference
  - [Heee's .gitignore 설정하기](https://gmlwjd9405.github.io/2017/10/06/make-gitignore-file.html)  
  - [GitHub gitignore repo](https://github.com/github/gitignore)  
  - [gitignore.io](https://www.toptal.com/developers/gitignore)  
  - [농장 .gitignore 설정](https://we-always-fight-with-code.tistory.com/66)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
