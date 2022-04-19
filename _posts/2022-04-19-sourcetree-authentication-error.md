---
layout: post
title: SourceTree로 저장소에 Push할 때 Repo 접근 인증 에러
subtitle: 
categories: git
tags: [git]
---


## 문제

SourceTree 상에서 내 Github Repository를 원격저장소로 추가한 뒤 Push할 때, 과거 입력한 username, password에 문제가 없음에도 에러가 발생


### 오류 메시지
```
git -c diff.mnemonicprefix=false -c core.quotepath=false --no-optional-locks push -v --tags --set-upstream origin main:main remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead. remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information. fatal: Authentication failed for 'https://github.com/{user_name}/{repository_name}/
```



## 해결

기존 비밀번호 인증 지원방식은 더이상 지원되지 않고 앞으로 Github에서 personal access token을 발급받아 사용할 것.

1. 깃허브 프로필 -> Settings -> Developer Settings -> Personal access tokens에서 발급할 수 있다. 권한은 repo만 주거나 repo, user에만 줘도 무관한 듯.
2. 기존 Password방식을 사용했던 경우, C:\Users\{사용자명}\AppData\Local\Atlassian\SourceTree 경로에 있는 passwd 파일을 삭제해주어야 한다.(기존 저장되어 있던 pw)
