---
layout: post
title: Django secret key 관리
subtitle: 
categories: django
tags: [django]
---

포트폴리오 정리 중 과거 프로젝트 중 django secret key 외 보안관련 key가 그대로 올라가 있는 것을 발견했다.

## Secret key?
  - 쉽게 말해 보안에 관련된 것으로, 공식문서 스크린샷 첨부
  ![docs](/img/secretkey.JPG)
  - Cryptographic Signing이란?
     - Web application security의 기본은 신뢰할 수 없는 출처로부터 온 데이터를 신뢰하지 않는 것
     - 하지만 때로는 신뢰할 수 없는 매체를 통해 데이터를 전달해야할 때가 있으므로
     - value를 Cryptogaraphically sign(암호화적 서명)하는 것이 필요
  
### Secret key 생성
기본적으로 django 프로젝트 생성 시 50자의 랜덤 문자로 자동 생성된다. 이것을 사용하지 않을 때에는 [Django Secret Key Generator](https://miniwebtool.com/django-secret-key-generator/)를 사용해 생성할 수 있다.

### Secret key 관리
  - secrets.json 생성 (평소 dic 다루듯이 마지막에 ,를 넣으면 에러가 난다고 하니 주의)
```
{
    "AWS_SECRET_ACCESS_KEY": "aws-secret-access-key"
    "AWS_ACCESS_KEY_ID": "aws-access-key-id"
    "SECRET_KEY": "your-secret-key"
}
```
  - settings.py 수정
```python
import json
from django.core.exceptions import ImproperlyConfigured

secret_file = os.path.join(BASE_DIR, 'secrets.json') # secrets.josn 위치 명시

with open(secret_file) as f:
    secrets = json.loads(f.read())


def get_secret(setting, secrets=secrets):
    try:
        return secrets[setting]
    except KeyError:
        error_msg = "Set the {} environment variable".format(setting)
        raise ImproperlyConfigured(error_msg)

SECRET_KEY = get_secret("SECTRET_KEY")
```

  - 이후 .gitignore에 secrets.json 추가



#### 참고
  - Django 보안 때문에 SECRET_KEY 유출을 조심해야하는 것도 있지만 만약 AWS 계정과 비밀번호같은 것이 노출되면 도용되어 요금폭탄을 맞을 수도 있다고 한다!
  - 본문에는 설정파일 패턴만 기록해두었지만 환경변수 설정을 통해 설정할 수도 있다. 다만 Pycharm을 사용할 경우 일반적인 방식은 통하지 않는다고 하며(추후 확인) Pycharm 설정에서 환경변수를 추가해야 한다고 한다.
  - [Django 공식문서 SECRET_KEY](https://docs.djangoproject.com/en/4.1/ref/settings/#std:setting-SECRET_KEY)