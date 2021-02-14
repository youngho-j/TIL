# 익명 클래스(Anonymous class)
  - 클래스의 선언과 객체의 생성을 동시에 함  
    따라서, **단 한 번만 사용될 수 있고 오직 하나의 객체만을 생성**할 수 있는 **일회용 클래스**이다.  

  - 이름이 없다
    즉, 생성자를 가질 수 없다. 만들어진 클래스의 생성자와 동일하게 객체를 생성할 뿐이다.  
    그럼 어떻게 생성하는가? 부모 클래스의 이름이나 구현하고자 하는 인터페이스의 이름을 사용해서 정의  
    ```java
    // Thread 익명 클래스 구현
    Thread t = new Thread(new Runnable() {
		  @Override
			public void run() {
				System.out.println("Child");
			}
		});
    
    // 여기서 t는 Thread 클래스를 확장한 익명 클래스의 객체
		t.start();
		System.out.println("Main");
    
    // Comperator 인터페이스로 익명 클래스 구현
    Arrays.sort(list, new Comparator<String>() {
			@Override
			public int compare(String o1, String o2) {
    // 문자열 길이가 짧은 순으로 정렬(오름차순), 같은 길이일 경우 사전 순서대로 오름차순
				if(o1.length() == o2.length()) {
					return o1.compareTo(o2);
				} else {
					return o1.length() - o2.length();
				}
			}
		});
    
    → 클래스 선언과 동시에 힙에 인스턴스가 생성된 후 선언한 변수에 생성된 인스턴스의 주소값을 저장
    ```

  - 단 하나의 인터페이스/클래스만을 구현 할 수 있음 

  - 사용 목적
    * 부모 클래스를 상속 받는 서브 클래스를 생성하지 않고도,  
      단일 객체를 만들어서 부모 클래스에 정의된 동작에서 행위를 추가 할 수 있음  
      → 상속한 것으로 처리가 된다고 보면 됨  
    * 단, 한번 밖에 쓰이지 않을 클래스를 익명 클래스를 사용하여 처리

  - 단점 
    
    * 코드가 지저분해질 수 있음
  
  - 알아두면 좋을수도?
    * 클래스 파일명 → '(외부 클래스명)$(숫자).class' 형식으로 결정
    * Ex) 익명 클래스 사용 후 class sortList 컴파일시 → 'sortList.java', 'sortList.class', 'sortList$1.class' 파일 생성

## Reference
  - [Daniel 익명 클래스](https://dduddublog.tistory.com/169)
  - [syundev 익명 클래스](https://syundev.tistory.com/)
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
