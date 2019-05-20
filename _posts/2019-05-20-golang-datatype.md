---
title: golang 기본 자료형 data type
date: 2019-05-20
categories:
 - go
---





## golang 기본 자료형

- Go는 정적 타입의 프로그래밍 언어로, 변수가 항상 특정 타입을 지니고 있고 해당 타입은 변경될 수 없다
- 프로그램이 종료될 때 까지 변하지 않기 때문에 변수 선언 및 관리를 꼼꼼하게 해줘야 한다!

```
bool

string
```

```
int  int8  int16  int32  int64  // 부호가 있는 정수
uint uint8 uint16 uint32 uint64 // 부호가 없는 정수

uintptr // unit과 크기가 동일, 포인터를 저장할 때 사용

byte    // uint8의 다른 이름(alias)

rune    // int32의 다른 이름(alias)
        // 유니코드 코드 포인트 값을 표현합니다. 
```

```
float32 float64

complex64 complex128  // 복소수 (허수부가 있는 숫자)
```





## 0) 불 boolean / bool

- 참(true)과 거짓(false)을 나타내는 데 사용되는 특별한 1비트의 정수
- A && B  : A와 B 모두 참일 때 참 (and)
- A || B  : A와 B 둘 중 참이 한 개 이상일 때 참 (or)
- ! B  :  B가 거짓일 때 참(not)

<table>
    <tr>
        <td>A</td>
        <td>B</td>
        <td>A && B</td>
        <td>A || B</td>
        <td> !B </td>
    </tr>
    <tr>
        <td>true</td>
        <td>true</td>
        <td>true</td>
        <td>true</td>
        <td>false </td>
    </tr>
    <tr>
        <td>true</td>
        <td>false</td>
        <td>false</td>
        <td>true</td>
        <td>true</td>
    </tr>
    <tr>
        <td>false</td>
        <td>true</td>
        <td>false</td>
        <td>true</td>
        <td>false</td>
    </tr>
    <tr>
        <td>false</td>
        <td>false</td>
        <td>false</td>
        <td>false</td>
        <td>true </td>
    </tr>
</table>



## 1) 문자열

- 텍스를 표현하는데 사용하는 자료형이다

- 보통 각 문자는 개별 바이트로 구성되어 있고, 공백 또한 하나의 문자로 간주된다

  ( 0부터 시작하는 인덱스 값이 부여되어 있음)

- " " (큰따옴표)나 `` (역따옴표) 를 사용한다

  - 큰따옴표로 작성한 경우 줄바꿈은 \n 
  - 여러 줄을 작성할 때는 역따옴표가 편리하다

  ```go
  var s1 string = "hello"
  var s2 string = `several
  lines`
  ```

- 문자열은 직접 수정이 불가능하다 s[1] = 'a' 이런 식으로 변경할 수 없음
- 문자열 연산
  - `==`  : 문자열 비교 
  -  `+`   : 문자열 붙이기





## 2) 숫자 _정수 int

- 소수부가 없는 숫자
- 일반적으로는 int 를 사용해서 변수를 선언해주면 된다
- 부호가 있는 정수  : + - 정수 (ex. unit8의 범위 0 ~ 255(2^8-1)) 
- 부호가 없는 정수 :  양의 정수 또는 0  (ex. int8의 범위 -128 ~ 127 (-2^7 ~ 2^7-1) )





## 3) 숫자 _ 실수 (부동 소수점 수) float64

- 부동 소수점 수 (floating point number) : 소수부가 포함된 숫자
- 일반적으로 float64를 사용한다

- 부동 소수점 수는 표현하기가 어려운 경우가 있다 (부정확함)
  - 1.01 - 0.99 의 결과는 0.020000000000000018 이다. 0.02와 매우 근접하지만 정확하게 일치하지는 않는다
  - 따라서 연산한 값을 == 로 직접 비교할 수 없다!!
- 일정한 크기 32비트 64비트로 이루어져있는데, 크기가 클수록 표현할 수 있는 숫자의 자리수가 커지기 때문에 정확도가 높아진다





## 더보기

- [변수 선언하기](#)