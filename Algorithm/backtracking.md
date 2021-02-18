# 백트래킹(Backtracking)
  - 백트래킹?
    * 상태공간을 트리로 나타낼 수 있을 때 적합한 방식  
      → 일종의 트리 탐색 알고리즘으로 봐도 됨  
    
    * 일반적인 알고리즘 중 하나이며, CSP를 해결하기 위해 쓰임  
    
    * CSP? 
      + Contstrain Satisfaction Problems : 특정 조건을 만족하는 문제
	  
	* 즉,  백트래킹이란 **조건을 만족하는** 모든 경우의 수를 살펴보는 것  
	  → 조건을 만족하는 경우에 대해서만 모든 조합을 살펴봄  
	  따라서, 경우에 따라서 모든 경우의 수를 찾는 것 보다 훨씬 빠를 수 있음   
  
  - 백트래킹 유망성 판단
    * 노드의 유망성 판단(promising)
      → 해가 될 만한지 판단(해가 될 가능성 존재하는지)
    * 유망하지 않을 경우 해당 노드의 이전(부모)로 돌아가 (Backtracking) 다음 자식으로 이동
    * 유망하지 않은 노드에 가지 않는 것(가지치기, pruning)
  - 백트래킹 방식
    * 깊이 우선 탐색(Depth First Search)
      ```
      - like 미로찾기
      
      - 상태공간을 나타낸 트리에서 바닥에 도달할 때까지 한쪽 방향으로만 내려가는 방식
        → 한 방향으로 들어가서 막다른 길(트리의 바닥)에 다다르면 왔던 길을 돌아 다른 방향으로 이동  
        → 목표지점(답)이 나올 때까지 반복  
        
      - 재귀함수로 구현 가능, 스택으로 구현 가능
      ```
    * 너비 우선 탐색(Breadth First Search)
      ```
      - 모든 분기점을 다 검사하면서 진행하는 방식
      
      - 큐를 써서 구현
      
      - 각 경우를 검사하면서 발생하는 새로운 경우를 큐에 집어 넣음  
        → 검사한 원소는 큐에서 뺌
      
      - 장점 : DFS가 못건드리는 문제를 풀 수 있음
      
      - 단점 : 공간 복잡도가 너무 커 가지치기를 제대로 안할 경우  
        DFS보다 오버플로우 발생 가능성 높음
      ```
    * 최선 우선 탐색(Best First Search/Heuristic Search)
      ```
      - BFS에서 조금 더 발전한 방식
      
      - 우선순위 큐(보통은 힙)를 써서 구현
      
      - 현재 가장 최적인 경우를 우선적으로 검사
      
      - 가지치기를 적용하면 상당히 효과적인 방법이 될 수 있음
      ```
    
  - 대표 예제
    * N-Queen 
      + N×N 크기의 체스판에서 N개의 퀸을   
        서로 공격하지 않도록 두는 경우의 수를 구하는 문제  
      + 수행 조건  
        ```
        조건(CSP)   
        퀸을 k컬럼에 두기 위해 상하좌우 및 대각선에 퀸이 없어야함  
        즉, 각 행 또는 열에는 오직 하나의 퀸만 있을 수 있다.   
	      ```  

      + 수행 과정
        <p align="center"><img src="/img/Algorithm/n-queen.png" width="70%" height="60%" title="n-queen 이미지"></img></p>
  
## Reference
  - [백준 N과 M(1)](https://st-lab.tistory.com/114?category=862595)
  - [오뚝이 개발자 백트래킹](https://otugi.tistory.com/88)
  - [Jeong Dowon Backtraking 이해하기](https://jeongdowon.medium.com/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-backtracking-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-13492b18bfa1)
  - [나무위키 백트래킹](https://namu.wiki/w/%EB%B0%B1%ED%8A%B8%EB%9E%98%ED%82%B9)
  - [마이구미 n-Queen](https://mygumi.tistory.com/199)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Algorithm/README.md "Go README.md")
