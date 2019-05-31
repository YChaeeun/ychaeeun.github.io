---
title: algo python 알아둘 것 정리 (계속 업데이트)
date: 9999-12-31
tags:
 - python
categories:
 - algorithm
toc: true
---



## 0) 기타

- /   :   나눗셈 연산

  % : 나머지를 구하는 연산

  //  :  몫을 구하는 연산

  

- enumerate()

  + for 문을 사용할 때, 인덱스와 값을 동시에 사용할 수 있게 해줌!

  ```python
  for i, j in enumerate(['a', 'b', 'c']):
      print(i, j)
      
      # 0 a
      # 1 b
      # 2 c
  ```



- sum( list )

  + 함수 안에 있는 list 요소들을 다 더해 줌 

  

- ord("Z")   < -- >   chr(90)




- 문자열을 리스트에 요소 하나하나 넣을 때

  ```python
  list1 = [int(i) for i in s]
  list2 = list(map(int, list1))
  ```

  

+ 빈 리스트를 선언할 때는 list1 = list() 보다는 **list1 = []** 가 좋다!  [(참고)](<https://stackoverflow.com/questions/2972212/creating-an-empty-list-in-python>)



- list.remove(x) : 리스트에서 x 를 제거함




## 1) 문자열

- 문자열 함수는 해당 문자열을 직접 수정하는 것이 아니라 **COPY**한 다른 문자열을 만들어내는 것!
- 문자열은 immutable한 자료형으로, s[3] = 'k' 같은 작업을 할 수 **없다**.

<hr/>

- s.lower()  / s.upper()
- s.count('x')
  + 문자열 s에 'x'가 몇 개 있는 지, 갯수를 리턴함
- s.index('x')  /  s.find('x')
  + 문자열 s에 'x' 가 어디에 있는지 그 인덱스 값을 반환함
  + 만약 'x'가 없을 경우, index()는 에러를 반환  /  find()는 -1을 반환한다
  + 리스트에도 사용가능 (흠...)
- **" ".join(string)**
  + 리스트 값들을 합쳐서 문자열로 만들어 준다
  + "".join(['a', 'b', 'c'])  -> "abc"
  + " &".join(['a', 'b', 'c'])  -> "a&b&c"
- s.isupper()  /  s.islower()  /  s.isalnum()  /  s.isdigit()  /  s.decimal()  /  s.isalpha()
- s.strip()  /  s.lstrip()  /  s.rstrip()
  + 문자열 공백 제거





## 2) 슬라이싱 Slicing

+ 슬라이싱은 새로운 배열을 반환한다!





## 3) lambda





## 4) 정렬 sort()  /  sorted()

- string.sort(**reverse**=True)  /  sorted(string, reverse=True)
  - 내림차순으로 정렬
  - reverse**d**  아니야!   **"reverse"**
- 차이점 [(참고)](<https://stackoverflow.com/questions/22442378/what-is-the-difference-between-sortedlist-vs-list-sort>)

<table>
    <tr>
    	<th>list.sort()  /  string.sort()</th>
        <th>sorted(list)  /  sorted(string)</th>
    </tr>
    <tr>
        <td> 원본을 <strong>직접</strong> 정렬
        </td>
        <td> 원본에 영향을 끼치지 않음 <br/>
        </td>
    </tr>
    <tr>
        <td>None을 반환함</td>
        <td>정렬한 <strong>새로운</strong> 문자열 혹은 list를 반환함</td>
    </tr>
</table>


## 5) dict 관련 함수

- setdefault(key, default_value)
  - 만약 dictionary에 key 값이 **없다면** key : default_value 를 추가한다
  - key 값이 있다면 default_value 무시



## for - else


- for 문안에 if와 break가 있을 때 주로 사용한다 (편리!)

- for문 안에서 **break를 만나지 않았고, for문이 종료되었을 경우** else 구문이 **한 번** 실행된다

- 만약 break를 만났다면 else는 실행되지 않고 for 문은 종료

  ```python
  for i in range(0,5):
      if i>10:
          print(i)
          break
  else :
      print ("else")
  ```

  - if 조건을 만족하지 않으므로 break를 만나지 않음
  - else 구문의 print("else") 가 실행됨



- 예시  [출처](<http://book.pythontips.com/en/latest/for_-_else.html>)

  ```python
  for n in range(2, 10):
      for x in range(2, n):
          if n % x == 0:
              print( n, 'equals', x, '*', n/x)
              break
      else:
          # loop fell through without finding a factor
          print(n, 'is a prime number')
  ```

  - 2 is a prime number

    3 is a prime number

    4 equals 2 * 2.0

    5 is a prime number

    6 equals 2 * 3.0

    7 is a prime number

    8 equals 2 * 4.0

    9 equals 3 * 3.0