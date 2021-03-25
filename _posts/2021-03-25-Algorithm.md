---
layout: post
title: Test Solution
subtitle: testing
date: '2021-03-24 00:01:13 -0400'
background: /img/posts/01.png
published: true
---

# Dijkstra

```java

import java.util.HashSet;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.Scanner;
import java.util.Set;
import java.io.FileInputStream;

class Pro0312
{
	static double[][] map;
	static double[][] vis;
	static int x;
	static int y;
	static int[] vx= {0,0,1,-1};
	static int[] vy= {1,-1,0,0};
	static double max;

	static class point implements Comparable<point>{
		int dx;
		int dy;
		public point(int dx, int dy) {
			super();
			this.dx = dx;
			this.dy = dy;
		}
		@Override
		public int compareTo(point o) {
			// TODO Auto-generated method stub
			if(map[o.dy][o.dx]<map[this.dy][this.dx]) {
				return -1;
			}else {
				return 0;
			}
			/*
			 * vis 비교하면 안된다 무조건 map 이다
			 * vis 는 초기 값이 0이기 때문에 방문 안한점이 있으면 우선0 순위가 되버려서 , vis로 비교하면 전체를 다 도는게 됨.
			 * 최대한 쓸데없는데 방문을 덜하려고 pq를 쓰는 거니까 이런거 주의하자.  
			 */
			//return (int)(o.cost-this.cost);
		}
	}
	public static void main(String args[]) throws Exception
	{
		Scanner sc = new Scanner(System.in);
		int T=sc.nextInt();

		for(int test_case = 1; test_case <= T; test_case++)
		{
			y=sc.nextInt();
			x=sc.nextInt();

			map=new double[y][x];
			vis=new double[y][x];
			for(int i=0;i<y;i++) {
				for(int j=0;j<x;j++) {
					map[i][j]=0.9999+0.000001*sc.nextDouble();
				}
			}
			PriorityQueue<point> pq=new PriorityQueue<>();
			vis[0][0]=map[0][0];
			pq.add(new point(0,0));
			while(!pq.isEmpty()) {
				point now=pq.poll();
				//System.out.println(now.dy+" "+now.dx);
				for(int i=0;i<4;i++) {
					if(now.dy+vy[i]>=y||now.dy+vy[i]<0||now.dx+vx[i]>=x||now.dx+vx[i]<0)continue;
					if(vis[now.dy+vy[i]][now.dx+vx[i]]<vis[now.dy][now.dx]*map[now.dy+vy[i]][now.dx+vx[i]]) {
						vis[now.dy+vy[i]][now.dx+vx[i]]=vis[now.dy][now.dx]*map[now.dy+vy[i]][now.dx+vx[i]];
						pq.add(new point(now.dx+vx[i], now.dy+vy[i]));
					}
				}
			}
			System.out.printf("#%d %.6f\n",test_case,vis[y-1][x-1]);
		}
	}

}

```

# Tree


```java

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.util.LinkedList;
import java.util.Scanner;


public class Pro0319 {
	static class node{
		int parent;
		int idx;
		long sum;
		long max=Integer.MIN_VALUE;
		long cost;
		LinkedList<Integer> children=new LinkedList<>();
		public node(int parent, long cost) {
			super();
			this.parent = parent;
			this.cost = cost;
			//this.max=cost;
			//this.sum=cost;
		}

	}
	static node[] list;
	static long[] ans;
	public static void main(String[] args) throws FileNotFoundException {
		System.setIn(new FileInputStream("input.txt"));
		Scanner sc = new Scanner(System.in);
		int t=sc.nextInt();
		//System.out.println(t);
		for(int tc=1;tc<=t;tc++) {
			int n=sc.nextInt();
			int r=sc.nextInt();
			ans=new long[2];
			list=new node[500001];
			node root=new node(0,r);
			list[0]=new node(-1,0);
			list[1]=root;
			for(int i=2;i<=n;i++) {
				int p=sc.nextInt();
				long c=sc.nextLong();
				list[i]=new node(p,c);
				list[i].idx=i;
				node parent=list[i];
				list[p].children.add(i);
				System.out.println(i+" "+p+" "+c);
				while(parent!=null) {
					parent.sum+=c;
					parent.max=Math.max(parent.max, parent.sum);

					if(parent.parent==-1)break;
					parent=list[parent.parent];
				}
			}
			for(int i=0;i<root.children.size();i++) {			
				if(list[root.children.get(i)].sum>=ans[1]) {
					getmax(list[root.children.get(i)],list[root.children.get(i)].sum);
				}
			}
			//getmax(root,0);
			for(int i=0;i<=n;i++) {
				if(list[i]!=null)
					System.out.println(i+" : "+list[i].cost+" "+list[i].sum+" "+list[i].max);
			}
			System.out.println(ans[0]+" "+ans[1]);
		}
	}
	private static void getmax(node now,long now_max) {
		if(now.max==now.sum) {
			//System.out.println(now.idx);
			if(ans[0]<now.sum) {
				ans[1]=ans[0];
				ans[0]=now.sum;
			}else if(ans[1]<now.sum) {
				ans[1]=now.sum;
			}
		}
		for(int i=0;i<now.children.size();i++) {			
			if(list[now.children.get(i)].sum>=now_max) {
				getmax(list[now.children.get(i)],list[now.children.get(i)].sum);
			}
		}
	}
}

```

