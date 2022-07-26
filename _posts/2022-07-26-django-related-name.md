---
layout: post
title: django 외래키 related_name 설정 방법
subtitle: 
categories: django
tags: [django]
---

## related_name
django 앱에서 model을 설정할 때, 외래키 설정 시 뒤에 related_name을 지정한다. 이 때, related_name이라는 속성이 참조하는 무언가에 관련된 이름인 것으로 착각되어 실수를 하는 경우가 생긴다.

### 예시
```python
class Member(models.Model):
    mem_id = models.AutoField(primary_key=True)
    ...

class Post(models.Model):
    post_id = models.AutoField(primary_key=True)
    post_userid = models.ForeignKey("Member", related_name="mem_id", on_delete=models.CASCADE, db_column="post_userid")
```
처음 검색해서 봤던 글 두군데에서 related_name을 설정할 때 상단과 같이 참조할 변수를 넣어놨었다. 하지만 이렇게 설정하니 make migration을 할 때 각종 에러가 발생.

### 해결
```python
class Member(models.Model):
    mem_id = models.AutoField(primary_key=True)
    ...

class Post(models.Model):
    post_id = models.AutoField(primary_key=True)
    post_userid = models.ForeignKey("Member", related_name="post", on_delete=models.CASCADE, db_column="post_userid")
```
참고한 내용
1. 외래키로 연결시켜 놓은 클래스에 related_name = post라고 해놓으면 member.post라는 것이 post 모델에 생기는 것이 아니라 post가 참조하고 있는 member에 생긴다.
2. 따라서 참조해준 객체 입장에서 related_name을 설정해줘야 한다

고 한다.
따라서 상단과 같이 related_name을 설정해주고, 해당 유저의 post를 가지고 오고 싶을 때 사용할 ORM은 comment = member.post.all()이 된다.

#### 기타
솔직히 제대로 이해를 하고 쓰고 있다고는 할 수 없고..추후 공부가 더 필요할 것.