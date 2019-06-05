---
title: python cookbook -2 (heapq - finding Largest/Smallest N items)
date: 2019-06-04
categories:
 - python
 - cookbook
---



## Finding the Larges or Smallest N items

- import heapq

- heapq  모듈은 priority queue (heap queue)를 구현하여 사용할 수 있게 해준다

  - heap 
    - 최댓값 및 최솟값을 빠르게 찾기 위해 고안됨 (complete binary tree 기반)
    -  부모노드 A와 자식노드 B 의 키값 사이에 대소관계 성립 (A>B 최대힙, A<B 최소힙)

  - priority queue : **우선순위**가 높은 순서대로 자료를 처리할 때 사용한다
  - 파이썬은 해당 모듈을 내장하고 있는데, 최소힙(min heap)만 제대로 지원한다고 함 (?)  --> O(n logn)

```python
import heapq

nums = [1,4,2,15,6,7,8,2,9,-3,5,1,23,41,0]

print(heapq.nlargest(3,nums))  # [41, 23, 15]
print(heapq.nsmallest(3,nums))  # [-3, 0, 1]
```



- 보다 복잡한 자료구조에서도 사용할 수 있음! 

  ```python
  student = [
      {'name' : 'ychae', 'kor' : 100, 'math' : 90},
      {'name' : 'Leah', 'kor' : 80, 'math' : 100},
      {'name' : 'Mary', 'kor' : 70, 'math' : 85},
      {'name' : 'Jane', 'kor' : 77, 'math' : 65},
  ]
  
  kor = heapq.nlargest(2, student, key=lambda s:s['kor'])
  math = heapq.nsmallest(2, student, key=lambda s :s['math'])
  
  print(kor[0]['name'], kor[1]['name']) # ychae Leah
  print(math)  # [{'name': 'Jane', 'kor': 77, 'math': 65}, {'name': 'Mary', 'kor': 70, 'math': 85}]
  ```

  - `key= lambda` 로 조건으로 원하는 정보를 추출



## heapq의 중요한 점!

- heapify : 우선 주어진 자료들을 heap 형태의 list로 바꾼다

  ```python
  import heapq
  nums = [1,4,2,15,6,7,8,2,9,-3,5,1,23,41,0]
  heap = list(num)
  heapq.heapify(heap)
  print(heap)
  ```

- heap[0] 은 언제나 제일 작은 값 (smallest item)

  - 즉 heapq.headpop(heap) 을 계속하면 작은 값들을 계속 뽑아내는 것과 마찬가지