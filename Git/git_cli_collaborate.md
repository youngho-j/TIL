# GIT CLI Collaborate

## 목차
1. [혼자서 작업하기](#1-혼자서-작업하기)  
1-1. [정리](#1-1-정리)  
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
      staging area에 파일 올
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

## Reference   
  - [생활코딩 GIT CLI Collaboration](https://opentutorials.org/course/3842)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
