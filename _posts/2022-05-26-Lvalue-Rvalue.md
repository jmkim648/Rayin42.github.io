---
layout: post
title: C++ Rvalue와 Lvalue, ++x와 x++
subtitle: 
categories: c++
tags: [c++]
---

## Lvalue와 Rvalue
  - C 표준 : 대입 연산자('=')를 기준으로 왼쪽과 오른쪽에 모두 사용될 수 있는 것은 Lvalue, 오른쪽에 위치하는 것이 Rvalue
  - C++ 표준 : 
    - Lvalue : 단일 표현식 이후에도 없어지지 않고 지속되는 개체 (이름을 가지는 객체, const타입 등의 변수는 Lvalue)
    - Rvalue : 표현식이 종료된 후 더 이상 존재하지 않는 임시적인 값

### 예시
```c++
#include <iostream>
#include <string>

using namespace std;

int main()
{
    int x = 3;
    const int y = x;
    int z = x + y;
    int* p = &x;

    cout << string("one");

    ++x;
    x++;
}
```
  - Lvalue : x, y, z, p 등의 이름을 가지는 변수, ++x
  - Rvalue : int x = 3;에서의 상수 값 3, 임시객체 string("one"), x + y, &x와 같은 표현식, x++

## ++x와 x++는 왜 다른가?
  - 둘 다 1 증가된 값을 리턴한다
  - ++x의 경우 증가된 x 자신을 리턴하기 때문에 Lvalue지만,
  - x++은 증가되기 전의 복사본 x를 리턴한 후 증가되기 때문에 Rvalue

### Lvalue와 Rvalue 구분이 어렵다면?
  - 표현식에 주소 연산자 '&'를 붙여본다
  - &연산자는 Lvalue를 요구하기 때문에 표현식이 Rvalue라면 컴파일 오류가 발생

#### 참고
[DevMachine's Blog : [C++11] Rvalue Reference #1 - Lvalue와 Rvalue](https://m.blog.naver.com/devmachine/176176191)