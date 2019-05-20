---
title: golang 변수 & 상수 선언하기 variables constant
date: 2019-05-20
categories:
 - go
---



> 참고 :  [golang 기본 자료형](#)



## 변수 variable


- 변수 한 개 선언하기
	```go
// 방법 1
var num1 int = 1
	
	// 방법 2
	var num2 = 1
	
	// 방법 3 : 짧은 선언
	num3 := 1
	```
	- 타입(자료형)이 명시 되지 않은 경우, 초기화된 값에 따라 결정된다


- 변수 여러 개 선언하기

	```go
	// 방법 1
	var x, y int = 10, 20

	// 방법 2
	var (
		a,b  int = 3,2
    	c,d      = "Hi", 10
	)

	// 방법 3
	a, b, c := 1, 2.3, "Hello"
	```





## 상수 const

- 상수 한 개 선언하기

  ```go
  const age1 int = 10
  const age2 = 20
  const age3 // 에러
  ```
  - 상수는 선언할 때 초기값을 무조건 설정해줘야 한다!

  

- 상수 여러 개 선언하기

	```go
	const (
		a = 0
    	b = 1
    	c = 2
    	d = 3
	)
	```

	- iota 를 사용해서 순서대로 값을 넣을 수 있음 (0부터)
	```go
	const (
		a = iota
    	b
   	c
    	d
	)
	```



## 변수 크기 구하기 Sizeof

```go
package main

import "fmt"
import "unsafe" // Sizeof 함수를 사용하기 unsafe 패키지 사용

func main() {
	var num1 int8  = 1
	var num2 int16 = 1
	var num3 int32 = 1
	var num4 int64 = 1

	fmt.Println(unsafe.Sizeof(num1)) // 1
	fmt.Println(unsafe.Sizeof(num2)) // 2
	fmt.Println(unsafe.Sizeof(num3)) // 4
	fmt.Println(unsafe.Sizeof(num4)) // 8
}
```





