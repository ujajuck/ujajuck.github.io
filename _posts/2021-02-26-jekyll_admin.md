---
layout: post
title: Jekyll 관리자 페이지 추가
subtitle: Jekyll 관리자 페이지 추가
date: '2021-02-26 00:09:00 -0400'
background: /img/posts/cool.jpg
published: true
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

## Prose.io

[Prose.io](http://prose.io)

admin 페이지를 사용하는것 보다 빠르게 포스트 수정이 된다.<br>
모든 깃 프로젝트를 간단히 수정할때 add commit push 과정을 웹으로 간단히 사용할 수 있다.<br>
하단 참고 링크에 설명 참조<br>

## 참고
* https://honbabzone.com/jekyll/start-gitHubBlog/
* https://blog.webjeda.com/jekyll-admin/
* http://labs.brandi.co.kr/2018/05/14/chunbs.html
* [Prose.id 란?](https://theorydb.github.io/envops/2019/05/04/envops-blog-posting-prose-io/)
