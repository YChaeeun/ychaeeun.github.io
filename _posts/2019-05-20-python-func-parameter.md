---
title: python 함수의 매개변수(parameter) 특징 - 기본값 & 가변형 매개변수
date: 2019-05-20
categories:
 - python
---




> 파이썬의 독특한  매개변수 parameter의 특징!
> <기본값 설정하기 & 가변형 매개변수>



## 함수의 매개변수 parameter

- 함수 내부에서 만든 코드에서 필요한 값을 전달해야 할 때, 이를 매개변수로 받을 수 있다
- 함수를 호출(call) 할 때 매개변수를 전달할 수 있고, 전달된 값은 함수에서 정의된 변수에 담긴다

- parameter는 1) 없을 수도 있고, 2) 여러 개가 있을 수도 있으며,  3) 크기나 형태가 넘겨줄 때 결정될 수도 있다

  ```python
  def funcParameter(a, b) :
      print('parameter:',a,b)
      
  funcParmeter(10,20)  # parameter: 10 20
  funcParameter('Hello', 'Hi') # parameter: Hello Hi
  ```

  - 호출할 때 정의된 매개변수의 개수만큼 값을 전달해야 한다 (기본값이 정의되어 있지 않다면)







## 1) 기본 값

- 기본값을 설정해놓으면, 함수 호출 시 값을 전달하지 않았을 경우, 기본값이 매개변수에 저장된다

  ```python
  def fun1(a=1, b=2, c=3) :
      print(a,b,c)
      
  fun1(6,2,8)   # 6 2 8
  fun1(2,4)	  # 2 4 3
  ```

  - 매개변수의 개수에 맞게 전달된다면 전달된 값이 변수에 저장된다
  - 개수에 맞지 않게 값을 전달 -> c에 설정되어 있던 기본값 3이 변수에 저장된다



- 모든 변수에 기본값을 주지 않을 거라면, **기본값이 설정되지 않은 매개변수가 앞쪽에 와야 한다**

  ```python
  def fun1(a=2, b, c)    # 에러 _ 기본값이 설정되지 않은 b와 c가 앞쪽에 와야 함
  def fun1(a, b=1, c=5)  # 바르게 작성 _ 1,1,5
  ```



### - 매개변수의 이름으로 값을 지정하고 호출하기

- 함수를 **호출 할 때**, 값을 순서대로 적지 않고 매개변수의 이름을 적고 값을 전달 할 수도 있다

- 기본값이 설정되지 않은 변수가 앞쪽에 와야 하고, 한 변수에 중복해서 값을 넣을 수 없다

  ```python
  fun1(b=3, a=4, 1)   # 에러 _ 기본값이 정의되지 않은 변수가 앞에 와야 함
  fun1(a=1, 3, c=5)   # 에러 _ 기본값이 정의되지 않은 변수가 앞에 와야 함
  ```
  ```python
  fun1(2, b=1, a=3)
  # 에러 _ a에 중복된 값 2, 3이 들어갔고, c에 해당하는 값이 없음
  ```
  ```python
  fun1(10, c=2, b=7)   # 10, 7, 2
  fun1(a2=1, a1=4)     # 4,1,3 _ c는 기본값이 들어감
  ```



## 2) 가변형 매개변수

- 함수 호출 시 넘겨주는 값에 따라 형태가 결정되는 매개변수
- 값으로 몇 개를 넘겨줘야 할 지 모를 때 사용한다



### - 리스트 & 딕셔너리

- 파이썬은 모든 변수들이 객체라서 리스트와 딕셔너리 등등을 그대로 넘겨줘도 된다

- 리스트

  ```python
  def sumAllelements(list1) :
      result = 0
    	for num in list1 :
          result += num
      return result
  
  exampleList = [1,2,3,4,5]
  print(sumAllelements(exampleList))  # 15 
  ```
  

- 딕셔너리

  ```python
  def dictionary(dic) :
      for key, value in dic.items() :
          print(f"{key} : {value}")
          
  exampledic = {'a' : 10, 'b' : 20}
  dictionary(exampledic)
  ```

  

### - 리스트 포인터*

- 리스트의 주소값을 넘겨준다

- 리스트를 직접 넘기는 것과의 차이 : 개발자가 직접 리스트를 입력해서 넣는 것이 아니라 컴퓨터가 실행하면서 자기가 리스트를 만들어서 넣는 다는 점!

  ```python
  def sumAllpointer(*list1) :
      return sum(list1)
  
  # 방법 1
  example = [1,2,3,4,5]
  sumAllpointer(*exmple)
  
  # 방법 2
  sumAllpointer(1,2,3,4,5)
  ```



### - 딕셔너리 포인터**

- 리스트 포인터와 달리 __**__ 두 개!

  ```python
  # 방법 1
  def dicPointer1(**dic) :
      for key, value in dic.items() :
          print(f"{key} : {value}")
          
  dic1 = {'a' :1, 'b':2, 'c':3}
  dicPointer1(**dic1)
  ```

  ```python
  # 방법 2
  def dicPointer2(**dic) :
      for key, value in dic :
          print(f"{key} : {value}")
  
  dicPointer2(a1=10)
  dicPointer2(b1 = 10, b2 =20, b3 = 49)
  ```

  

## 3) 가변형 매개변수 작성 순서 및 규칙

### 순서!!

- **일반변수, 일반변수 .... 리스트형 매개 변수, 딕셔너리형 매개 변수**



### 규칙

- 섞여 있을 경우, **일반 매개 변수를 먼저** 작성

- 리스트 포인터 매개변수가 먼저, 그 다음에 딕셔너리 포인터 매개변수 

  ```python
  def fun1(*a1, **a2, a3, a4) :
      print(a1, a2, a3, a4, sep="\n")  # 에러 _ 일반 변수를 앞에 써야 해
  ```

  ```python
  def fun2(**a3, *a4) :
      print(a3, a4, sep="\n")  		# 에러 _ 리스트형 매개변수가 먼저!!
  ```

  ```python
  def fun3(a1, a2, *a3, **a4) :
      print(a1, a2, a3, a4, sep="\n")  # 바른 순서!
  ```

  

- 같은 종류의 **포인터** 가변형 매개변수를 여러 개 사용할 수 없음! ( 리스트포인터 / 딕셔너리포인터는 **한 번씩만** 사용 가능 )

  ```python
  def fun4(*a, *b) :
      print(a,b)   # 에러 _ 같은 종류의 포인터 가변형 매개변수를 사용할 수 없음
  ```

  ```python
  def fun5(a, b, *c) :
      print(a,b)
  
  list1 = [1,2,3]
  list2 = [4,5,6]
  list3 = [7,8,9]
  
  fun5(list1, list2, *list3)		
  
  # 바른 작성 _ 리스트 포인터 한 번 사용
  ```

  




## 더 보기

- [함수란?](#)
- [함수의 결과값은 언제나 하나?](#)

