# GIT CLI Collaborate

## 목차
1. [혼자서 작업하기](#1-혼자서-작업하기)  
1-1. [정리](#1-1-정리)  
2. [같이 작업하기](#2-같이-작업하기)  
2-1. [정리](#2-1-정리)  
3. [push & pull](#3-push--pull)  
3-1. [협업 중 일어날 수 있는 경우의 수](#3-1-협업-중-일어날-수-있는-경우의-수)  
4. [remote branch 와 fetch](#4-remote-branch-와-fetch)  
4-1. [정리](#4-1-정리)  
***
### 1. 혼자서 작업하기
  - #### 1-1. 정리
    - 디렉토리 생성  
      ```
      git init (디렉토리 명)
      디렉토리를 생성
      ```
    - 작업파일 생성  
      ```
      cd (경로) 
      해당 폴더로 이동
      
      nano (파일명).(파일확장자)
      파일 생성
      ```
    - staging에 파일 추가  
      ```
      git add (파일)
      staging area에 파일 올림
      ```
    - 버전만들기  
      ```
      git commit -m "메세지"
      commit 메세지를 쓰고 버전 만들기
      ```
    - 원격 저장소 생성  
      ```
      github에서 원격 저장소 생성(다른 원격저장소 이용해도 상관없음) 
      ```
    - 원격 저장소와 로컬 저장소 연결 및 백업(동기화)  
      ```
      이미 지역저장소가 존재 하므로 existing repo ~ 내용을 따라서 진행
      
      git remote add (원격저장소 별명, origin이 기본) (원격 저장소 주소)
      현재 저장소에 원격저장소 추가

      git push -u origin master
      지역저장소의 마스터와 원격 저장소의 마스터를 페어링(Tracked) 
      ```  
### 2. 같이 작업하기
  - #### 2-1. 정리
    - github에서 비공개, 공개 저장소 사용시 버전을 올리기 위해서는 승인이 필요
    - 저장소 승인하기
      ```
      1. 공유하는 원격 저장소에서 settings로 이동 
      
      2. 우측 Collaborators & teams 탭 클릭
      
      3. 하단 Collaborators에 username or email adress 추가
      
      4. 초대 받은 사람은 메일을 받게 되고 해당 메일에서 view invitation 클릭

      5. Accept invitation을 클릭하면 협업자 관계 맺어짐  
         
         참고  
         Copy invite link - 못받았을 경우 링크를 복사해서 보내주면 됨  
         Premission level - Admin / Write / Read 가 있음  
      ```
    - 협업자 저장소 세팅
      ```
      저장소 주소 복사
      
      git clone (원격 저장소 주소) (clone을 받을 디렉토리)
      ```
### 3. push & pull
  - #### 3-1. 협업 중 일어날 수 있는 경우의 수
    1. A 라는 사람이 work.txt 파일을 수정하고 버전을 만들어 원격저장소에 push 한 뒤  
       B 라는 사람이 pull을 깜빡하고 work.txt 파일을 수정 후 버전을 만들어 원격 저장소에 push를 한 상황
       ```
       code
       
       1. A : git pull을 통해 현재 원격저장소에서 변경된 내용을 로컬에 내려받음
       
       2. A : nono work.txt를 통해 파일을 수정(2번째 줄)
       
       3. A : git add work.txt
       
       4. A : git commit -m "work 2a"
       
       5. A : git push
       
       6. B : nano work.txt를 통해 파일 수정(2번째 줄)
       
       7. B : git add work.txt
       
       8. B : git commit -m "work 2b"
       
       9. B : git push -> rejected 발생  
              원인 : 원격저장소에 변경된 작업이 존재하는데 내려받지 않아서  
              해결 : 원격저장소의 내용을 pull로 내려받고 push를 실행해라  
       
       10. B : git pull -> CONFLICT 발생  
               원인 : 같은 줄을 수정했기 때문에 충돌 발생  
               해결 : 병합도구(git mergetool or nano (파일)을 통해 수동으로 수정)  
       
       11. B : nano work.txt로 원하는 내용으로 수정 후 git add work.txt
       
       12. B : git commit  
               git commit -m "(메세지)" 형태처럼 사용하지 않는 이유  
               : git이 conflict 상황을 기억하기 때문에 자동으로 메세지를 생성해줌   
       
       13. B : git log --all --graph --oneline 사용시 병합이 된 것을 알 수 있음
       
       14. B : 병합된 새로운 버전을 git push
       
       15. A : 작업을 하기 전 git pull을 통해 새로운 버전을 내려 받아 동기화 시킴  
               각 로컬에서 git log --all --graph --oneline 사용해 보면 됨  
       
       Point!
       최대한 작업을 빨리 끝내고 push를 자주해야지 충돌이 일어나지 않음
       
       작업시 반드시 git pull을 통해 업데이트된 내용이 있는지 확인하는 것은 매우 좋은 습관이다.
       
       -> conflict, push, pull의 기능을 통해 협업자간 커뮤니케이션이 증대될 수 있다.         
       ```
### 4. remote branch 와 fetch
  - #### 4-1. 정리
    1. git fetch; git merge
       협업시 기본적인 작업 순서는 아래 순서와 같음 
       
       1. git pull → commit → git push   
       
       위와 같이 사용할 수 있으나 아래와 같이 작업을 진행 할 수 있음(결과는 같다.)  
       
       2. git fetch → git merge FETCH_HEAD → commit → push  
          ```
          git fetch 
           = 원격 저장소로부터 필요한 파일을 다운(remote branch만 가져옴)
             지역 저장소의 브랜치는 지역 저장소의 최근 커밋 상태
             원격 저장소의 브랜치(origin/master)는 다운 받은 최신 커밋의 상태를 가리킴
           
           git merge (원격저장소별명)/(브랜치명)
           = 원격 저장소의 브랜치를 로컬 저장소의 master branch로 merge(병합)
           
           참고, 그냥 git pull해도 상관은 없음.
          ```
           
       즉, `git pull = git fetch → git merge origin/master`   
       
       참고  
       ```
       git merge (원격저장소별명)/(브랜치명)을 보다 간편하게 사용하고 싶을 경우
       
       git merge FETCH_HEAD을 사용하면 자동적으로 적용이 됨
       
       그럼 어떻게 자동 적용이 되는걸까?
       fetch를 사용시 .git/FETCH_HEAD라는 파일을 생성하여 참고하여 자동 적용
       ```
         
       git fetch는 언제 쓰이나?  
       ```
       신중하게 git의 데이터를 pull하고 싶을때 
       데이터를 일단 가져오고 나중에 결합하면 됨
       ```
         
       git fetch 사용하는 이유  
       ```
       1. 원래 내용과 바뀐 내용과의 차이를 알 수 있음 
          → git diff HEAD origin/master  
       2. commit이 얼마나 됐는지 알 수 있음
          → git log --decorate --all --oneline
       ```
## Reference   
  - [생활코딩 GIT CLI Collaboration](https://opentutorials.org/course/3842)  
  - [유자의 개발아지트 pull과 fetch의 차이](https://yuja-kong.tistory.com/60)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
