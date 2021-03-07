# GIT CLI Collaborate

## 목차
1. [혼자서 작업하기](#1-혼자서-작업하기)  
1-1. [정리](#1-1-정리)  
2. [같이 작업하기](#2-같이-작업하기)  
2-1. [정리](#2-1-정리)  
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
## Reference   
  - [생활코딩 GIT CLI Collaboration](https://opentutorials.org/course/3842)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
