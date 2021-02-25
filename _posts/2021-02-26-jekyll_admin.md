---
layout: post
title: "Jekyll 관리자 페이지 추가"
subtitle: "Jekyll 관리자 페이지 추가"
date: 2021-02-26 00:09:00 -0400
background: '/img/posts/cool.jpg'
---
Jekyll 관리자 페이지 추가
====================

프로젝트 root에  Gemfile 파일에 아래 스크립트 추가

```
gem 'jekyll-admin', group: :jekyll_plugins
```


프로젝트 root에서 요청

```
bundle install
```

 http://localhost:4000/admin 으로 접속시 관리자페이지 접속가능

![image](/img/posts/cool.jpg)