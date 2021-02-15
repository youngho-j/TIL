# 알고리즘 
  - 알고리즘이란?
    * 어떠한 문제를 해결하기 위한 '일련의 절차를 공식화한 형태(해결방법)'로 표현한 것
    * 해결방법은 여러 가지로 존재 할 수 있다.
    * 따라서 시간 복잡도가 가장 낮은 알고리즘을 선택하여 사용하여야 한다!
  - 알고리즘 실행시간
    * 컴퓨터가 알고리즘 코드를 실행하는 속도에 의존
    * 코드 실행 속도는 '컴퓨터의 처리속도, 언어종류, 컴파일러의 속도에 달려있음'
      
  - 알고리즘에 필요한 기본 개념
     * 점근적 분석
      ```
      각 알고리즘이 주어진 데이터의 크기를 기준으로 수행시간 혹은 사용공간이 얼마나 되는지를  
      객관적으로 비교할 수 있는 기준을 제시
      ```
    * 점근적 표기법(복잡도를 나타내는 방법)
      - 입력값의 크기에 따른 함수의 증가량(성장률)에 가장 큰 영향을 주는 항만 계산하여 표기
      - 어떤 함수의 증가 양상을 다른 함수와의 비교로 표현하는 수론과 해석학의 방법
      - 알고리즘의 복잡도를 단순화할 때나 무한급수의 뒷부분을 간소화시 사용
      - 특히, 알고리즘의 복잡도를 나타내는 용어로는 "계산 복잡도 이론" 또는 "시간복잡도"로  
        **Big O 표기법**이 일반적으로 사용  
        왜? 평균인 세타를 사용하면 가장 정확하고 좋지만 평가가 까다로움,  
        최악의 경우 판단시 평균과 가까운 성능으로 예측하기 쉽기 때문에
        ```
        1. 최선의 경우 (Big-Ω Notation) : 점근적 하한
        2. 평균의 경우 (Big-θ Notation) : 점근적 하한과 점근적 상한의 교집합
        3. 최악의 경우 (Big-O Notation) : 점근적 상한(최악의 상황에서도 이 성능 이상을 보장한다.)
        ```
    * Big-O 표기법  
      ```
      불필요한 연산을 제거하여 알고리즘분석을 쉽게 할 목적으로 사용  
      
      알고리즘의 효율성을 나타내는 지표
      
      최악의 상항만을 염두해 두기에 상수나, 영향력이 없는 항은 철저하게 무시  
      
      Big-O로 측정되는 복잡성에는 시간과 공간 복잡도가 있음
      ```
      <p align="center"><img src="/img/Algorithm/Big-O Complexity chart.png" width="70%" height="60%" title="Big-O 복잡도 이미지"></img></p>
      
    * 공간 복잡도(Space Complexity)
      ```
      알고리즘 실행 후 완료하는데 필요한 **메모리의 양**  
      
      FYR) 저장 기술의 발달로 인해 현재는 시간 복잡도를 우선 고려하는 경우가 많다.
      ```
    * 시간 복잡도(Time Complexity)  
      ```
      입력 값의 개수와 알고리즘의 처리 시간과의 상관관계를 표현한 말  
      
      알고리즘을 수행하기 위해 프로세스가 수행해야하는 연산을 수치화 한 것  
      → 입력된 N의 크기에 따라 실행되는 조작의 수
      
      왜 연산 수치로 판별하는지? 알고리즘 실행시간은 컴퓨터의 처리속도, 프로그래밍 언어에 따라
      편차가 크기 때문에 명령어의 실행횟수만 고려
      ```
     
      중요하게 보는 것은 가장 큰 영향을 미치는 n의 단위
      |실행횟수|Big-O표기|영향|
      |:--:|:--:|:---|
      |1|O(1)|→ 상수|
      |2n+20|O(n)|→ n이 가장 큰 영향을 미침|
      |3n²|O(n²)|→ n²이 가장 큰 영향을 미침|
      |(3^N)M|O((3^N)M)|→ (3^N)M이 가장 큰 영향을 미침|
      
      문제 해결 단계
      ```
      O(1) – 상수 시간 : 문제를 해결하는데 오직 한 단계만 처리
      
      O(log n) – 로그 시간 : 문제를 해결하는데 필요한 단계들이 연산마다 특정 요인에 의해 줄어듬
      
      O(n) – 직선적 시간 : 문제를 해결하기 위한 단계의 수와 입력값 n이 1:1 관계를 가짐
      
      O(n log n) - 로그 선형 시간: 문제를 해결하기 위한 단계의 수가 N*(log2N) 번만큼의 수행시간을 가짐
      
      O(n²) – 2차 시간 : 문제를 해결하기 위한 단계의 수는 입력값 n의 제곱
      
      O(C^n) – 지수 시간 : 문제를 해결하기 위한 단계의 수는 주어진 상수값 C 의 n 제곱
      ```
      <p align="center"><img src="/img/Algorithm/Big-O function ranking.png" width="40%" height="50%" title="Big-O 시간복잡도 랭킹"></img></p>
      
      구하는 요령(유형 파악 예시)
      ```
      하나의 루프를 사용하여 단일 요소 집합을 반복 하는 경우 : O (n)
      
      컬렉션의 절반 이상 을 반복 하는 경우 : O (n / 2) -> O (n)
      
      두 개의 다른 루프를 사용하여 두 개의 개별 콜렉션을 반복 할 경우 : O (n + m) -> O (n)
      
      두 개의 중첩 루프를 사용하여 단일 컬렉션을 반복하는 경우 : O (n²)
      
      두 개의 중첩 루프를 사용하여 두 개의 다른 콜렉션을 반복 할 경우 : O (n * m) -> O (n²)
      
      컬렉션 정렬을 사용하는 경우 : O(n*log(n))
      ```
      정렬 알고리즘 시간복잡도 비교
      <p align="center"><img src="/img/Algorithm/Array Sorting.png" width="70%" height="60%" title="정렬 알고리즘 시간복잡도 비교"></img></p>  
      
      자료구조 시간복잡도 비교
      <p align="center"><img src="/img/Algorithm/Data Structure image.png" width="80%" height="70%" title="자료구조 시간복잡도 비교"></img></p>
## Reference
  - [Yena Choi 알고리즘 공부 시작 방법 및 순서](https://blog.yena.io/studynote/2018/11/14/Algorithm-Basic.html)
  - [알고리즘과 성능 척도 #1](https://godgod732.tistory.com/9?category=659135)
  - [위키백과 점근 표기법](https://ko.wikipedia.org/wiki/%EC%A0%90%EA%B7%BC_%ED%91%9C%EA%B8%B0%EB%B2%95)
  - [Khan Academy 점근적 표기법](https://ko.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/asymptotic-notation)
  - [견우와 직녀 점근적 표기법](https://ledgku.tistory.com/31)
  - [Chulgil.Lee 알고리즘의 시간 복잡도와 Big-O 쉽게 이해하기](https://blog.chulgil.me/algorithm/)
  - [Big-O Complexity Chart](https://www.bigocheatsheet.com/)
  - [까스활명문.log 시간복잡도와 Big_O-표기법](https://velog.io/@jeongho3786/Time-Complexity-%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84%EC%99%80-Big-O-%ED%91%9C%EA%B8%B0%EB%B2%95)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Algorithm/README.md "Go README.md")
