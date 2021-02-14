# List와 ArrayList 객체 생성시 차이
  - List list = new ArrayList(); 와 ArrayList list = new ArrayList(); 의 차이?
    ```java
    - List<Object> list = new ArrayList<>();
    - ArrayList<Object> list = new ArrayList<>();
    ```  
    
    * List → 인터페이스 / ArrayList, LinkedList → 리스트에 상속된 클래스  
    
    * 위 코드를 실행 시 같은 결과를 도출하지만 List 인터페이스를 사용하여 ArrayList 생성 시 **유연성 ↑**  
    
    * 유연성 예시 코드  
      ```java
      List<Object> list = new ArrayList<>(); // 빠른 탐색을 위함
      List<Object> list = new LinkedList<>(); // 삽입,삭제를 위함
      위의 코드(↑)처럼 구현함으로써 내부 디테일과 메모리 함축에서 이점과 성능을 개선 가능
      ```  
  - 자바의 다형성  
    * 다형성?  
      → 하나의 메소드나 클래스가 있을 때 이것들이 다양한 방법으로 동작하는 것을 의미  
        즉, 동일한 조작방법으로 동작시키지만 동작방법은 다른 것  
    
    * 도형에 비유한 코드
      ```java
      List<Object> list = new ArrayList<>();
       → 도형 list = new 정사각형();
      List<Object> list = new LinkedList<>();
       →  도형 list = new 직사각형();
      ArrayList list = new ArrayList();
       → 정사각형 list = new 정사각형();
       위의 코드(↑)처럼 도형 타입으로 생성시 도형 인터페이스를 구현한 클래스에서 사용 가능
       그러나 정사각형 클래스로 생성시 해당 클래스 외에는 사용 불가
      ```  
   - 결론  
     ```
     List를 상속받은 클래스를 사용할 경우 'List<Object> list = new 상속받은 클래스()' 를 사용하여 유연성을 높이자
     ```
## Reference
  - [개인주의 List와 ArrayList 차이](https://galgum.tistory.com/18)
  - [알면 쓸모있는 개발 지식 List와 ArrayList 차이](https://yoon-dailylife.tistory.com/7)
  - [심플. List와 ArrayList 차이](http://be-simple-and-kind.blogspot.com/2017/07/list-arraylist.html)
  - [Opentutorials.org 다형성](https://opentutorials.org/module/516/6127)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
