---
title: golang echo 기초 -1 (설치 & GET)
date: 2019-05-12
tags:
 - echo
categories:
 - golang
---



## echo 웹 프레임워크



> [guide](<https://echo.labstack.com/guide>)
>
> Echo is a high performance, extensible, minimalist web framework for Go (Golang)



echo는 go(golang)의 웹 프레임워크다. (ex. python flask) go 언어 자체가 흥한지 얼마 되지 않아서, 아직 풀이 엄청 크지는 않지만 최근에  잘 쓰이고 있다고 한다.



## echo 설치하기 (window)



go get 방법을 사용했다. VS Code 아래 터미널 창을 열고 아래와 같이 입력한다.

```python
$ go get -u github.com/labstack/echo/...
```



## Hello world! 출력하기



```go
package main

import (
	"net/http"
    
    "github.com/labstack/echo"
)

func main() {
    
    e := echo.New()
    e.GET("/", func(c echo.Context) error {
        return c.String(http.StatusOK, "Hello World!")
    })
    
    e.Logger.Fatal(e.Start(":1323")) // localhost:1323
    
}
```



주소창에 http://localhost:1323 을 입력하면 Hello world가 잘 출력된다.





## 값 받아와서 화면에 출력하기 (GET)



```go
package main

import (
	"net/http"
    
    "github.com/labstack/echo"
)

func main() {
    
    e := echo.New()
    // 첫 화면
    e.GET("/", func(c echo.Context) error {
        return c.String(http.StatusOK, "Hello World!")
    })
    
    e.GET("/users/:id", getUser)
    
    e.Logger.Fatal(e.Start(":1323")) // localhost:1323
}

func getUser(c echo.Context) error {
    
    id := c.Param("id")
    return c.String(http.StatusOK, id)
}
```



위 코드를 입력한 뒤, 주소창에 http://localhost:1323/users/string-you-want-to-print 를 입력하면 화면에 string-you-want-to-print 가 출력된다. 출력하고 싶은 값을 적어주면, id 값으로 해당 값이 넘어가서 화면에 출력된다.



## Qeury Parameters (GET)



값 받아와서 화면에 출력하기 2

**/show?team=Avenger&member=Spiderman**



```go
package main

import (
	"net/http"
    
    "github.com/labstack/echo"
)

func main() {
    
    e := echo.New()
    // 첫 화면
    e.GET("/", func(c echo.Context) error {
        return c.String(http.StatusOK, "Hello World!")
    })
    
    e.GET("/show", show)
    
    e.Logger.Fatal(e.Start(":1323")) // localhost:1323
}

func show(c echo.Context) error {
    
    team := c.QueryParam("team")
    member := c.QueryParam("member")
    return c.String(http.StatusOK, "team:"+team+", member:"+member)
}
```



주소창에 http://localhost:1323/show?team=Avenger&member=Spiderman 를 입력하면, 화면에 team: Avenger, member: Spiderman 이 출력된다.




