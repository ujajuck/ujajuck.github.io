---
layout: post
title: "프로그래밍 언어의 기초"
subtitle: "언어형식과 속도"
date: 2021-02-15 00:09:00 -0400
background: 'https://source.unsplash.com/category/nature/1600x900'
---
프로그래밍 언어의 기초
========================
<br>
## 언어형식과 속도
--------------------------
### 인터프리터 언어 vs 컴파일 언어
* 인터프리터 언어
기계어로의 번역없이 한줄 한줄 해석 후 실행한다. 보안적 관점에서 우수하다.
ex) python, R

* 컴파일 언어
전체 프로그램을 기계어로 변환 후 실행.  소스 전체를 컴파일 해야하기 때문에 빌드 시간이 오래걸리나 실행시간 면에서 압도적이다.
ex) C,C++

* 자바는 인터프리터와 컴파일 둘을 모두 사용하는 언어다.
JVM에 올릴 .class 파일 생성을 위해 .java 파일을 컴파일 한다. java 인터프리터는 .class 파일이 특정 환경에서 동작하도록 한줄 한줄 실행한다.<br>
![image](https://mblogthumb-phinf.pstatic.net/MjAxODAzMTNfMjU1/MDAxNTIwOTM2MDg5NzU5.FC9iwVzwVFoJ7L3d7R1MF1YBW8BMwQV9DLS3wCNvSJsg.OEmYIspBpTdYGKlQYIPsfThUhCdxdcS_rJnTuU-CTfkg.PNG.ehcibear314/%EC%9E%90%EB%B0%94%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC%EC%99%80%EC%9E%90%EB%B0%94%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0.png?type=w800) <br>
즉, 자바는 JVM 만 설치되어 있다면 플랫폼에 종속적이지 않다는 장점을 가진다. 이러한 자바의 플랫폼 독립성은 기기마다 다른 기계어의 영향을 받지 않으므로 프로그램의 이식성을 높인다.

* 파이썬은 왜 느린가?
파이썬은 변수의 형태가 정해져 있지않은 동적타입의 언어이고 인터프리터 언어이다. <br>
+)파이썬은 암묵적인 자료형의 변환을 허용하지 않는 강타입 동적타입 언어다. 약타입 동적차입 언어에는 대표적으로 javascript 가 있다.

### 수행시간 어림짐작하기
1초안에 수행할 수 있는 연산은 1억(10^8)이라고 한다. <br>
여기서 시간제한 1초가 의미하는 것은, 내 코드를 실행했을 때 실행시간이 1초 내여야한다는 것을 뜻한다. <br>
대부분의 환경에서 1억번 연산이 1초 정도 걸리기 때문에, 내 코드에 제일 큰 테스트케이스를 돌려도 연산이 1억번 내여야만 통과가 된다는 것이다. <br>
심지어 백준에 문제도 있다. [백준 시간초과](https://www.acmicpc.net/problem/11332)
