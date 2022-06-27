---
layout: post
title: Exception Handling (예외 처리)
subtitle: 
categories: programming
tags: [programming]
---

## Exception Handling?
  - Exception : 정상적인 프로그램 흐름을 중단시키는 에러
  - Exception Handling : 정상적인 프로그램 흐름을 중단하고 주변의 컨텍스트 또는 코드 블록에서 계속하기 위한 메커니즘

### 예시
Value Error가 발생했을 경우 -1을 리턴하고 코드가 중단하지 않는다.
```python
def convert(s):
    # int로 변환
    try:
        a = int(s)
        print("성공")
    except ValueError:
        print("실패")
        a = -1
    return a
```
결과
```python
>>> convert("test")
실패
-1
```
이 때, try의 마지막 구문인 "성공"은 출력되지 않는다. 에러가 발생하면 그 다음 코드는 건너뛰고 except블록으로 넘어가기 때문
```python
def convert(s):
    # int로 변환
    try:
        a = int(s)
        print("성공")
    except ValueError:
        print("ValueError")
        a = -1
    except TypeError:
        print("TypeError")
    return a
```
위와 같이 Error 종류 별로 except를 지정할 수 있으며,
```python
def convert(s):
    # int로 변환
    try:
        a = int(s)
        print("성공")
    except (ValueError, TypeError):
        print("실패")
        a = -1
    return a
```
except를 합칠 수도 있다