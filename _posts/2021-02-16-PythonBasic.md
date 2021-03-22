---
layout: post
title: "Python 기초"
subtitle: "Python 기초문법"
date: 2021-02-16 00:09:00 -0400
background: 'https://source.unsplash.com/category/nature/1600x900'
---
Python 기초
========================
Data type
---------------------
내가 햇갈려서 정리하는 python 기초문법
type() 으로 데이터 타입 확인가능

|Data Structure|Oedered|변형가능|구성|Example|비고|
|--------------|-------|-------|----|-------|----|
|List|Yes|Yes|[] or list()|[3.2, 1, 'yes']|-----|
|Tuple|Yes|No|() or tuple()|(3.2, 1, 'yes')|괄호없이 선언시 default|
|Set|No|Yes|{} or set()|{3.2, 1, 'yes'}|빈 set을 만들려면 set ()을 사용|
|Dictionary|No|Yes|{} or dict()|{"a":3.2, "b":1, "c":'yes'}|키는 변경 불가능,dict_name[key]로 value 확인|

중괄호를 사용하여 {1, 2, 3}와 같은 집합을 정의 할 수 있습니다.<br>
그러나 다음과 같이 중괄호를 비워두면 {} Python이 대신 빈 사전을 만듭니다. 따라서 **빈 set을 만들려면 set ()을 사용하십시오.**
<br><br>
사전 자체는 변경 가능하지만 각 개별 키는 변경 불가능해야합니다.
