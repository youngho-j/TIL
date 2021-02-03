# 재귀 알고리즘 
  - 재귀 함수 : 어떤 함수 내에서 자기 자신(함수)을 다시 호출하여 작업을 수행하는 방식의 함수   
    → 함수를 연이어 호출 시 스택처럼 메모리에 쌓임(push)   
    → 쌓인 역순으로 하나씩 실행(pop) like stack
  - 함수내에서 다시 자신을 호출한 뒤 그 함수가 끝날 때 까지 함수 호출 이후의 명령문 수행되지 X
  - stack overflow를 방지하기 위해 종료조건이 꼭 포함 되어어야함 
  
  - 실행 예제(팩토리얼)
    ~~~ java
	  public static void main(String[] args) throws IOException {
		  BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		  int num = Integer.parseInt(br.readLine());
		  System.out.println(recursive(num));
	  }
    ~~~
    ~~~ java
    public static int recursive(int n) {
      if(n <= 1) {
        return 1;
      } else {
          return n * recursive(n-1);
      }
    }
    ~~~
  - 실행 과정
    | n = 3        | n = 2        | n = 1        |       →      |              |              |              |    결과      |
    | :----------: | :----------: | :----------: | :----------: | :----------: | :----------: | :----------: | :----------: |
    |              |              | recursive(1) |              | return 1     |              |              |              |
    |              | recursive(2) | recursive(2) |              |              | return 1 * 2 |              |              |
    | recursive(3) | recursive(3) | recursive(3) |              |              |              | return 1 * 2 * 3 | 3! = 6   |
       
  - stack overflow 
     * 각각 주어진 스택 메모리보다 데이터를 더 넣거나, 스택이 메모리가 비어있는데 거기서 데이터를 꺼내려했을때 발생
## Reference
  - https://gomguard.tistory.com/111
  - https://smile2x.tistory.com/entry/%EC%9E%AC%EA%B7%80%ED%95%A8%EC%88%98%EC%9D%98-%EC%9B%90%EB%A6%AC-%EB%B0%8F-%EB%8F%99%EC%9E%91
   
# 분할 정복법
  - 여러 알고리즘의 기본이 되는 해결 방법
  - 엄청나게 크고 방대한 문제를 조금씩 나눠가면서 용이하게 풀 수 있는 문제 단위로 나눈 뒤 그것들을 다시 합하여 해결   
    → 주어진 문제를 작은 사례로 나누고 각각의 작은 문제들을 해결하여 정복하는 방법
  - 하향식 접근 방법 → 아래로 내려가면서 작은 사례에 대한 해답을 구함으로써 최상위 사례의 해답을 구함
  - 설계전략 (상단 분할, 중앙 정복, 하단 조합)
    ```
    분할 : 문제를 동일한 유형의 여러 하위 문제로 나눔
    정복 : 가장 작은 단위의 하위 문제를 해결하여 정복
    조합 : 하위 문제에 대한 결과를 원래 문제에 대한 결과로 조합
    ```
  - 예시  
    * 이분검색, 합병정렬, 퀵정렬, 최대값 찾기, 임계값의 결정, 쉬트라센 행렬곱셈 알고리즘 등
    
  - 장, 단점
    * 장점 
      1. 문제를 나눔으로써 어려운 문제를 해결할 수 있음
      2. 문제를 나누어 해결한다는 특징상 병렬적으로 문제를 해결하는 데 큰 강점이 있음

    * 단점
      1. 함수를 재귀적으로 호출한다는 점에서 함수 호출로 인한 오버헤드가 발생 가능
      2. 스택에 다양한 데이터를 보관하고 있어야 하므로 스택 오버플로우가 발생하거나 과도한 메모리 사용을 하게 됨
      3. 문제에 따라 알고리즘의 퍼포먼스의 차이 발생 가능

## Reference
  - https://namu.wiki/w/%EB%B6%84%ED%95%A0%20%EC%A0%95%EB%B3%B5%EB%B2%95
  - https://kimch3617.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%B6%84%ED%95%A0%EC%A0%95%EB%B3%B5%EB%B2%95-Divide-and-Conquer

# 하노이의 탑 
  - 1883년 프랑스 수학자 에두아르 뤼카가 소개한 문제
    <이미지 추가 Tower_of_Hanoi.jpeg>
  - 재귀 호출을 이용하여 풀 수 있는 가장 유명한 예제 중 하나
  - 아래 두 가지 조건을 만족시키면서, 한 기둥에 꽂힌 원판들을 그 순서 그대로 다른 기둥으로 옮겨서 다시 쌓는 것
    1. 한 번에 하나의 원판만 옮길 수 있으며, 막대에서 막대로만 움직일 수 있다.
    2. 큰 원판이 작은 원판 위에 있어서는 안 된다.
  - 이동 횟수 구하기
    
    
## Reference
  - https://ko.wikipedia.org/wiki/%ED%95%98%EB%85%B8%EC%9D%B4%EC%9D%98_%ED%83%91
  - https://kimch3617.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%B6%84%ED%95%A0%EC%A0%95%EB%B3%B5%EB%B2%95-Divide-and-Conquer
