---
title: python cookbook -4 (multidict - defaultdict vs setdefault)
date: 2019-06-06
categories:
 - python
 - cookbook
---



## multidict

- mapping keys to multiple values in a dictionary

  - key값 하나에 여러개의 value값을 가지는 딕셔너리

  - multiple values를 담을 리스트나 집합 자료형을 선언하면 됨!

    ```python
  d = {
        'a' : [1,2,3],  # 리스트 list
        'b' : [4,5,6]
    }
    e = {
        'a' : {1,2,3},  # 집합 set
        'b' : {4,5,6}
    }
    ```
  
    - 리스트 : 순서가 있고, 중복을 허용
    - 집합 : 순서가 없고, 중복을 허용하지 않음
  



### 1) from collection import defaultdict

- defaultdict
  - automatically initializes the first value
  
  - dictionary에 key가 없을 경우에 자동으로 list나 set으로 초기화를 해준다 
  
    - if key not in d : d[key] = [] 같이 처음 key가 딕셔너리에 없을 때 초기화하는 코드를 작성할 필요 없음
  
    ```python
    from collections import defaultdict
    
    d = defaultdict(list) # value들을 리스트에 담을 수 있음
    d['a'].append(1)
    d['a'].append(2)
    d['b'].append(3)
    d['c'].append(4)
    
    print(d)
    # defaultdict(<class 'list'>, {'a': [1, 2], 'b': [3], 'c': [4]}) 
    print(dict(d))
    # {'a': [1, 2], 'b': [3], 'c': [4]}
    ```
  
    ```python
    from collections import defaultdict
    
    e = defaultdict(set)  # value들을 집합에 담음
    
    e['a'].add(1)
    e['a'].add(2)
    e['b'].add(3)
    e['c'].add(4)
    print(e)
    # defaultdict(<class 'set'>, {'a': {1, 2}, 'b': {3}, 'c': {4}})
    ```
  
    - **모든 key값에 대해** value를 담을 공간을 초기화함 (새로 key가 들어오면 -> 이 value를 담을 []나 {}가 생성되어 있음)
    - 깔끔하게 dict 값만 출력하고 싶으면 dict() 형 변환을 해줘야 해



### 2) dict.setdefault

- 굳이 전체key에 대해 multi values를 가질 필요가 없을 때 사용함

- 하지만 매번 호출할 때마다 초깃값의 새로운 인스턴스를 생성하기 때문에 unnatural

  - 호출할 때 마다 매번 element마다 리스트나 집합 공간을 새롭게 생성해야 함

  - instance : OOP(객체지향프로그래밍)에서 객체가 선언된 후, 실제로 메모리에 할당되어 사용되는 구체적인 실체를 의미

  ```python
  d = {}  # 빈 딕셔너리 선언
  
  d.setdefault('a', []).append(1)
  d.setdefault('a', []).append(2)
  d.setdefault('b', []).append(3)
  d.setdefault('c', []).append(4)
  print(d)
  # {'a': [1, 2], 'b': [3], 'c': [4]}
  ```

  

## defaultdict VS dict.setdefault

- 상황에 따라 다르게 사용하면 됨!   [참고](<http://stupidpythonideas.blogspot.com/2013/08/defaultdict-vs-setdefault.html>)

  - 만약 아예 빈 리스트 전체를 multidict으로 사용해야 할 경우에는 **defaultdict()** 사용하는 것이 편리

    - value를 담을 공간에 대한 초기화를 생성과 동시에 한 번만 해주면 되니까
- 나중에 dict() 형변환을 해야 하더라도 더 빠르고 효율적
  - 모든 key에 대해 value가 여러 개일 필요가 없고, 일부 key만 multi values 를 가지면 된다면 **setdefault()**를 사용하는 것이 편리
    - 일부분의 key에만 setdefault 해주면 되기 때문에 굳이 전체를 초기화할 필요는 없지



### 실행속도는 defaultdict()가 빠름

> [참고](<https://docs.python.org/3/library/collections.html#defaultdict-examples>)

  - defaultdict는 처음 딕셔너리를 생성할 때 key : value를 담을 공간을 **한 번**에 초기화해줄 수 있음 (d= defaultdict(list))
  - 반면 setdefault()는 호출할 때마다 매번 인스턴스를 생성해야 하기 때문에 속도가 느릴 수 밖에 