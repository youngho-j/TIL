# Git Error

### 목록

  1. [credential prompt](#1-logon-failed-use-ctrl--c-to-cancel-basic-credential-prompt)  
  2. [git push error](#2-git-push-error-failed-to-push-some-refs-to)  
  3. [git You asked to pull from the remote 'upstream', but did not specify a branch](#3-git-pull-error-you-asked-to-pull-from-the-remote-upstream-but-did-not-specify-a-branch)  

#### 1. Logon failed, use ctrl + c to cancel basic credential prompt
  1. Git Bash를 사용하여 git push 진행 중 위 제목과 같은 문구 발생하며 로그인창 뜸

  2. 계정, 이름, 비밀번호로 모두 시도 했지만 실패

  3. 원인은 무엇인가?  
     `Git 최신 업데이트로 인한 이슈`  

  4. Bash에 `git update-git-for-windows` 입력 후 업데이트 진행

  5. 업데이트 후 문제 해결

## Reference   
  - [규글 Logon failed, use ctrl + c to cancel basic credential prompt](https://kim6394.tistory.com/251)  
***

#### 2. git push error: failed to push some refs to
  1. 원인  
     `GitHub에 있는 파일과 현재 push하려는 commit이 일치하지 않아서 발생`  
  
  2. pull을 통해 중요한 내용은 없어서 marge 후 다시 push 진행함  
  
  3. 작업한 내용이 많거나 중요한 경우 `-f` 옵션 사용하여 push  
     `커밋 이력을 강제로 덮어씌우게 되므로 사용 안하는게 좋음!`  

  4. git clone을 사용하여 원본 파일 가져온 뒤 원본파일 중 누락된 파일을 작업디렉토리로  
     이동 시켜 삭제함으로써 로컬과 깃허브의 동기화하여 진행하는 방법도 있음  

## Reference   
  - [Nirsa git push error: failed to push some refs to ~ 에러 해결방법](https://nirsa.tistory.com/167)  
  - [victolee failed to push some refs to ~](https://victorydntmd.tistory.com/100)
***

#### 3. git pull error: You asked to pull from the remote 'upstream', but did not specify a branch
  1. 원인  
     `GitHub 원격 저장소와 상호작용시 브랜치를 지정하지 않아서 발생`
       
     You asked to pull from the remote 'upstream', but did not specify a branch.  
     Because this is not the default configured remote for your current branch,  
     you must specify a branch on the command line.  
     
  2. 수행과정
      1. 현재 git-prac 폴더의 기본 분기는 github repo의 master branch로 설정 되어있음  
      
      2. pull을 하고자 하는 remote repo는 gitlab repo의 master branch  
      
      3. git pull 명령어 실행시 내려받을 파일이 없다고 함 (기본으로 설정된 github의 내용을 가져와서)  
     
      4. git pull (gitlab repo 별명) 명령어 실행시 위 에러코드 발생  
      
      5. git pull (gitlab repo 별명) (해당 repo의 branch) 명령어 실행  
      
      6. gitlab remote repo의 내용이 git-prac(local repo)로 복제된 것 확인
      
      7. git push 명령어를 실행하여 github로 백업된 것 확인 
      
      8. git-prac(local repo), github(remote repo), gitlab(remote repo) 모두 파일 버전 동기화 확인 

   3. 참고
      git pull과 마찬가지로 git push 진행시에도 위와 같은 오류 발생 가능  

## Reference   
  - [SPECTRUM LEARNS TO DIG fork 해온 저장소를 최신 상태로 유지하기](http://spectrumdig.blogspot.com/2013/01/git-fork.html)  
  - [Gullele's Corner You Asked To Pull From The Remote But Did Not Specify The Branch Github Error](https://gullele.com/you-asked-to-pull-from-the-remote-but-did-not-specify-the-branch-github-error/)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")
