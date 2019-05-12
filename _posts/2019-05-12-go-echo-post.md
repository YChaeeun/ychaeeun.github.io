---
title: golang echo 기초 -2 (POST)
date: 2019-05-12
tags:
 - echo
categories:
 - golang
---



> [guide](<https://echo.labstack.com/guide>)
>
> Echo is a high performance, extensible, minimalist web framework for Go (Golang)



## Form `application/x-www-form-urlencoded`



```go
package main

import (
	"net/http"
	"github.com/labstack/echo"
)

func main() {
    
    e.GET("/" func(c echo.Context) error {        return c.String(http.StatusOK, "Hello World!")
     })  
    
    e.POST("/save", save)
    
    e.Logger.Fatal(e.Start(":1324")) // localhost:1324
   
}

func save(c echo.Context) error {
    
    name  := c.FormValue("name") 
    email := c.FormValue("email")
    
    return c.String(http.StatusOK, "name:"+name+", email:"+email)
}
```



```go
$ curl -F "name=Joe Smith" -F "email=joe@labstack.com" http://localhost:1324/save

// => name:Joe Smith, email:joe@labstack.com
```



POST로 넘긴 값은 화면에 출력되지 않고 ` {"message":"Method Not Allowed"}` 라는 값을 반환한다. 값이 POST로 잘 넘어갔는지 확인하고 싶다면 Postman을 사용해서 값을 직접 확인 할 수 있다.



![postman]({{site.url}}{{site.baseurl}}/assets/images/postman-2.png)



[Postman 사용하기](#)





## Form `multipart/from-data`



