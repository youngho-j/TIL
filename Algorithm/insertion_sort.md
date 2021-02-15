# 삽입 정렬
  - Insertion Sort
  - **손안의 카드를 정렬하는 방법과 유사**    
    <p align="center"><img src="/img/Algorithm/Insertion_Sort.gif" width="40%" height="50%" title="삽입정렬 이미지"></img></p>  
  
  - 자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열부분과 비교하여  
    자신의 위치를 찾아 삽입하여 정렬 완성하는 알고리즘
    ```
    즉, 두 번째 자료부터 시작하여 그 앞(왼쪽)의 자료들과 비교하여 삽입할 위치를 지정한 후   
    자료를 뒤로 옮기고 지정한 자리에 자료를 삽입하여 정렬하는 알고리즘
    
    Point
      1. 처음 정렬 시작 시 두번째 인덱스부터 시작(첫 번째 인덱스는 정렬된 것으로 본다.)
      2. 선택한 원소를 key에 저장
      3. key와 선택한 원소의 이전 원소들과 비교하면서 삽입
      4. 선택한 원소의 다음 원소를 선택하여 3번 반복
    ```  
  - 장점
    * 구현이 간단함
    * 선택 정렬이나 버블 정렬과 같은 O(n²) 알고리즘에 비교하여 빠르고, 안정 정렬이고 in-place 알고리즘이다.  
    
  - 단점
    * 배열이 길어질수록 효율 ↓
  
  - 시간 복잡도(탐색 대상 요소 n개로 가정)  
    → 최선의 경우 (비교 연산 횟수 = 이미 정렬되어 이동 없이 1번 비교) →  O(n)  
    → 최악의 경우 (비교 연산 횟수 = 역으로 정렬되어 있는 경우) →  O(n²)
  
## Reference
  - [위키백과 삽입정렬](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC)
  - [DevJin-Blog Stable Sort, inplace algorithm이란?](https://devjin-blog.com/sort-algorithm-1/)
  - [ZeddiOS 정렬 알고리즘 정리1](https://zeddios.tistory.com/20)
  - [Heee's Development Blog 삽입정렬이란?](https://gmlwjd9405.github.io/2018/05/06/algorithm-insertion-sort.html)
  - [열쓰 삽입정렬](http://blog.naver.com/PostView.nhn?blogId=redwave102&logNo=80073417047)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Algorithm/README.md "Go README.md")
