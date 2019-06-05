---
title: python cookbook -3 (heapq - Implementing a Priority Queue)
date: 2019-06-05
categories:
 - python
 - cookbook

---



## Implementing a Priority Queue

- **Priority Queue** : 우선순위가 높은 순서대로 자료를 처리할 때 사용하는 자료구조 (complete binary tree)

  ```python
  import heapq
  
  class PriorityQueue:
      def __init__(self) :
          self._queue = []
          self._index = 0
          
      def push(self, item, priority) :
          heapq.heappush(self._queue, (-priority, self._index, item))
          self._index += 1
          
      def pop(self) :
          return heapq.heappop(self._queue)[-1]
  ```

  - PriorityQueue 객체 생성

  - push(self, item, priority)  

    - self._queue 리스트 객체에 ( **- priority**, `self.__index`, item) 넣기
    - **-priority**  :  우선순위를 마이너스 처리 했기 때문에 실제 우선순위가 클수록 heap에 넣을 값은 작아져서 heap의 맨앞에 위치하게 됨 (우선순위 5 --> -5)
  - **self._index**  :  튜플 객체끼리 비교를 할 때 (?) 사용할 수 있음 (priority가 같은 경우, index로 대소비교 가능)
  
- pop(self) 
  
  - self._queue 객체에서 마이너스 우선순위가 작은 객체를 pop()
  
    - 파이썬heap은 min-heap이기 때문에 heap[0]이 항상 제일 작은 값
    
    - [-1]을 해서 (-priority, self._index, item) 중에 item 값만 추출
  
  
  
### 적용하면

```python
class Item :
  def __init__(self, name) :
        self.name = name
  def __repr__(self) :
        return 'Item({!r})'.format(self.name)
```

- `__repr__(self)` 
  - 내장 함수 repr()에 의해 호출되어 객체의 **"형식적인 official"** 문자열 표현 시 사용 (디버깅 할 때 참고할 수 있음)
    - `__str__()` 은 str()과 format() print() 에 의해 호출된 **비형식적인 informal** 문자열 표현 (보다 편리하고 간단하게 사용 가능)
  - python interpreter가 해당 객체를 해석할 수 있는 공식적인 문자열로 나타낼 때 주로 사용한다
  - 객체 안에서 따로 `__str__()` 이 정의되어 있지 않으면 `__repr__(self)` 와 `__str__()`은 기능상 차이가 없음

```python
q = PriorityQueue()  # 객체생성

q.push(Item('foo'), 1)
q.push(Item('bar'), 5)
q.push(Item('koo'), 3)

print(q._queue)
# [(-5, 1, Item('bar')), (-1, 0, Item('foo')), (-3, 2, Item('koo'))]

print(q.pop())   # Item('bar')
print(q.pop())   # Item('koo')
print(q.pop())   # Item('foo')
```

