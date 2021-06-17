# 정적 팩토리 메서드(Static Factory Method)

## 목차
1. [정적 팩토리 메서드란?](#1-정적-팩토리-메서드)    
1-1. [유래](#1-1-유래)  
1-2. [취지](#1-2-취지)  
1-3. [정리](#1-3-정리)  
1-4. [코드 예시](#1-4-코드-예시)  
2. [생성자와 정적 팩토리 메서드](#2-생성자와-정적-팩토리-메서드)  
2-1. [왜 정적 팩토리 메서드를 사용하는가?](#2-1-왜-정적-팩토리-메서드를-사용하는가)  
2-2. [장점1 - 이름을 가질 수 있음](#2-2-장점1--이름을-가질-수-있음)  
2-3. [장점2 - 호출할 때마다 새로운 객체 생성할 필요가 없음](#2-3-장점2--호출할-때마다-새로운-객체-생성할-필요가-없음)  
2-4. [장점3 - 하위 자료형 객체를 반환할 수 있음](#2-4-장점3--하위-자료형-객체를-반환할-수-있음)  
2-5. [장점4 - 객체 생성을 캡슐화 할 수 있음](#2-5-장점4--객체-생성을-캡슐화-할-수-있음)  
2-6. [정리](#2-6-정리)  
3. [정적 팩토리 메서드 네이밍 컨벤션](#3-정적-팩토리-메서드-네이밍-컨벤션)  

***
### 1. 정적 팩토리 메서드란?
  - #### 1-1. 유래
    - GoF 디자인 패턴 중 팩토리 패턴에서 유래
  - #### 1-2. 취지
    - 객체를 생성하는 역할을 분리하고자 함  
  - #### 1-3. 정리
    - `객체 생성의 역할을 하는 클래스 메서드`
  - #### 1-4. 코드 예시
    ```java 
    class LocalTime {
      
      ...
      
      public static LocalTime of(int hour, int minute) {
        ChronoField.HOUR_OF_DAY.checkValidValue((long)hour);
        if (minute == 0) {
          return HOURS[hour];
        } else {
          ChronoField.MINUTE_OF_HOUR.checkValidValue((long)minute);
          return new LocalTime(hour, minute, 0, 0);
        }
      }
    }
    
    ...

    // hour, minutes을 인자로 받아서 9시 30분을 의미하는 LocalTime 객체를 반환
    LocalTime openTime = LocalTime.of(9, 30); 
    ```
  
### 2. 생성자와 정적 팩토리 메서드
  - #### 2-1. 왜 정적 팩토리 메서드를 사용하는가?
    - 생성자 : 객체를 생성하는 역할
    - 정적 팩토리 메서드 : 메서드를 통해 객체 생성
    - "생성자 대신 정적 팩토리 메서드를 고려하라" (이펙티브 자바 내용 중)
  - #### 2-2. 장점1 - 이름을 가질 수 있음   
    - 생성자를 통해 객체 생성시
      ```
      객체는 생성 목적과 과정에 따라 생성자를 구별해서 사용해야함.
      new 클래스명(...)을 통해 객체를 생성 시 내부 구조를 잘 알고 있어야 목적에 맞게 객체 생성 가능
      ```
    - 정적 팩토리 메서드 사용시
      ```java
      public class LottoFactory() {
        private static final int LOTTO_SIZE = 6;
        
        // 1~45까지의 로또 번호
        private static List<LottoNumber> allLottoNumbers = ...; 
        
        // 메서드 이름을 보고 생성의 목적을 알 수 있음 -> 가독성 증가
        public static Lotto createAutoLotto() {
          Collections.shuffle(allLottoNumbers);
          return new Lotto(allLottoNumbers.stream()
                  .limit(LOTTO_SIZE)
                  .collect(Collectors.toList()));
        }
        
        public static Lotto createManualLotto(List<LottoNumber> lottoNumbers) {
          return new Lotto(lottoNumbers);
        }
        ...
      }
      ```
      
  - #### 2-3. 장점2 - 호출할 때마다 새로운 객체 생성할 필요가 없음
    - enum과 같이 자주 사용되는 요소의 개수가 정해져 있는 경우
      ```java
      class Node {
        private enum Direction {
          LEFT, CENTER, RIGHT;
        }

        private Direction direction;
        
        // 생성자의 접근 제한자를 private으로 설정하여 객체 생성을 정적 팩토리 메서드로만 가능하도록 제한
        // 즉, 범위를 벗어나는 생성을 막을 수 있음.
        private Node(Direction direction) {
          this.direction = direction;
        }

        ...
        
        // 정적 팩토리 메서드
        static Node createCenterNode() {
          return new Node(Direction.CENTER);
        }

        static Node createRightNode() {
          return new Node(Direction.RIGHT);
        }

        static Node createLeftNode() {
          return new Node(Direction.LEFT);
        }
        
        ...
      ```
    - 클래스 안에서 반복문을 통해 생성하는 경우  
      ```java
      public class LottoNumber {
        private static final int MIN_LOTTO_NUMBER = 1;
        private static final int MAX_LOTTO_NUMBER = 45;

        private static Map<Integer, LottoNumber> lottoNumberCache = new HashMap<>();

        static {
          IntStream.range(MIN_LOTTO_NUMBER, MAX_LOTTO_NUMBER)
                      .forEach(i -> lottoNumberCache.put(i, new LottoNumber(i)));
        }

        private int number;

        private LottoNumber(int number) {  
          this.number = number;
        }
        
        // LottoNumber를 반환하는 정적 팩토리 메서드
        public LottoNumber of(int number) {  
          return lottoNumberCache.get(number);
        }

        ...
      }
      ```
  - #### 2-4. 장점3 - 하위 자료형 객체를 반환할 수 있음
    - 상속을 사용시 확인 가능
    - 생성자의 역할을 하는 정적 팩토리 메서드가 반환값을 가지고 있기 떄문에 가능
    - 시험 점수에 따라 등급 타입을 반환하는 정적 팩토리 메서드  
      구조 : Basic, Intermediate, Advanced 클래스가 Level라는 상위 타입을 상속
      ```java
      public class Level {
      
      ... 
      
      public static Level of(int score) {
        if (score < 50) {
          return new Basic();
        } else if (score < 80) {
          return new Intermediate();
        } else {
          return new Advanced();
        }
      }
      
      ...
      }
      ```
  - #### 2-5. 장점4 - 객체 생성을 캡슐화 할 수 있음
    - 캡슐화?
      ```
      데이터의 은닉, 여기서는 생성자를 클래스의 메서드 안으로 숨기면서
      내부 상태를 외부에 노출시킬 필요 없이 객체 생성 인터페이스 단순화 시킬 수 있음
      ```
    - DTO(데이터 전송 위한 객체, catDto)와 Entity(Car) 예시
      ```java
      public class CarDto {
        private String name;
        private int position;
        
        ...
        
        pulbic static CarDto from(Car car) {
          return new CarDto(car.getName(), car.getPosition());
        }
      }


      // 정적 팩토리 메서드 사용하여 Car -> CatDto 로 변환시 내부 구현을 노출할 필요 없음
      CarDto carDto = CarDto.from(car);
      
      // 생성자 사용하여 Car -> CatDto 로 변환시 내부 구현을 노출됨
      CarDto carDto = new CarDto(car.getName(), car.getPosition);
      ```
  - #### 2-6. 정리
    - 생성자의 역할을 대신 할 수 있음 + 가독성 좋은 코드 작성, 객체지향적으로 프로그래밍할 수 있도록 도움
    - 객체간 형 변환이 필요한 경우, 여러 번의 객체 생성이 필요한 경우 활용하면 좋음
    - 참고! 팩토리 메서드만 존재하는 클래스 생성 시 상속 불가  
      왜? 상속을 위해서는 public 이나 protected 접근 제어자를 가진 생성자 필요하기 떄문

### 3. 정적 팩토리 메서드 네이밍 컨벤션
    - from : 하나의 매개 변수를 받아서 객체를 생성
    - of : 여러개의 매개 변수를 받아서 객체를 생성
    - getInstance | instance : 인스턴스를 생성, 이전에 반환했던 것과 같을 수 있음
    - newInstance | create : 새로운 인스턴스를 생성
    - get[OtherType] : 다른 타입의 인스턴스를 생성, 이전에 반환했던 것과 같을 수 있음
    - new[OtherType] : 다른 타입의 새로운 인스턴스를 생성
    
## Reference   
  - [yeonseok 정적 팩토리 메서드](https://velog.io/@ljinsk3/%EC%A0%95%EC%A0%81-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9C%EB%8A%94-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C)     
  - [피누 생성자 대신 정적 팩토리 메서드를 고려하라](https://velog.io/@litien/%EC%83%9D%EC%84%B1%EC%9E%90-%EB%8C%80%EC%8B%A0-%EC%A0%95%EC%A0%81-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9C%EB%A5%BC-%EA%B3%A0%EB%A0%A4%ED%95%98%EB%9D%BC)  

***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")
