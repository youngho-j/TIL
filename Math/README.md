# 제곱과 제곱근 차이
  - 제곱(square)?
    ```
    * 같은 수를 두 번 반복해서 곱하는 계산
    * Ex) 2의 제곱 -> 2 × 2 / 기호 : 2²
  - 루트(root)?
    ```
    * 제곱의 반대 -> '어떤수'를 두 번 곱했을때 해당 수가 나왔을까요? 라는 질문에서 '어떤수'에 해당
    * 기호
    * Ex) √9(루트 9) = 3
  - 제곱근(square root)?
    ```
    * 무엇을 제곱하면 해당 수가 되는지 그 정답을 찾으시오 라고 보면됨 -> 무엇을 찾는 것!
    * Ex) 144의 제곱근을 구하시오 -> ±12[+12, -12]
    * Ex) -5의 제곱근을 구하시오 -> ±√-5[+√-5, -√-5]
## Reference
  - https://m.blog.naver.com/PostView.nhn?blogId=sbssbi69&logNo=220221686187&proxyReferer=https:%2F%2Fwww.google.com%2F
  - [근사값 참고] (https://blog.naver.com/jugbong/40055730668)
    
# 에라토스테네스의 체
  - 에라토스테네스의 체
    ```
    - 특정 범위가 주어지고 그 범위 내의 모든 소수를 찾아야하는 경우 빠르고 정확하게 구할 수 있음
    - 대량의 소수를 판별할때 이용하면 좋음  
  - 원리
    ```
    1. 배열을 생성하여 초기화
    2. 2부터 시작하여 특정 수의 배수에 해당하는 수를 모두 지움(주어진 자연수 √N 보다 같거나 작은수까지 구하면 됨)
      * 1은 소수가 아님
      * 지울때 자기 자신은 지우지 않음 Ex) 2를 제외한 나머지 2의 배수 지우기
    3. 이미 지워진 수는 건너 뜀
    4. 해당 범위의 소수 모두 출력
## Reference
  - https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4
  - https://coding-factory.tistory.com/600