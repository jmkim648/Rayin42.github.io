---
layout: post
title: python 데코레이터
subtitle: 
categories: python
tags: [python]
---

## Decorator(장식자)
함수(메서드)를 장식하는 기능. 함수를 수정하지 않고 추가 기능을 구현하는 데 사용할 수 있다
```python
class A:
    @staticmethod    # 데코레이터
    def add(a, b):
        print(a + b)
```

### 예시
디버그 용도 등으로 함수의 시작과 끝에 print 기능을 넣을 때
```python
# 함수 내부
def A():
    print("A start")
    print("A")
    print("A end")


def B():
    print("B start")
    print("B")
    print("B end")


A()
B()
```
```python
# 데코레이터
def trace(func):                       # 호출할 함수를 매개변수로
    def wrapper():                     
        print(func.__name__, 'start')  # __name__으로 함수의 이름을 출력가능
        func()
        print(func.__name__, 'end')
    return wrapper


def A():
    print("A")


def B():
    print("B")


trace_A = trace(A)
trace_B = trace(B)
trace_A()
trace_B()
```
@를 사용하여 아래와 같이 바꿀 수 있다
```python
# def A() 이하 부분
@trace       # @데코레이터
def A():
    print("A")


@trace
def B():
    print("B")


A()
B()
```
함수의 위에 @로 데코레이터를 붙인 뒤 해당 함수를 그대로 호출하면 데코레이터가 적용된 것을 알 수 있다

### 기타
데코레이터는 중복해서 사용이 가능하다. 이 때 데코레이터는 위에서부터 아래 순으로 실행된다
```python
@trace1
@trace2
def A():
    print("A")


# @를 사용하지 않았을 때에는 다음 형태와 같다
trace_A = trace1(trace2(A))
trace_A()
```