# 양쪽 LIS

[LIS 설명](https://hyun0k.tistory.com/entry/Baekjoon11054%EA%B0%80%EC%9E%A5-%EA%B8%B4-%EB%B0%94%EC%9D%B4%ED%86%A0%EB%8B%89-%EB%B6%80%EB%B6%84-%EC%88%98%EC%97%B4DP)
[문제 링크](https://www.acmicpc.net/problem/11054)

```java

import java.util.Scanner;

public class Main11054 {
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		int n=sc.nextInt();
		int[] num=new int[n];
		for(int i=0;i<n;i++)num[i]=sc.nextInt();
		int[] dp1=new int[n];
		int[] dp2=new int[n];
		int idx1=0,idx2=0;
		for(int i=0;i<n;i++) {
			for(int j=0;j<i;j++) {			
				if(num[j]<num[i]) {
					dp1[i]=Math.max(dp1[j]+1,dp1[i]);
				}
				if(num[n-1-j]<num[n-1-i]) {
					dp2[n-1-i]=Math.max(dp2[n-1-j]+1,dp2[n-1-i]);
				}
			}
		}
		int max=0;
		for(int i=0;i<n;i++) {
			//System.out.println(dp1[i]+" "+dp2[i]);
			if(max<dp1[i]+dp2[i])max=dp1[i]+dp2[i];
		}
		System.out.println(max+1);
	}
}

```


* [부분수열의 증가수열 D6 X](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXgZWImaAwYDFASW&categoryId=AXgZWImaAwYDFASW&categoryType=CODE&problemTitle=%EB%B6%80%EB%B6%84%EC%88%98%EC%97%B4%EC%9D%98&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [두트리 D6 X](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXfRipHqKacDFAS5&categoryId=AXfRipHqKacDFAS5&categoryType=CODE&problemTitle=%EB%91%90+%ED%8A%B8%EB%A6%AC&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [보물 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXeJNmQqSCsDFAS5&categoryId=AXeJNmQqSCsDFAS5&categoryType=CODE&problemTitle=%EB%B3%B4%EB%AC%BC&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [최솟값의 인덱스 D6 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXdHx9X6C5IDFAS5&categoryId=AXdHx9X6C5IDFAS5&categoryType=CODE&problemTitle=%EC%B5%9C%EC%86%9F%EA%B0%92&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [연속하는 수의 곱셈 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXb6NiNKvHsDFARR&categoryId=AXb6NiNKvHsDFARR&categoryType=CODE&problemTitle=%EC%97%B0%EC%86%8D%ED%95%98%EB%8A%94&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [가위바위보와 무승부 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXaSbPaKPckDFASQ&categoryId=AXaSbPaKPckDFASQ&categoryType=CODE&problemTitle=%EA%B0%80%EC%9C%84&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [보석도둑 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXZudmIa0AoDFAST&categoryId=AXZudmIa0AoDFAST&categoryType=CODE&problemTitle=%EB%B3%B4%EC%84%9D&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [쿼리의최대값 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXYmnKa6dYoDFAST&categoryId=AXYmnKa6dYoDFAST&categoryType=CODE&problemTitle=%EC%BF%BC%EB%A6%AC&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [클러스터링 D6 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXXjDfE662IDFAST&categoryId=AXXjDfE662IDFAST&categoryType=CODE&problemTitle=%ED%81%B4%EB%9F%AC&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [01채우기 D5 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXWXPp76-b8DFAST&categoryId=AXWXPp76-b8DFAST&categoryType=CODE&problemTitle=%EC%B1%84%EC%9A%B0%EA%B8%B0&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [트리 부수기 D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXVJpLGqK7wDFASe&categoryId=AXVJpLGqK7wDFASe&categoryType=CODE&problemTitle=%ED%8A%B8%EB%A6%AC&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [수만들기 D6 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXTC4piqD_IDFASe&categoryId=AXTC4piqD_IDFASe&categoryType=CODE&problemTitle=%EC%88%98+%EB%A7%8C%EB%93%A4%EA%B8%B0&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [조 신나  D5 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXSVnJc6EHIDFAQT&categoryId=AXSVnJc6EHIDFAQT&categoryType=CODE&problemTitle=%EC%8B%A0%EB%82%98&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [수나열누기  D6](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXRSfaWq-igDFAXS&categoryId=AXRSfaWq-igDFAXS&categoryType=CODE&problemTitle=%EC%88%98%EB%82%98%EC%97%B4%EB%88%84%EA%B8%B0&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [셋이놀기 D5 ](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AXO8U7N6RBEDFAXS&categoryId=AXO8U7N6RBEDFAXS&categoryType=CODE&problemTitle=%EC%85%8B&orderBy=FIRST_REG_DATETIME&selectCodeLang=ALL&select-1=&pageSize=10&pageIndex=1)
* [철인 N 종 경기](https://velog.io/@doontagi/%EA%B7%B8%EB%9E%98%ED%94%84-%EC%B5%9C%EB%8B%A8%EA%B1%B0%EB%A6%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-1-%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C-3-%EC%B2%A0%EC%9D%B8-N%EC%A2%85-%EA%B2%BD%EA%B8%B0-qcjyf2ngdm)