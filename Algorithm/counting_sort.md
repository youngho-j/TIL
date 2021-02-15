# 계수 정렬

  - Counting Sort
  
  - 숫자의 개수를 센 후 누적 합을 구하고, 다시 숫자를 넣어주는 방식의 정렬
  
  - 특정한 범위(Ex) 0~100) 안에 있을 때 사용
    <p align="center"><img src="/img/Algorithm/CountingSort.gif" width="80%" height="80%" title="계수정렬 애니메이션"></img></p>  
    
  - 실행 과정
    ```
    1. A배열을 처음부터 끝까지 돌면서 각 요소가 몇번 나왔는지 count 배열에 저장
    2. count 배열에 저장된 등장 횟수를 누적합으로 변경  
       누적합을 통해 해당 숫자가 인덱스 번호 안에 속한다는 것을 알 수 있음 즉, 위치를 알 수 있음
    3. count 배열의 누적 합을 통해 위치를 참고하여 A배열을 뒤에서 앞으로 순회하면서 정렬된 B배열에 넣어줌
    ```  
   - 장점
     * 비교를 하지 않고 정렬하는 Counting Sort 알고리즘의 시간복잡도는 O(n+k) 
     * 안정 정렬(같은 숫자라도 정렬 시 순서가 섞이지 않음)
    
  - 단점
    * 대부분의 상황에서 엄청난 메모리 낭비 야기 할 수 있음(숫자 개수 저장 공간, 결과 저장 공간)  
      → 누적합 배열에 대한 접근을 O(n) 달성하기 위해 정렬할 배열에 포함된 숫자의 최댓값 만큼의 메모리를 필요
    * 가장 큰 숫자에 영향을 받음

  - 시간 복잡도  
    → 최상의 경우 → O(n + k)  
	    `n : 데이터갯수`  
      `k : 범위(정렬할 수 중 가장 큰 값)`  
    → 최악의 경우 → O(n!)

## Reference
  - [개발냥발 특수 정렬 알고리즘](https://coding-nyan.tistory.com/7)
  - [멍멍멍 Counting Sort : 계수 정렬](https://bowbowbow.tistory.com/8)
  - [얍문's Coding World.. 정렬별 장단점 및 시간복잡도](https://yabmoons.tistory.com/250)
  - [Burton Rosenberg Counting Sort](http://www.cs.miami.edu/home/burt/learning/Csc517.091/workbook/countingsort.html)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Algorithm/README.md "Go README.md")
