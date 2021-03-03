# GIT CLI Branch Conflict 

## 목차
1. [Branch](#1-branch)  
1-1. [Branch란?](#1-1-branch란)   
2. [Branch 사용법](#2-branch-사용법)  
2-1. [정리](#2-1-정리)  
3. [Branch 병합](#3-branch-병합)  
3-1. [merge](#3-1-merge)  
3-2. [서로 다른 파일 병합](#3-2-서로-다른-파일-병합)  
3-3. [서로 같은 파일 병합](#3-3-서로-같은-파일-병합)  
3-3-1. [서로 같은 파일 다른 부분 병합](#3-3-1-서로-같은-파일-다른-부분-병합)   
3-3-2. [서로 같은 파일 같은 부분 병합](#3-3-1-서로-같은-파일-같은-부분-병합)  
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
### 3. Branch 병합
  - #### 3-1. merge
    1. merge - 합친다. / 병합한다.
    2. 예시 
       ```
       1. master branch에서 commit을 통해 버전1을 만듦
       
       2. master branch에서 commit을 통해 버전2을 만듦 
       
       3. master branch에서 commit을 통해 버전3을 만듦
       
       4. master branch에서 apple 브랜치를 만듦
       
       5. checkout을 통해 apple 브랜치에서 버전a를 만듦
       
       6. 다시 checkout을 통해 master branch로 돌아와 google 브랜치를 만듦
       
       7. google branch에서 버전g를 만듦
       
       8. 다시 checkout을 통해 master branch로 돌아와 버전4를 만듦
       
          이상황에서 apple branch 내용과 master branch 내용을 가지고 있는 새로운 버전을 만들고 싶음 즉, merge를 하고 싶다.
       
          - 여기에서 base는 버전a, 버전4의 공통의 조상은 버전3, 즉, 합치려고 하는 것의 공통의 조상을 base라고 함
       
          - base를 바탕으로 해서 merge(버전a, 버전4) 된 버전5는 merge commit이라고 함
       ```  
       <p align="center"><img src="/img/Git/merge1.png" width="70%" height="60%" title="merge 이미지"></img></p>  
       
  - #### 3-2. 서로 다른 파일 병합
    1. 진행과정
       1. manual-merge 폴더에서 새로 시작
       ```
       git init manual-merge
       
       cd manual-merge
       
       폴더 생성과 동시에 git init 후 폴더로 이동
       ```
       
       2. work1 버전 만들기
       ```
       nano work.txt
       
       git add work.txt
       
       git commit -m "work 1"
       ```
       
       3. 새로운 branch o2 생성 및 각 브랜치 work2 버전 만들기
       ```
       1. 새로운 branch o2 생성
       git branch o2
       
       2. master branch work2 버전 만들기
       nano master.txt
       
       git add master.txt
       
       git commit -m "work2"
       
       2-1. 커밋 메세지 변경하기
       현재 메세지인 work2 에서 master work2로 메세지 변경
       
       git commit --amend
       
       3. o2 branch에서 버전만들기
       nano o2.txt
       
       git add o2.txt
       
       git commit -m "o2 work2"
       ```
       
       4. 병합하기(master에 o2 branch를 병합)
       ```
       방향 o2 branch의 내용을 master로 
       
       1. 메인이 되는 branch로 이동
       git checkout master
       
       2. 현재 branch로 병합하고 싶은 branch를 merge를 통해 지정
       git merge o2
       
       3. git log --all --graph --oneline으로 병합 되었는지 확인
       
       4. git reset --hard (리셋하고 싶은 버전)
       -> 연습해보기 위해 사용
       ```  
  - #### 3-3. 서로 같은 파일 병합
    ##### 3-3-1. 서로 같은 파일 다른 부분 병합
       1. manual-merge 폴더에서 새로 시작
          ```
          git init manual-merge
       
          cd manual-merge
       
          폴더 생성과 동시에 git init 후 폴더로 이동
          ```
       
       2. 1 버전 만들기
          ```
          nano work.txt
       
          git add work.txt
       
          git commit -m "1"
          ```
       
       3. 새로운 branch o2 생성 및 각 브랜치 work2 버전 만들기
          ```
          1. 새로운 branch o2 생성
          git branch o2
       
          2. master branch master work 2 버전 만들기
          nano work.txt
       
          git add work.txt
       
          git commit -m "master work 2"
       
          3. o2 branch에서 o2 work 2 버전 만들기
          git checkout o2
       
          nano work.txt
       
          git add work.txt
       
          git commit -m "o2 work2"
          ```
       
       4. 병합하기(master에 o2 branch를 병합)
          ```
          방향 o2 branch의 내용을 master로 
       
          1. 메인이 되는 branch로 이동
          git checkout master
       
          2. 현재 branch로 병합하고 싶은 branch를 merge를 통해 지정
          git merge o2
       
          3. git log --all --graph --oneline으로 병합 되었는지 확인
       
          4. cat work.txt로 변경된 부분 확인 
          ```  
       
       중요!  병합시 같은 파일이라고 하더라도 서로 다른 부분을 수정했다면 알아서 수정해준다.   
    
    ##### 3-3-2. 서로 같은 파일 같은 부분 병합
       1. manual-merge 폴더에서 새로 시작
          ```
          git init manual-merge
       
          cd manual-merge
       
          폴더 생성과 동시에 git init 후 폴더로 이동
          ```
       
       2. work 1 버전 만들기
          ```
          nano work.txt
       
          git add work.txt
       
          git commit -m "work 1"
          ```
       
       3. 새로운 branch o2 생성 및 각 브랜치 work2 버전 만들기
          ```
          1. 새로운 branch o2 생성
          git branch o2
       
          2. master branch master work 2 버전 만들기
          nano work.txt
       
          git add work.txt
       
          git commit -m "master work 2"
       
          3. o2 branch에서 o2 work 2 버전 만들기
          git checkout o2
       
          nano work.txt
       
          git add work.txt
       
          git commit -m "o2 work2"
          ```
       
       4. 병합하기(master에 o2 branch를 병합)
          ```
          방향 o2 branch의 내용을 master로 
       
          1. 메인이 되는 branch로 이동
          git checkout master
       
          2. 현재 branch로 병합하고 싶은 branch를 merge를 통해 지정
          git merge o2
       
          3. CONFLICT 발생
          Auto-merging work.txt
          CONFLICT (content): Merge conflict in work.txt
          Automatic merge failed; fix conflicts and then commit the result.
          
          충돌이 발생해서 자동으로 합칠 수 없다는 것
          즉, 이 부분만 해결해주면 다른 부분은 알아서 하겠다.

       
          4. git status로 현재 상태 보기
          On branch master
          You have unmerged paths.
            (fix conflicts and run "git commit")
            (use "git merge --abort" to abort the merge)

          Unmerged paths:
            (use "git add <file>..." to mark resolution)
                  both modified:   work.txt

          no changes added to commit (use "git add" and/or "git commit -a")
          
          해당 파일이 충돌이 났다.
          
          5. 파일 확인해보기
          nano work.txt
          
          아래와 같이 파일 내용이 보여짐
          #Title
          content
          <<<<<<< HEAD         ← 현재 Branch 즉, master의 내용
          master
          =======              ← 구분자
          o2
          >>>>>>> o2           ← o2 Branch의 내용
          #Title
          content
          
          즉, 위 내용은 구분자를 중심으로 위에는 현재 Branch의 내용이고, 아래는 o2 Branch의 내용
          "이 부분은 자동으로 합칠 수 없으니 이 부분을 해결해 준다면 나머지는 알아서 하겠다."
          
          중요하다고 생각하는 부분을 남기면 됨 
            1. master가 중요하다고 생각하면 master 내용에서 수정한 부분을 제외하고 다 지움
               Ex) 
               #Title
               content
               master
               #Title
               content
            
            2. o2가 중요하다고 생각하면 o2 내용에서 수정한 부분을 제외하고 다 지움
            
            3. 둘 다 중요하다고 생각하면 master, o2 내용에서 수정한 부분을 제외하고 다 지움(형식은 본인 마음대로)
               Ex) 
               #Title
               content
               master, o2
               #Title
               content
               
          6. 충돌 해결 후 버전만들기
          git add work.txt
          
          git commit
          자동으로 Conflict가 해결되었다고 나오면서 merge commit이 됨
          ```

## Reference   
  - [생활코딩 GIT CLI Branch](https://opentutorials.org/course/3840)

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")

