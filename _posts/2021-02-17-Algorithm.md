---
layout: post
title: "그래프 알고리즘"
subtitle: "그래프 알고리즘 정리"
date: 2021-02-17 00:09:00 -0400
background: '/img/posts/coding.jpg'
---

그래프 알고리즘 

============

## 그래프 표현 방식

-----------------

* 인접 행렬 표현
  
  * O(|v|^2) 공간 사용

* 인접 리스트 표현 

  * 희소 그래프 (간선의 수가 V^2 보다 훨씬 적은 그래프) 에서 유리
  
  * O(|V|X|E|) 공간 사용


## 그래프 깊이 우선 탐색

--------------------

시간 복잡도 : O(|V|X|E|)

위상정렬 : [고대어 사전 (하)](https://www.algospot.com/judge/problem/read/DICTIONARY)

오일러 서킷 : 그래프의 모든 간선을 정확히 한 번씩 지나서 시작점으로 돌아오는 경로를 찾는 문제

오일러 트레일 : 오일러 서킷처럼 그래프의 모든 간선을 정확히 한 번씩 지나지만, 시작점과 끝점이 다른 경로 

  * 무방향 그래프의 경우 모든 정점이 짝수개
  * 방향 그래프는 in == out

[단어 제한 끝말잇기(하)](https://www.algospot.com/judge/problem/read/WORDCHAIN)


### 참고 링크

-------------------------

> <https://namu.wiki/w/%ED%95%9C%EB%B6%93%EA%B7%B8%EB%A6%AC%EA%B8%B0>

> <https://sonsh0824.tistory.com/entry/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B3%B5%EB%B6%804-%ED%95%9C%EB%B6%93%EA%B7%B8%EB%A6%AC%EA%B8%B0Eulerian-circuit>

> <https://velog.io/@doontagi/%EA%B7%B8%EB%9E%98%ED%94%84-%EC%98%A4%EC%9D%BC%EB%9F%AC-%EC%84%9C%ED%82%B7%EA%B3%BC-%ED%8A%B8%EB%A0%88%EC%9D%BC>

> <https://projooni.tistory.com/entry/%EC%98%A4%EC%9D%BC%EB%9F%AC-%EC%84%9C%ED%82%B7>

> <https://coloredrabbit.tistory.com/36>

> <https://100100e.tistory.com/118>



## 그래프 너비 우선 탐색

----------------------


