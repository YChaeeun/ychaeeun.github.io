---
title: python 함수 return 반환값 특징  
date: 2019-05-17
categories:
 - python
---





## return 반환값은 언제나 한 개!

- 반환값은 언제나 한 개를 반환한다

- 리스트 (주소값) 한 개 / 딕셔너리 (주소값) 한 개 / 튜플 (주소값) 한 개 

  ```python
  def operation(a,b) :
      r1 = a+b
      r2 = a-b
      r3 = a*b
      r4 = a/b
      
      list1 = [r1,r2,r3,r4]
      return list1
  ```

  ```python
  result = operation(1,5)
  print(result) # [6,-4,5,0.2]
  ```

  

- return 옆에 여러 개의 값을 적으면 **튜플 값 한 개**로 되돌려 준다 (튜플의 주소값 **한 개**가 반환된다)

  ```python
  def mul_10(a,b,c,d) :
      return a*10, b*10, c*10, d*10
  ```

  ```python
  result1 = mul_10(1,2,3,4)
  print(result1)  # (10,20,30,40)
  
  r1, r2, r3, r4 = mul_10(1,2,3,4)
  print(r1,r2,r3,r4) # 10, 20, 30, 40
  ```



## 되돌아감

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

    

## return을 만나면 바로 종료

- return 구문이 여러개 있더라도, return을 만나면 함수가 완료되었다고 판단해서 함수를 호출한 쪽으로 되돌아간다

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

