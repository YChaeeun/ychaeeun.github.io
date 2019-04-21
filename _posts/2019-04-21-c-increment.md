---
title: c 전위후위 증감연산자 prefix & postfix increment operator
date: 2019-04-21
categories:
 - C
---



## 증감연산자

증감 연산자는 `변수++`,  `변수--`,  `++변수`,  `--변수` 으로 `변수 = 변수 + 1` 과 같은 연산을 

짧게 쓴 것이다. 저 연산자들이 앞에 붙느냐, 뒤에 붙느냐는 큰 차이가 있다.





## 전위 증감연산자 prefix increment operator

- `++변수` , `--변수`

- 먼저 변수의 값을 변화시킨 다음, 해당 변수에 연산한 값을 할당한다! 

  ```c
  int i = 10;
  printf("%d", ++i);  # 11   # 먼저 i의 값을 +1 한 뒤에, printf를 실행함
  printf("%d", i);    # 11
  ```

  



## 후위 증감 연산자 postfix increment operator

- `변수++`, `변수--`

- 연산한 값을 할당하거나 동작을 한 뒤에, 변수의 값을 변화시킨다.

  ```c
  int i = 10;
  printf("%d", i--);  # 10    # printf를 실행한 뒤에 -1을 수행함
  printf("%d", i);    # 9
  ```

  



## 문자 자료형에서 사용하기

- 문자 자료형에서 사용하면 아스키코드 값에서 더하거나 빼기가 이루어진다.

  ```c
  char a1 = 'A';
  printf('%c', ++a1);  # B
  
  char a2 = 'B';
  prinf("%c", --a2)    # A
  ```

  