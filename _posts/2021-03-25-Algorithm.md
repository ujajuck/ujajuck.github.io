---
layout: post
title: Test Solution
subtitle: testing
date: '2021-03-24 00:01:13 -0400'
background: /img/posts/01.png
published: true
---

Dijkstra

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

Tree

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
