---
layout: post
title: python lambda 등 메모리 관리
subtitle: 
categories: python
tags: [python]
---

## lambda 함수
  - 익명함수 : 메모리를 아끼고 가독성을 향상시킨다
  - 일반적인 함수는 객체를 만들고, 재사용을 위해 함수 이름(메모리)를 할당한다
```python
# lambda 인수1, 인수2, ... : 인수를 이용한 표현식
sum = lambda a, b: a+b
sum(3,4)
```

### lambda는 왜 쓰는가?
  - 익명함수이기 때문에 한번 쓰이고 다음줄로 넘어가면 힙(heap)메모리 영역에서 증발
  - (*참고*) 가비지 컬렉터(참조하는 객체가 없으면 지워버림)
    - 파이썬에서는 모든 것이 객체로 관리되고 각 개체들은 레퍼런스 카운터를 가진다. 이 카운터가 0이 되면(참조하는 것이 없다면) 메모리를 환원하게 된다

## map
  - 내장함수
  - 입력받은 자료형의 각 요소가 함수에 의해 수행된 결과를 묶어서 map iterator 객체로 리턴
```python
# map(f, iterable)의 형태
li = [1, 2, 3] #Input
# Output : result = [1, 4, 9]

result = list(map(lambda i: i ** 2, li))
```
  - map을 사용하면 게으른 연산을 진행해 메모리를 절약
  - map의 연산 결과는 map iterator 객체로 리턴

### 게으른 연산
  - 필요할 때에 가져다 쓴다(map 함수의 결과 객체)
  - iterator 객체
    - next() 메소드로 데이터를 순차적으로 호출 가능한 object
    - 마지막 데이터까지 불러오면 다음은 StopIteration exception 발생
    - iterable한 객체를 iterator로 변환하고 싶다면 iter()라는 built-in function 사용
    - for문으로 반복하는동안 python 내부에서는 임시로 list를 iterator로 변환

```python
# ex1
li = [1, 2, 3]
result = map(lambda i: i * i, li)
next(result) # 1
next(result) # 4
next(result) # 9
next(result) # StopIteration 발생

# ex2
>>> x = [1, 2, 3]
>>> type(x)
<class 'list'>
>>> y = iter(x)
>>> type(y)
<class 'list_iterator'>
```

## 3항연산자

```python
# if else
def func(a):
    if a > 10:
        return 'a는 10보다 크다'
    else:
        return 'a는 10보다 작다'

# 3항연산자
def func2(a):
    return 'a는 10보다 크다' if a > 10 else 'a는 10보다 작다'

```

### 3항연산자 예제
  - 조건이 3개일 경우에도 사용 가능
```python
# Input : li = [-3, -2, 0, 6, 8]
# Output : ['음수', '음수', 0, '양수', '양수']

# 풀이 1
>>> ['양수' if i > 0 else ('음수' if i < 0 else 0) for i in li]
>>> ['음수', '음수', 0, '양수', '양수']

# 풀이 2
>>> list(map(lambda i: '양수' if i > 0 else ('음수' if i< 0 else 0), li))
>>> ['음수', '음수', 0, '양수', '양수']
```

## filter 함수
  - filter(f, iterable)
  - 두번째 인수인 반복가능한 자료형 요소들을 첫번째 인자 함수에 하나씩 입력하여 리턴값이 참인 것만 묶어서 돌려준다
  - 함수의 리턴값은 참 or 거짓

```python
li = [-2, -3, 5, 6]

# 양수만 반환하는 함수
def ft(li):
    result = []
    for e in li:
        if e > 0:
            result.append(e)
        else:
            pass
    return result


# filter 사용시
def positive(x):
    return x > 0


list(filter(positive, li))

# filter + lambda
list(filter(lambda x: x > 0, li))
```

--------------
메모리 관리가 필요한 코딩이나 코테 등에서 사용할 필요가 있을 것!