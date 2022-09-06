# net-tools

## 목차
 1. [net-tools란?](#net-tools란)    
 2. [설치 방법](#설치-방법)    
 3. [대체 명령어와 비교](#대체-명령어와-비교)    
---
### net-tools란?
  - Linux 운영 체제용 NET-3 네트워킹 배포의 기본적인 세트를 구성하는 프로그램들의 모음
  - 간단하게, `Linux 운영체제용 네트워크 관련 도구 모음`

### 설치 방법  
  - 명령어    
    ```console
    sudo apt install net-tools
    ```

### 대체 명령어와 비교
| 프로그램 명 | Linux 대체 명령어 | 기능 | 
|:-:|:-:|:-:|
| arp | ip neigh | 연결하려는 시스템의 MAC 주소 확인 |
|ifconfig | ip addr | 네트워크 인터페이스 구성 확인 |
|ipmaddr | ip maddr |
|iptunnel | ip tunnel |
|route | ip route | 라우터 설정정보 확인 |
|nameif | ifrename |
|mii-tool | ethtool |