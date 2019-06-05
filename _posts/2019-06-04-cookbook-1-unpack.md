---
title: python cookbook -1 (Unpack a Sequence, star expression)
date: 2019-06-04
categories:
 - python
 - cookbook
---





## 1.1 Unpacking a Sequence



### into Separate Variables

- 간단한 대입 연산 (=) 으로 튜플이나 리스트 등등의 Sequence의 값들을 변수에 각각 넣을 수 있다

  ```python
  a = (1,2,("hello!", 3)
  x,y,z = a
       
  print(x,y) #1,2
  print(z)  # (hello! 3)
  ```

  ```python
  listA= ['python', (2019, 12, 31)]
  subject, year, month, day = listA
  
  print(year, month, day) # 2019 12 31
  ```

  - 넘겨 받는 변수의 개수가 맞지 않으면 에러 발생



- 문자열도 이렇게 받을 수 있다!!

  ```python
  greeting = "hello"
  a,b,c,d,e = greeting
  
  print(a,b,c,d,e)  # h e l l o
  ```



- 특정 값이 필요 없으면 변수명을 _ 로 처리해주면 된다

  ```python
  name = "chaen"
  x,y,_,_,z = name
  print(x,y,z)   # c h n
  ```





### from Iterables of Arbitrary Length

- 받을 값의 길이를 모른다면??? 변수 개수를 하나하나 정해줄 수 없으니 --> **Star Expression** 사용하기

- **Star Expression** `*`  `**`

  >  use `*` operator to unpack the arguments out of a list or tuple  [출처](<https://docs.python.org/3/tutorial/controlflow.html#unpacking-argument-lists>)

  - Unpack을 할 때 사용할 수 있다!! (**리스트 반환**)
  - 함수의 가변 매개변수를 공부할 때 봤던 개념인 듯

  ```python
  def drop_first_last(grades) :
      first, *middle, last = grades
      return print(middle)
  
  grades = [10, 20, 30, 40]
  drop_first_last(grades)  # [20 30]
  # 중간값인 20, 30 만 출력된다 (미칭!)
  ```

- 한 줄에 한 번(?)만 사용할 수 있다 a, *b, *c = (1,2,3) 하면 에러남

- starred expression 위치에 따른 변화!!

  ```python
  a, b, *c = [1,2,3,4,5]
  print(a,b,c)  # 1 2 [3 4 5]
  
  a, *b, c = [1,2,3,4,5]
  print(a,c,c)  # 1 [2 3 4] 5
  
  *a, b, c = [1,2,3,4,5]
  print(a,b,c)  # [1 2 3] 4 5
  ```

  - 만약 받을 변수의 개수가 더 많으면 값은 우선 일반 변수에 할당되고 **starred 는 그냥 빈 리스트를 반환**

    ```python
  a, b, *c = (1 2)
    print(a,b,c)  # 1 2 []
    
    a, *b, c = (1 2)
    print(a,b,c)  # 1 [] 2
    
    *a, b, c = (1 2) 
    print(a,b,c)  # [] 1 2
    ```
  
  
  



### starred expression을 사용하면 좋을 때!

- A와 B의 특성을 가진 값들이 서로 섞여 있는데 서로 다른 작업을 해줘야 할 때! -->> A와 B의 **공통 부분을 추출**해서 값들을 크게 둘로 **분류**한 뒤에 원하는 작업을 해줄 수 있음

  ```python
  student = [
   ('math', 100, 95),
   ('eng', 'nice', 'great'),
   ('math', 42, 63),
   ('eng', 'bad', 'not good')
  ]
  
  def do_math(*args) :
      print(sum(args)//2)
  def do_eng(s1, s2) :
      print(s1 + s2)
      
  for tag, *args in student :
      if tag == 'math' : do_math(*args)
      elif tag == 'eng' : do_eng(*args)
  ```

  - student 값들의 공통부분인 'math'와 'eng'를 기준으로 분류한 뒤 다르게 처리

- 문자열 처리할 때도 유용함! split()와 함께

  ```python
  line = 'ychae:%:Unprevileged User:/ychae/python:/src/bin'
  
  userName, *field, homdir, sh = line.split(':')
  print(userName, field, homdir, sh)
  # ychae ['%', 'Unprevileged User'] /ychae/python /src/bin
  ```

  