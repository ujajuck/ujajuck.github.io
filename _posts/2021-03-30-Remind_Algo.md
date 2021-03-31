---
layout: post
title: 복원
subtitle: 9개
date: '2021-03-30 00:01:13 -0400'
background: 'https://source.unsplash.com/category/nature/1600x900'
published: true

---

## 위대한 항로

> 다익스트라
>
> 출발점 반대로 하기

```java
import java.util.PriorityQueue;
import java.util.Scanner;

public class Remind01 {
	static class Line implements Comparable<Line>{
		int to;
		int food;
		public Line(int to, int food) {
			super();
			this.to = to;
			this.food = food;
		}
		@Override
		public int compareTo(Line o) {
			if(this.food==o.food) return Integer.compare(this.to, o.to);
			return Integer.compare(Math.max(this.food-list[this.to].food,0), Math.max(o.food-list[o.to].food,0));
		}
		
	}
	static class island{
		int idx;
		int food;
		PriorityQueue<Line> to;
		public island(int idx, int food) {
			super();
			this.idx = idx;
			this.food = food;
			to=new PriorityQueue();
		}
		
	}
	static int min;
	static island[] list;
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		int tc=sc.nextInt();
		for(int t=1;t<=tc;t++) {
			int end=sc.nextInt();
			int line=sc.nextInt();
			int n=sc.nextInt();
			list=new island[100001];
			for(int i=0;i<100001;i++) {
				list[i]=new island(i,0);
			}
			for(int i=0;i<line;i++) {
				int from=sc.nextInt();
				int to=sc.nextInt();
				int food=sc.nextInt();
				list[to].to.add(new Line(from,food));
			}
			for(int i=0;i<n;i++) {
				list[sc.nextInt()].food=sc.nextInt();
			}
			min=Integer.MAX_VALUE;
			solv(end,0);
			System.out.println("#"+t+" "+min);
		}
	}
	private static void solv(int now, int cost) {
		if(now==1) {
			min=Math.min(min, cost);
			return;
		}
		while(!list[now].to.isEmpty()) {
			Line temp=list[now].to.poll();
			solv(temp.to,cost+Math.max(temp.food-list[temp.to].food,0));
		}
	}
}
```



##  생산품

