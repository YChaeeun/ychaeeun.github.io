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



