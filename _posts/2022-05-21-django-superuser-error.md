---
layout: post
title: Django superuser 생성 시 no such table에러
subtitle: 
categories: django
tags: [django]
---

### 현상
python manage.py createsuperuser 입력 시
```
django.db.utils.OperationalError:no such table: auth_user
```
위와 같은 오류가 뜨면서 진행이 안됨

### 해결
해당 테이블이 장고에 지정된 db에 존재하지 않아서 생긴 것으로 migration 생성, migrate하면 정상작동 되는 것을 확인
```
python manage.py makemigrations
python manage.py migrate
```