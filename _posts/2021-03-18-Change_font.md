---
layout: post
title: "GitBlog Custom"
subtitle: "블로그 폰트 바꾸기"
date: 2021-03-17 00:09:00 -0400
background: 'http://source.unsplash.com/category/nature/1600x900'
---
블로그 폰트 바꾸기
========================

Jekyll 블로그 clean blog 테마 css 수정하기

## 폰트 바꾸기

비상업용 무료 폰트 사이트 [눈누](https://noonnu.cc/)

```
.\assets\vendor\startbootstrap-clean-blog\scss\_bootstrap-overrides.scss
```


위 경로 css 수정

## Code block highlight 적용

cmd 에서 markdown 의 확장판? 인 kramdown을 설치

```
gem install kramdown rouge
```


코드블럭 css 스타일 복사

```
rougify style  base16.monokai
```

위 경로  bootstrap-overrides.css에 css 붙여널기

> <code></code> 헤더 사용시 css 가 안먹는다. ```(type) 을 사용하자

* [참고](https://syki66.github.io/blog/2020/02/08/clean-blog-highlighter.html)
