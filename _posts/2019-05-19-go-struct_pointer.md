---
title: golang 구조체 & 포인터
date: 2019-05-19
published : false
categories:
 - go


---







## 구조체



```go
package main

import "fmt"

type Vertex struct {
    X int
    Y int
}

func main() {
    v := Vertex{1,2}
    v.X = 4
    fmt.Println(v.X)
    fmt.Println(Vertex{1, 2})
}
```

- 구조체 필드의 데이터는 (.) 으로 접근



## 포인터 Pointers



- 포인터가 있지만, 포인터 연산은 불가능

- 구조체 변수는 구조체 포인터를 이용해서 접근 할 수 있다

  ```go
  package main
  
  import "fmt"
  
  type Vertex struct {
      X int
      Y int
  }
  
  func main() {
      p := Vertex{1, 2}
      q := &p
      q.X = 1e9
      fmt.Println(p)
  }
  ```

  



## 구조체 리터럴 Struct Literals



- 필드와 값을 나열해서 구조체를 새로 할당하는 방법

- `{name : value}`구문을 통해 할당할 수 있다 (필드의 순서와는 무관)

  ```go
  package main
  
  import "fmt"
  
  type Vertex struct {
      X, Y int
  }
  
  var (
      p = Vertex{1, 2}  // has type Vertex
      q = &Vertex{1, 2} // has type *Vertex
      r = Vertex{X: 5, Y:6} // X:5 Y:6
    
      s = Vertex{X: 1} // Y:0 is implicit
      t = Vertex{}      // X:0 and Y:0
  )
  
  func main() {
      fmt.Println(p, q, r, s, t)
  }
  ```

  





## new(T)

- 모든 필드에 0(zero value) 가 할당된 T 타입의 포인터를 반환

  ```go
  var t*T = new(T)
  ```

  ```go
  t := new(T)
  ```

  - 변수 t는 T에서 반환된 포인터를 가짐

```go
package main

import "fmt"

type Vertex struct {
    X, Y int
}

func main() {
    v := new(Vertex)
    fmt.Println(v)
    v.X, v.Y = 11, 9
    fmt.Println(v)
}

```

