---
layout: post
title: Markdown에서 이미지 삽입, 크기 조절
subtitle: 
categories: markdown
tags: [markdown]
---


마크다운 사용(사이즈 조절 불가능)

 ```markdown
    ![image](https://url/image.png)
 ```


HTML 태그 사용 (사이즈 조절)

 ```markdown
    <img src="https://url/image.png" width="50" height="50"/>
 ```


 - URL을 쓰려면 다른 저장소에 이미지를 넣어둔 후 링크를 해야하지만 img폴더를 따로 만들어서 경로를 잡아주면 훨씬 편하게 쓸 수 있다.
 ```markdown
 ![image](./img/screenshot.png)
 ```
