# Spring AOP 개념 이해하기
## 목차
1. [AOP](#1-aop)     
1-1. [AOP란?](#1-1-aop란)    

***
### 1. AOP
  - #### 1-1. AOP란?
    - Aspect Oriented Programming
    
    - 관점(관심) 지향 프로그래밍 쉽게 말한다면, 프로젝트 구조를 `바라보는 관점을 바꿔서 보는 것`  
    
    - 예를 들어 은행이라는 프로그램에 이체, 대출승인, 이자계산 3가지의 서비스가 존재한다고 가정한 뒤 생각해보면,  
      은행의 각 서비스의 핵심기능에는 계좌이체, 대출승인, 이자계산 기능이 존재하며,   
      각자 자신만의 코드를 구현하고 있음을 볼 수 있음  
      
      ![image](https://user-images.githubusercontent.com/65080004/118761333-31400980-b8af-11eb-849d-3c07c93cfd05.png)  
    
    - 이 관점을 핵심기능에서 보는게 아닌 부가기능적인 관점에서 바라본다면 아래 그림과 같이 볼 수 있으며,  
      로깅, 보안, 트랜잭션 기능이 공통되는 것을 알 수 있음
      
      ![image](https://user-images.githubusercontent.com/65080004/118762052-84668c00-b8b0-11eb-9853-da5f5496a9d0.png)  

    - AOP는 기존 OOP에서 `바라보던 관점을 다르게 하여 부가기능적인 관점에서 보았을때 공통된 요소를 추출하여 모듈화` 하자는 것
   
## Reference
 - [effortDev SpringAOP 내용정리](https://shlee0882.tistory.com/206)    
 - [기억보단 기록을 AOP 정리](https://jojoldu.tistory.com/71?category=635883)  
***
