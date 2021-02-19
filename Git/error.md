# Git Error

### 목록

  1. [credential prompt](#1-logon-failed,-use-ctrl-+-c-to-cancel-basic-creaetial-prompt)
  2. [git push error](#2-git-push-error:-failed-to-push-some-refs-to-~)

#### 1. Logon failed, use ctrl + c to cancel basic creaetial prompt
  1. Git Bash를 사용하여 git push 진행 중 위 제목과 같은 문구 발생하며 로그인창 뜸
  2. 계정, 이름, 비밀번호로 모두 시도 했지만 실패
  3. 원인은 무엇인가?  
     `Git 최신 업데이트로 인한 이슈`  
  4. Bash에 `git update-git-for-windows` 입력 후 업데이트 진행
  5. 업데이트 후 문제 해결

## Reference   
  - [규글 Logon failed, use ctrl + c to cancel basic creaetial prompt](https://kim6394.tistory.com/251)  
***
#### 2. git push error: failed to push some refs to ~
  1. 원인  

    'GitHub에 있는 파일과 현재 push하려는 commit이 일치하지 않아서 발생'
  2. pull을 통해 중요한 내용은 없어서 marge 후 다시 push 진행함
  3. 작업한 내용이 많거나 중요한 경우 `-f` 옵션 사용하여 push  
     `커밋 이력을 강제로 덮어씌우게 되므로 주의해서 사용!`
***
## Reference   
  - [Nirsa git push error: failed to push some refs to ~ 에러 해결방법](https://nirsa.tistory.com/167)  
  - [victolee failed to push some refs to ~](https://victorydntmd.tistory.com/100)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")