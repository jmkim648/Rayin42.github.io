---
layout: post
title: Django로 여러 앱을 구축할 때
subtitle: 
categories: django
tags: [django]
---

## Template의 위치
 - 앱 경로 내부에 /templates/app_name의 폴더를 만들고 그 곳에 template 파일을 저장한다.
 - view에서 template을 참조하는 경우 app_name/file_name으로 기재한다.

### 이유

 - 예를 들어 app1/templates 폴더가 비어 있고, app2/template 폴더에 index.html이 있을 때 app1에서 index.html을 호출하면 app2/template의 index.html이 검색되어 표시된다. 이를 피하기 위해 각 template 폴더에서도 app_name폴더를 추가해 경로를 지정해준다.

 ---

## 정적 파일(Static)의 위치
 - 정적 파일 : 자바스크립트, 이미지, CSS 등
 - 각 app 경로에 /static/app_name이라는 폴더를 생성, 그곳에 파일을 저장한다.

 ### 이유
  - Deployment 시 collectstatic을 실행할 때 각 static 폴더 밑의 내용을 그대로 복사하므로 동명 파일들이 충돌하지 않게 하기 위함 (공부 더 필요)

---

## URL 설정
 - 각 app의 urls.py에 고유의 app_name을 설정
 - 프로젝트의 urls.py에 각 app의 정의를 include
 - template에서 app_name을 지정

### 이유

 ``` python
 # project/urls.py
 from django.contrib import admin
 from django.urls import path
 from app1 import views as v1
 from app2 import views as v2

 urlpatterns = [
    path('admin/', admin.site.urls),
    path('app1/', v1.HomeView.as_view(), name="app1home"),
    path('app2/', v2.HomeView.as_view(), name="app2home"),
 ]
 ```
 위와 같이 urlpatterns를 지정할 경우 url을 수정해야할 때마다 프로젝트도 수정해야하며 프로젝트가 복잡해질수록 name을 명명하기 어려워진다. 따라서 django의 include기능을 이용한다.

 - 우선, app/urls.py 작성
 ```python
 # app1/urls.py
 from django.urls import path
 from .apps import App1Config as config
 from . import views as v

 app_name = config.name # app1이 들어있다
 urlpatterns = [
    path('', v.HomeView.as_view(), name='home'),
 ]
 ```
 - 이후 project의 urls.py에 include
 ```python
 from django.contrib import admin
 from django.urls import path, include
 from app1 import urls as v1
 from app2 import views as v2
 
 urlpatterns = [
    path('admin/', admin.site.urls), path('app1/', include(v1)), # 변경（app1의URL을 추가）
    path('app2/', v2.HomeView.as_view(), name="app2home"),
]
 ```
 위와 같이 변경하면 자동적으로 app1의 url로의 라우팅이 추가된다. 이 때 view와 template의 html에도 변경이 필요하다.

 - 적당한 view가 작성되어 있다고 가정했을 때
 ```python
 # app1/urls.py
 from django.urls import path
 from .apps import App1Config as config
 from . import views as v

 app_name = config.name # app1이 들어있다
 urlpatterns = [
    path('', v.HomeView.as_view(), name='home'),
    path('app/', v.ApplicaionView.as_view(), name='app'), #추가된 부분
 ]
 ```
 ```python
 # app1/templates/index.html
 
 <!DOCTYPE html>
 <html lang="en">
   <head>
       <link href="{% static 'app1/main.css' %}" rel="stylesheet">
   </head>
   <body>
     <h1>Hello App1!</h1>
     <a href={% url 'app1:app' %}>링크</a>
   </body>
 ```
위의 index.html에서
```python
<a href={% url 'app1:app' %}>링크</a>
```
이 구문과 같이 지정하면 app명을 판정하여 링크를 만들어 app 간의 이름 충돌을 방지할 수 있다.


 ---
 ### 추가 공부 필요
 - Deployment 시 collectstatic을 실행 ~~
 - app/urls의 view 함수 중 ~~~.as_view()의 의미
 - url 전반적..
 