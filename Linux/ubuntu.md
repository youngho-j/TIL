# Ubuntu

## 목차
 1. [ISO 이미지란?](#iso-이미지란)  
 2. [Ubuntu server](#ubuntu-server)  
 3. [대체 명령어와 비교](#ubuntu-server와-desktop의-차이)  
 4. [우분투 서버 버전 live ISO 다운로드](#우분투-서버-버전-live-iso-다운로드)  
---
### ISO 이미지란?
  - 국제 표준화 기구(ISO)가 제정한 광학 디스크의 압축 파일(디스크 이미지)  
  - ISO 이미지는 압축된 BD(블루레이 디스크)나 CD를 비롯한 디스크 포맷에 포함된 `모든 파일 데이터를 압축되지 않은 형태로 담고있음`  
  - 파일 확장자는 일반적으로 `.iso` 확장자를 가짐  

### Ubuntu server?  
  - 추가 정리 필요

### Ubuntu server와 Desktop의 차이
  - `GUI 포함 여부`(server에는 GUI가 포함되어 있지 않음)
    - 설치시 차이가 있음(server의 경우 프로세스 중심 메뉴를 사용)   
  - 사용 목적의 차이
    - Ubuntu Desktop : 호스트 컴퓨터에서 사용하는 데 중점  
    - Ubuntu Server : 보안 + 클라이언트와의 연결을 허용하는 데 중점 
    - 따라서 설치되는 패키지 또는 응용프로그램의 차이가 있음
  - 성능의 차이
    - 보통 같은 사양일 경우 server가 성능이 좋음
    - 단, 여러 어플리케이션이 혼합되면 상황이 달라짐
  - 결론
    - GUI를 제외하면 `큰 차이는 없다.`
    - 데스크탑과 서버용 모두 같은 커널을 사용하기 떄문


### 우분투 서버 버전 live ISO 다운로드
  - [Ubuntu server download](https://ubuntu.com/download/server) 
  - [kakao mirror에서 다운로드](https://mirror.kakao.com/ubuntu-releases/)  
    - 해당 mirror 서버에서 받을 경우 공식사이트 다운로드보다 빠름  
  - [한국이 아닌경우 다른 mirror 서버 찾기](https://launchpad.net/ubuntu/+cdmirrors)   