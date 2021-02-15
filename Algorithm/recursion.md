# 재귀 알고리즘 
  - 재귀 함수 : 어떤 함수 내에서 자기 자신(함수)을 다시 호출하여 작업을 수행하는 방식의 함수   
    → 함수를 연이어 호출 시 스택처럼 메모리에 쌓임(push)   
    → 쌓인 역순으로 하나씩 실행(pop) like stack  

  - 함수내에서 다시 자신을 호출한 뒤 그 함수가 끝날 때 까지 함수 호출 이후의 명령문 수행되지 X
  
  - stack overflow를 방지하기 위해 종료조건이 꼭 포함 되어어야함 
  
  - 이미지
    <p align="center"><img src="/img/Algorithm/Recursion_via_vlc.png" width="70%" height="60%" title="재귀 이미지"></img></p>  
    <p align="center">화면 녹화 프로그램에서의 재귀. 화면 속에 작은 화면이 무한히 들어간다. vlc team, ubuntu, Hidro (talk) - 자작</p>  
    
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
  - [곰가드의 라이브러리 재귀 알고리즘](https://gomguard.tistory.com/111)
  - [스티브김스 재귀함수의 원리와 동작](https://smile2x.tistory.com/entry/%EC%9E%AC%EA%B7%80%ED%95%A8%EC%88%98%EC%9D%98-%EC%9B%90%EB%A6%AC-%EB%B0%8F-%EB%8F%99%EC%9E%91)
  - [위키피디아 재귀 이미지](https://ko.wikipedia.org/wiki/%EC%9E%AC%EA%B7%80_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)#/media/%ED%8C%8C%EC%9D%BC:Screenshot_Recursion_via_vlc.png)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Algorithm/README.md "Go README.md")
