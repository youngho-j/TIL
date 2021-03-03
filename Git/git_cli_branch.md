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
3-3-2. [서로 같은 파일 같은 부분 병합](#3-3-2-서로-같은-파일-같은-부분-병합)  
4. [CONFLICT](#4-conflict)  
4-1. [3 way merge](#4-1-3-way-merge)  
4-2. [외부 도구를 이용해서 병합하는 방법](#4-2-외부-도구를-이용해서-병합하는-방법)  
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

### 4. CONFLICT
  - #### 4-1. 3 way merge
    - 충돌은 브랜치와 브랜치 병합시, 협업시도 발생 가능
    
    - 그렇다면 Git은 어떻게 충돌에 대처하는가? 3 way merge 방법 사용
      ```
      brance 그림

      *    -> merge commit
      │\
      │ *  -> there(branch 이름)
      * │  -> here(branch 이름)
      │/
      *    -> base : here, there branch의 조상
      ```
      |here|base|there|2 way merge|3 way merge|
      |:---:|:---:|:---:|:---:|:---:|
      |A|A|A|A|A|
      |H|B|B|?|H|
      |C|C|T|?|T|
      |H|D|T|?|?|
    
    - 2 way merge 방법 사용시  
      here와 there branch를 비교하여 자동으로 합할 수 있는 것과 없는 것을 판별  
    
    - 3 way merge 방법 사용시  
      2 way merge에서 좀 더 많은 것들을 자동화하기 위해 등장  
      
      3 way merge 방법은 merge 하고자 하는 branch들의 공통의 조상인 base를 알아야함.  
      ```
      위 표의 here base there을 보면
      
      A A A 로 모두 같음, 따라서 수정한게 없으므로 A
      
      H B B 로 base와 there가 같으므로 수정이 되지 않았음, here가 다르므로 수정이 되었음 따라서 H
      
      C C T 로 base와 here가 같으므로 수정이 되지 않았음, there가 다르므로 수정이 되었음 따라서 T
      
      H D T 로 모두 다름, 따라서 두 branch가 모두 수정되었으므로 자동병합이 불가하므로 충돌 발생 -> 사람이 수정해야함
      ```  

  - #### 4-2. 외부 도구를 이용해서 병합하는 방법
    - P4MergeTool
      1. 다운로드(운영체제에 맞게)  
         [P4MergeTool 다운로드](https://www.perforce.com/downloads/visual-merge-tool)  
         
      2. 환경변수 설정(windows)  
          1. 작업표시줄에서 시스템 환경 변수 편집 검색 후 클릭  
          2. 환경 변수 버튼 클릭  
          3. 시스템 변수 그룹에서 Path 클릭 후 편집   
          4. 새로 만들기 클릭하여 p4merge.exe가 설치된 폴더 경로 입력  
      
      3. git config에 등록하기  
          1. Diff Tool 등록  
             ```
             git config --global diff.tool p4merge
             git config --global difftool.p4merge.path "C:/Program Files/Perforce/p4merge.exe(설치경로)"
             git config --global difftool.prompt false
             ```
          2. Merge Tool 등록  
             ```
             git config --global merge.tool p4merge
             git config --global mergetool.p4merge.path "C:/Program Files/Perforce/p4merge.exe(설치경로)"
             git config --global mergetool.prompt false
             ```
          3. 등록 확인  
             cat ~/.gitconfig  
      
      4. 실행  
          `git difftool`  
          `git mergetool`  
          
      5. 충돌을 해결하고 저장한 뒤 프로그램을 끄면 자동으로 add로 staging에 올려줌  
      
      6. orig 파일은 충돌난 상태를 백업해 놓은 것으로 rm (충돌난 파일).orig 로 삭제  
      
      7. git commit으로 버전 저장  
    
    - 3 way merge tool은 좋은게 많으니 검색해보고 좋은거 쓰면 됨  
  

## Reference   
  - [생활코딩 GIT CLI Branch](https://opentutorials.org/course/3840)  
  - [테디노트 p4mergetool](https://teddylee777.github.io/git/study-git-2)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Git/README.md "Go README.md")

