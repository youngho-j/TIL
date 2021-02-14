# 데이터 타입
  - 기본(원시) 타입(primeitive type)
    <table>
      <tr>
        <td>값의 종류</td>
        <td>기본 타입</td>
        <td colspan="2">메모리 사용 크기</td>
        <td>기본값</td>
        <td>부호</td>
        <td>범위</td>
        <td>기타</td>
      </tr>
      <tr>
        <td rowspan="5">정수</td>
        <td>byte</td>
        <td>1 byte</td>
        <td>8 bit</td>
        <td>0</td>
        <td>+,-</td>
        <td>-2^7~(2^7-1)<br>[-128~127]</td>
        <td>색상정보, 파일 또는 이미지 등의 <br>이진(바이너리) 데이터 처리시 사용</td>
      </tr>
      <tr>
        <td>char</td>
        <td>2 byte</td>
        <td>16 bit</td>
        <td>\u0000</td>
        <td>없음</td>
        <td>0 ~ 2^16-1<br>(유니코드 : \u0000~\uFFFF, 0~65,535)</td>
        <td>자바는 모든 문자를 유니코드로 처리,<br> 유니코드는 음수 X</td>
      </tr>
      <tr>
        <td>short</td>
        <td>2 byte</td>
        <td>16 bit</td>
        <td>0</td>
        <td>+,-</td>
        <td>-2^15~(2^15-1)<br>-32,768~32,767</td>
        <td>C 언어와의 호환을 위해 사용,<br> 자바에선 비교적 잘 사용하지 않음</td>
      </tr>
      <tr>
        <td>int</td>
        <td>4 byte</td>
        <td>32 bit</td>
        <td>0</td>
        <td>+,-</td>
        <td>-2^31~(2^31-1)<br>-2,147,483,648 ~<br>2,147,483,647</td>
        <td>일반적으로 정수 저장시 사용<br>직접 코드에서 입력시 8, 10, 16진수로 표현 가능,<br>숫자앞 '0'(8진수), '0x'(16진수),<br>값이 2진수로 변환되어 저장 </td>
      </tr>
      <tr>
        <td>long</td>
        <td>8 byte</td>
        <td>64 bit</td>
        <td>0L</td>
        <td>+,-</td>
        <td>-2^63~(2^63-1)<br>-9,223,372,036,854,775,808 ~ <br>9,223,372,036,854,775,807</td>
        <td>수치가 큰 데이터를 다루는 프로그램(은행 및 우주 관련)</td>
      </tr>
      <tr>
        <td rowspan="2">실수</td>
        <td>float</td>
        <td>4 byte</td>
        <td>32 bit</td>
        <td>0.0F</td>
        <td>+,-</td>
        <td>±1.4X10^-45 ~ <br>±3.4028235X10^38</td>
        <td rowspan="2">실수타입 -> 소수점이 있는 실수 데이터를 저장 가능<br>부동 소수점 방식 : ± m X r^e<br>(± : 부호 m : 가수 r : 밑수 e : 지수 )</td>
      </tr>
      <tr>
        <td>double</td>
        <td>8 byte</td>
        <td>64 bit</td>
        <td>0.0 or 0.0d/td>
        <td>+,-</td>
        <td>±4.9X10^-324 ~ <br>±1.7976931348623157X10^308</td>
      </tr>
       <tr>
        <td>논리</td>
        <td>boolean</td>
        <td>1 byte</td>
        <td>8 bit</td>
        <td>false</td>
        <td>없음</td>
        <td>true, false</td>
        <td>두 가지 상태값을 저장할 필요성이 있을 시, <br>조건문, 제어문의 실행 흐름 변경시 주로 사용</td> 
      </tr>
    </table>
    
## Reference   
  - 신용권, 이것이 자바다, 한빛미디어(2019)  
***
[목차로 이동](https://github.com/youngho-j/TIL/blob/main/Java/README.md "Go README.md")  
