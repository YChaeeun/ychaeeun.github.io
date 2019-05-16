---
title: python 함수란?
date: 2019-05-17
categories:
 - python
---





## 함수 function

- 소프트웨어를 개발할 때, 어떤 문제를 해결할 때 **하나의 기능을 따로 떼어내서 구현**할 수 있게 해준다

- 반복되는 기능을 함수로 작성하면, 불필요하게 코드를 작성할 필요가 없어진다! (유지보수에 용이함)

  ```python
  def 함수이름 (매개변수1, 매개변수 2....) :
      수행할 기능
      return 반환값
  ```

  ```python
  def sumAll (num1, num2) :
      result = num1 + num2
      return result
  ```

  - 함수 sumAll은 num1과 num2를 인자로 받아서, 더한 결과를 반환하는 함수이다

  - **매개변수 parameter**는 없을 수도 있고, 여러 개가 있을 수도 있다 -> [심화](#)

  - **return**은 **하나**의 값만 반환한다 

    

## 함수가 작동하는 방식

### 1) call

- 함수는 작성된 뒤 **호출 call**해야 사용할 수 있다 

- 호출하기 전에 먼저 함수를 정의해야 한다 (안그러면 에러)

  ```python
  def getAverage(kor, math, eng) :
      avg = float((kor+math+eng)/3)
      return avg
      
  def printTotal(kor, math, eng) :
      print(kor+math+eng)
      
  avg = getAverage(97,86,78)
  print(avg)
  # print(getAverage(97,86,78)) 해도 됨
  ```

  - printTotal은 호출되지 않았기 때문에 사용하지 않는다
  - getAverage()의 반환값을 avg라는 변수에 담아서 출력



### 2) pass

- 함수를 정의했지만 아직 내용을 작성하고 싶지 않을 때는 **pass**를 적으면 에러가 발생하지 않는다

```python
def getFunction(a) :
    pass

getFunction(a)  # None
```



### 3) return

- return을 만나면 바로 함수를 빠져나와 함수를 호출한 쪽으로 **되돌아간다**

  ```python
  def operation(a,b) :
      return a+b
  	return a*b
  	return a-b
  
  operation(5,2)
  # 처음 만난 return a+b의 결과만 반환됨
  ```

  - return을 여러 개 적는다고 여러 개의 값을 반환할 수는 없다
  
  - 여러 개의 값을 반환하고 싶다면 [리스트나 딕셔너리, 튜플에 넣어서 반환해야 한다]()
  
    


-  return 구문이 여러개 있더라도, return을 만나면 함수가 완료되었다고 판단해서 함수를 호출한 쪽으로 되돌아간다

  ```python
  def isNumEven(a) :
      if a % 2 == 0 :
          print(f"{a}는 짝수다!") # (i)
          return
   	else :
          print(f"{a}는 홀수다!") # (ii)
          
  isNumEven(12)
  # 이때 (i)만 출력되고 return
  # (ii)는 실행되지 않는다
  ```
  
  

## 전체 흐름 이해하기



![func]({{site.url}}{{site.baseurl}}/assets/images/func.png)



## 더 보기

- [파이썬에만 있는 함수의 특징 - 매개변수](#)
- [함수의 결과값은 언제나 하나?](#)

