---
title: golang 분기문 switch
date: 2019-06-02
categories:
 - go

---





## switch()



- 형식

  ```go
  switch 변수 {
  case 값1 :
      // 변수 == 값1 일 때, 실행
  case 값2 :
      // 변수 == 값2 일 때, 실행
  default :
      // 위 모든 조건에 만족하지 않을 때 실행
  }
  ```

  - **숫자** 뿐만 아니라 **문자열**, **조건식** 또한 값으로 사용할 수 있다



### break _ 실행 중지

- break 사용 가능

  ```go
  s := "Hello"
  i := 2
  
  switch i{
  case 1 :
      fmt.Println(1)
  case 2 :
      if s == "Hello"{
          fmt.Println(s,2)  // Hello 2
          break
      }
      fmt.Println(2)
  }
  ```




### fallthrough _ 그 다음 case문도 실행

- fallthrough 사용하기

  - 특정 case 를 실행 한 후, **바로 그 다음 case 문**도 실행하고 싶을 때 사용
  - 마지막 case 문에는 사용할 수 없음

  ```go
  i := 2
  
  switch i {
  case 3 :
      fmt.Println("3")
      fallthrough
  case 2:
      fmt.Println("2")  // 실행 2
      fallthrough
  case 1 :
      fmt.Println("1")  // 실행 1 끝
  default :
      fmt.Println("0")
      // fallthrough 사용 불가능
  }
  ```

  - case 2 조건에 부합해서 fmt.Println("2") 실행
  - fallthrough를 만나서 바로 그 다음 조건문도 실행
  - case 1 에는 fallthrough가 없으니 실행 종료



### 조건을 주는 여러가지 방법

- 여러 조건 함께 처리하기

  - , (콤마) 로 값을 구분해주면 됨

    ```go
    i := 3
    switch i {
    case 1,3,5 :
        fmt.Println("홀수")
    case 2,4,6 :
        fmt.Println("짝수")
    }
    ```

    

- 조건식으로 분기하기

  - swtich 키워드 다음에 판별할 변수를 지정하지 않고 case에서 조건식으로만 문장을 실행 할 수도 있음!!

  ```go
  i := 7
  
  switch {
  case i >= 5 && i<10 :
      fmt.Println("5이상, 10 미만")
  
  case i >= 0 && i < 5 :
      fmt.Println("0이상, 5 미만")
  
  }
  ```



- 또한 switch 분기문안에서 함수를 실행한 뒤, 그 결과값으로 분기할 수도 있음

  - 이때 함수를 실행한 뒤에 ; (세미콜론)을 붙여줌
  - case 에서는 값으로 분기할 수 없고 **조건식**만 사용 가능

  ```go
  import (
      "fmt"
      "time"
  )
  
  func main() {
      fmt.Println("When's Saturday?")
      today := time.Now().Weekday()
      switch time.Saturday {
      case today + 0:
          fmt.Println("Today.")
      case today + 1:
          fmt.Println("Tomorrow.")
      case today + 2:
          fmt.Println("In two days.")
      default:
          fmt.Println("Too far away.")
      }
  }
  ```

  - 이때 case 5 : 이런식으로 값을 직접 주면 에러남

  