# DTO와 VO

## 목차
1. [DTO와 VO](#1-dto와-vo)  
1-1. [DTO와 VO는 같은 개념인가?](#1-1-dto와-vo는-같은-개념인가)  
1-2. [DTO](#1-2-dto)  
1-3. [VO](#1-3-vo)  
1-4. [정리](#1-4-정리)  

***

### 1. DTO와 VO
  - #### 1-1. DTO와 VO는 같은 개념인가?
    - 검색을 하면 대부분 동일한 개념으로 설명한다.  
    - 하지만, 마틴 파울러의 저서 Patterns of Enterprise Application Architecture에 답이 나와 있음  
  
  - #### 1-2. DTO
    - DTO : 데이터 전달용  
    
    - 의미   
      DTO(Data Transfer Object)  
      `데이터를 전달`하기 위해 사용하는 객체  
      쉽게 생각한다면 `데이터를 담아서 전달하는 바구니`라고 생각하면 됨  
    
    - 개념  
      ![image](https://user-images.githubusercontent.com/65080004/118463092-53fce180-b73a-11eb-950a-fe7eaa3c842b.png)  
      Controller(Web Layer)와 Service(Service Layer) 둘 사이에서 데이터를 주고 받기위해 DTO를 사용  
    
    - 특징
      - getter/setter 메서드만을 갖는다.  
      - 다른 로직을 갖지 않는다.  
        왜? 순수하게 데이터 전달만을 위한 객체이기 때문에 이외의 비즈니스 로직은 굳이 있을 필요 없음  
    
    - 예시
      ```java
      // 해당 DTO는 setter 메소드를 가지므로 데이터가 가변적
      // 왜? setter 메소드로 새로운 값을 설정하면 되기 떄문에
      public class CrewDto {
        private String name;
        private String nickname;
        
        public String getName() {
          return name;
        }
        
        public void setName(String name) {
          this.name = name;
        }
        
        public String getNickname() {
          return nickname;
        }
        
        public void setNickname(String nickname) {
          this.nickname = nickname;
        }
      }
      
      // setter 메서드를 삭제하고 생성자를 통해 속성값을 초기화하게 한다면 불변객체로 만들 수 있음
      // 전달과정 중 데이터 불변성을 보장할 수 있음
      public class CrewDto {
        private String name;
        private String nickname;
        
        public CrewDto(String name, String nickname) {
          this.name = name;
          this.nickname = nickname;
        }
        
        public String getName() {
          return name;
        }
       
        public String getNickname() {
          return nickname;
        }
      }
      ```
  - #### 1-3. VO
    - VO : 값 표현 용  
    
    - 의미
      VO(Value Object)  
      `값 그 자체를 표현`하는 객체  
    
    - 핵심역할
      `equals()와 hashCode()를 오버라이딩 하는 것`  
      
      왜 해당 메서드들을 오버라이딩하는가?  
      `두 객체의 모든 필드 값들이 동일하면 두 객체는 같다.`라는 것을 증명하기 위해  
      두 객체의 모든 필드 값들이 모두 같으면 같은 객체이도록 만들 수 있는 equals(), hashCode() 오버라이딩  
    
    - 특징  
      setter 성격의 메서드는 없애고 `불변 객체`로 만들어야함    
      왜? 특정 값 자체를 표현하기 때문에  
    
    - 구현
      ```java
      public class Money {
        // 속성 value
        private final int value;
        
        // 값 자체를 표현하기에 불변객체여야함
        // 따라서 setter 성격의 메서드를 포함하면 안되며, 생성자를 통해 초기화
        public Money(int value) {
          this.value = value;
        }
        // getter, setter 이외 로직 포함 가능
        public int getHalfValue() {
          return value / 2;
        }
        
        @Override
        public boolean equals(Object o) {
          if(this == o) {
            return true;
          }
          if(!(o instanceof Money)) {
            return false;
          }
          Money money = (Money) o;
          return value == money.value;
        }
        
        @Override
        public int hashCode() {
          return Object.hash(value);
        }
      }
      ```
  - #### 1-4. 정리
    ||DTO|VO|
    |:---:|:---:|:---:|
    |용도|레이어 간 데이터 전달|값 자체 표현|
    |동등 결정|속성값이 모두 같다고 해서 같은 객체가 아님|속성값이 모두 같으면 같은 객체|
    |가변/불변|setter 존재 시 가변, 존재X시 불변|불변|
    |로직|getter/setter외 로직 갖지 X| getter/setter외의 로직 가질 수 있음|
  

  - #### 1-5. Reference
    - [taehee-kim-dev.log DTO, VO](https://velog.io/@taehee-kim-dev/DTO-vs-VO)    
    - [우아한 tech DTO, VO](https://www.youtube.com/watch?v=z5fUkck_RZM)  
    - [gil.log Entity, DTO, VO 바로알기](https://velog.io/@gillog/Entity-DTO-VO-%EB%B0%94%EB%A1%9C-%EC%95%8C%EA%B8%B0#%E2%99%82%EF%B8%8F-%EC%B0%B8%EA%B3%A0%EC%82%AC%EC%9D%B4%ED%8A%B8-%E2%99%82%EF%B8%8F)  
    - [긴이별을 위한 짧은 편지 DTO란 무엇인가](https://kafcamus.tistory.com/13)  
    - [손너잘 DTO, VO ](https://bperhaps.tistory.com/entry/DTO%EC%99%80-VO-%EC%9D%98%EB%AC%B8%EC%97%90-%EB%8C%80%ED%95%9C-%EB%8B%B5%EB%B3%80-DTO%EC%99%80-VO%EB%8A%94-%EC%99%9C-%ED%98%BC%EC%9A%A9%EB%90%98%EB%8A%94%EA%B0%80-DTO%EB%8A%94-%EC%99%9C-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94%EA%B0%80-VO%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)  
