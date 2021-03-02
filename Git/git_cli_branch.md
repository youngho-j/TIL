# GIT CLI Branch Conflict 

## 목차
1. [Branch](#1-branch)  
1-1. [Branch란?](#1-1-branch란)   
2. [Branch 사용법](#2-branch-사용법)  
2-1. [정리](#2-1-정리)  
***

### 1. Branch
  - #### 1-1. Branch란?
    - 가지라는 뜻   
    
    - 그럼? 가지란 무엇인가?  
      줄기에서 뻗어나온 것이다.   
    
    - 같은 뿌리에서 나왔지만 서로 다른 역사를 써가는 버전들  
    
    - 독립적으로 어떤 작업을 진행하기 위한 개념  
    
    - 여러 개발자들이 동시에 다양한 작업을 할 수 있게 만들어 주는 기능  
    
    - 참고  
      뒤에서 배울 내용이지만 브랜치 사용시 충돌(conflict)이 발생 가능  
      ```
       * 같은 파일인데 다른 부분을 합쳤을때 자동으로 병합
       
       * 같은 파일인데 같은 부분을 합쳤을때 병합과정을 멈추고
         수동으로 수정 요청을 보냄
      ```

### 2. Branch 사용법
  - #### 2-1. 정리
    1. 현재 브랜치 확인하기
       ```
       git branch 
       명령어 사용시 branch 목록 확인 가능
       
       참고 
       branch 목록 중 '*'은 현재 브랜치를 나타냄
       
       git log --all --graph --oneline
       현재상태를 계속 보기위해 사용
       
       --all : 모든 브랜치가 보이는 옵션
       --graph : 시각적으로 표현하는 옵션
       --oneline : 한줄로 표현하는 옵션
       
       위 git log ~ 출력시 HEAD -> 브랜치명, 은 
       현재 브랜치에 속해있는 상태라는 것을 알려줌
       
       HEAD외에는 생성된 브랜치명들임 
       ```
    2. 브랜치 만들기
       ```
       git branch (브랜치이름)
       입력한 브랜치이름을 가진 branch 생성
       ```
    3. 브랜치 이동하기
       ```
       git checkout (브랜치이름)
       사용하고자 하는 브랜치로 이동
       ```
## Reference   
  - [생활코딩 GIT CLI Branch](https://opentutorials.org/course/3840)

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")

