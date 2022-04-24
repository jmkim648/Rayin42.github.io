---
layout: post
title: Python으로 코드 작성 시 PEP8 스타일 가이드
subtitle: 
categories: python
tags: [python]
---


## PEP8

 - PEP8 : 파이썬 개선 제안서 -> 파이썬 코드를 어떻게 구상할 지 알려주는 스타일 가이드
 - 읽기 좋은 코드가 좋은 코드!
 - 스타일에 맞춰 코드를 작성하면 이후 수정하기도 편하다.


### 명명법

 - 함수, 변수, 속성 : losercase_underscore
 - protected 인스턴스 속성 : _leading_underscore
 - private 인스턴스 속성 : __double_leading_underscore
 - 클래스 및 예외 : CapitalizeWord
 - 모듈 수준 상수 : ALL_CAPS
 - 클래스의 인스턴스 메서드에서는 첫번째 파라미터 (해당 객체 참조)의 이름을 self로 지정
 - 클래스 메서드에서는 첫번째 파라미터(해당 클래스 참조)의 이름을 cls로 지정


### 공백, 줄바꿈

 - 코드 작성 시 한 줄의 문자 길이가 79자를 넘지 않도록
   - 줄을 바꿔야 할 때 예시
   ```python
    # 인수를 구분하기 위해 4칸 더 들여쓰기
    def long_function_name(
           var_one, var_two, var_three,
           var_four):
        print(var_one)

    #리스트 요소, 인수 등 표기
    my_list = [
        1, 2, 3,
        4, 5, 6,
    ]
    result = some_function_that_takes_arguments(
        'a', 'b', 'c',
        'd', 'e', 'f',
    )

    #연산자의 경우
    income = (gross_wages
              + taxable_interest
              + (dividends - qualified_dividends)
              - ira_deduction
              - student_loan_interest)

    
    #이후 추가...
   ```
 - Tab보다는 Space 4개를 활용(특히 섞어 쓰지 말 것!)
 - 함수와 클래스는 빈 줄 두개로 구분
 - 클래스에서 메서드는 빈 줄 하나로 구분
 - 변수 할당 앞 뒤에는 스페이스 1개
 - 리스트 인덱스, 함수 호출, 키워드 인수 할당에는 스페이스를 사용하지 않는다.


### 기타
 - import는 최상단에
   - import 순서 : 표준 라이브러리 모듈 > 서드파티 모듈 > 자신이 만든 모듈


### 참고
 - 어지간하면 IDE에서 자동으로 수정 혹은 지적해주지만 알아두자!
 - [PEP 8 – Style Guide for Python Code]
 
 
 
 
 
 
 [PEP 8 – Style Guide for Python Code]: (https://peps.python.org/pep-0008/)