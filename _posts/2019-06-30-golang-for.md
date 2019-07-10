---
title: golang 반복문 for
date: 2019-06-30
categories:
 - go

---





## for 반복문

- c/c++ 이랑은 달리 반복문에 for 만 있다

- 형식

  ```go
  for 초깃값;조건식;변화식 {
      // () 를 사용하지 않는다
  }
  ```

  ```go
  for 조건 {
      //변화식
  }
  ```

  ```go
  for {
      // 무한루프
  }
  ```
  
- 예시

  ```go
  package main
  
  import "fmt"
  
  func main() {
  	sum := 0
  	for i := 0; i < 10; i++ {
  		sum += 10 * i
  		fmt.Println(sum)
  	}
  }
  ```

  

  

### range() 

  - 슬라이스나 맵을 순회할 수 있음 iterate

  ``` go
  package main
  
  import "fmt"
  
  var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
  
  func main() {
      for i, v := range pow {
          fmt.Printf("2**%d = %d\n", i, v)
      }
  }
  
  ```

  - 원하지 않는 값은 _ 을 적으면 사용하지 않을 수 있음

  ``` go
  for _, value := range pow {
      fmt.Printf("%d\n", value)
  }
  ```





## break & continue


- break : 반복문 중단

  ```go
  package main
  
  import "fmt"
  
  func main() {
  	i := 0
      for {
  		if i > 9 {
  			break
  		}
  		i++
  		fmt.Printf("%d ", i)
  	}
  	fmt.Println("end")
  }
  // 1 2 3 4 5 6 7 8 9 10 end
  ```

  

- continue : 아래 명령어를 무시하고 반복문의 처음부터 다시 시작

  ```go
  package main
  
  import "fmt"
  
  func main() {
  
  	for i := 0; i < 10; i++ {
  		if i%2 == 0 {
  			continue
  		}
  		fmt.Printf("%d ", i)
  	}
  	fmt.Println("end")
  }
  // 1 3 5 7 9 end
  ```

  



  - Loop 라벨을 붙여서 사용할 수 있고, 라벨의 이름 짓기 규칙은 변수 이름 짓기 규칙과 동일

    ```go
    func main() {
    Loop:
    	for i := 1; i < 10; i++ {
    		for j := 1; j < 10; j++ {
    			if i >= 5 {
    				break Loop
    			}
    			fmt.Println(i, j)
    		}
    	}
    	fmt.Println("END")
    }
    ```

    - 라벨과 for 문 사이에 어떠한 코드도 있어서는 안됨
    - break Loop을 만나면 더이상 for문을 실행하지 않고 빠져나와 다음 줄인 fmt.Println("END") 를 실행한다

- continue

  - break와 동일하게 Loop 라벨을 붙여서 사용 가능
  - continue 아래 명령들을 무시하고 다시 for 문의 처음 시작 부분으로 간다
  
  

### 레이블 label 붙이기

- break 나 continue를 사용할 때 원하는 지점으로 바로 이동할 수 있도록 레이블을 달아줄 수 있다

- 특히 중첩된 for 반복문에서 완전히 빠져나올 때 유용하다

  ```go
  package main
  
  import "fmt"
  
  func main() {
      
  Loop1 :
  	for i := 0; i < 10; i++ {
          Loop2 :
  		for j := 0; j < 5; j++ {
  			if j%2 == 0 {
  				fmt.Println(i, j)
  				continue Loop1
  			}
  		}
  	}
  	fmt.Println("end")
  }
  ```

  - 중첩된 j %2 == 0 조건에 걸리면 바로 루프를 빠져나와서 Loop 레이블로 이동, 맨 처음 for 문부터 다시 진행 (그래서 이 경우에는 j가 0 밖에 안나옴 0 만나자 마자 i++로 가니까)
  - 만약 Loop 레이블이 없었다면 continue는 j 값을 증가시키는 for 루프를 다시 실행 ( j는 0 2 4 가 나옴 )

- 레이블명 짓기는 변수명 지을 때 규칙과 동일하게 지으면 됨

- 레이블과 for 반복문 조건 사이에 다른 코드가 들어가면 안돼

  ```go
  Loop:
  	fmt.Println(a)
  	for i:=1;i<10;i++{    
  	}
  ```

  - 이런 식으로 레이블과 for 반복문 사이에 다른 코드들이 들어가면 안돼!



## 변수 여러 개 사용하기

- go 변화식에서 여러 변수를 처리하려면 **병렬할당**을 사용하면 된다

  ```go
  for i,j:=0,0; i<10 ; i,j=i+1,j+2{
      fmt.Println(i,j)
  }
  ```
	- 병렬할당을 사용하지 않고 그냥 i++, j += 2 이런 식으로 옆으로 나열하기만 하면 에러발생!

