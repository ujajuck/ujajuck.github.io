---
layout: post
title: 복원
subtitle: 9개
date: '2021-03-30 00:01:13 -0400'
background: 'http://source.unsplash.com/category/nature/1600x900'
published: true
---

## 위대한 항로

> 다익스트라
> 출발점 반대로 하기

<details>
<summary>code</summary>
  
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
  
</details>


##  생산품

> 투 포인터 활용(O(n))
> 모르겠다 진짜....


## 나이트의 이동

> 다익스트라

<details>
<summary>code</summary>
  
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;

public class Remind03 {
	static class point{
		int x;
		int y;
		public point(int y, int x) {
			super();
			this.x = x;
			this.y = y;
		}
	}
	static String[][] map;
	static int[][] cost;
	static double[][] cnt;
	static point start;
	static point end;
	static int[] dx= {1,2,2,1,-1,-2,-2,-1};
	static int[] dy= {2,1,-1,-2,-2,-1,1,2};
	static int Y;
	static int X;
	static int ans;
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
		int tc=Integer.parseInt(br.readLine());
		for(int t=1;t<=tc;t++) {
			String[] line=br.readLine().split(" ");
			Y=Integer.parseInt(line[0]);
			X=Integer.parseInt(line[1]);
			map=new String[Y][X];
			cost=new int[Y][X];
			cnt=new double[Y][X];
			for(int i=0;i<Y;i++) {
				line=br.readLine().split("");
				for(int j=0;j<X;j++) {
					map[i][j]=line[j];
					cost[i][j]=Integer.MAX_VALUE;
					if(map[i][j].equals("S")) {
						start=new point(i,j);
					}
					if(map[i][j].equals("D")) {
						end=new point(i,j);
					}
				}
			}
			ans=0;
			cost[start.y][start.x]=0;
			cnt[start.y][start.x]=1;
			solv();
			for(int i=0;i<Y;i++) {
				for(int j=0;j<X;j++) {
					System.out.printf(cost[i][j]+" ");
				}
				System.out.println();
			}
			
			System.out.printf("#"+t+" ");
			if(cost[start.y][start.x]==Integer.MAX_VALUE)System.out.println("-1");
			else System.out.println(cost[end.y][end.x]+" "+(int)cnt[end.y][end.x]%1000000007);
		}
	}
	private static void solv() {
		int y=start.y,x=start.x;
		Queue<point> q=new LinkedList<>();
		q.add(start);
		while(!q.isEmpty()) {
			point now=q.poll();
			y=now.y;
			x=now.x;
			//System.out.println(y+" "+x);
			for(int v=0;v<8;v++) {
				//System.out.println(v);
				if(y+dy[v]>=Y||y+dy[v]<0||x+dx[v]>=X||x+dx[v]<0) {
					continue;
				}
				if(map[y][x].equals("R")&&map[y+dy[v]][x+dx[v]].equals("R")) {
					continue;
				}
				if(map[y+dy[v]][x+dx[v]].equals("#")) {
					continue;
				}
				if(map[y+dy[v]][x+dx[v]].equals("R")) {
					if(cost[y+dy[v]][x+dx[v]]<cost[y][x])continue;
					if(cost[y+dy[v]][x+dx[v]]==cost[y][x]) {
						cnt[y+dy[v]][x+dx[v]]+=cnt[y][x];
						continue;
					}
					cost[y+dy[v]][x+dx[v]]=cost[y][x];
				}else {
					if(cost[y+dy[v]][x+dx[v]]<cost[y][x]+1)continue;
					if(cost[y+dy[v]][x+dx[v]]==cost[y][x]+1) {
						cnt[y+dy[v]][x+dx[v]]+=cnt[y][x];
						continue;
					}
					cost[y+dy[v]][x+dx[v]]=cost[y][x]+1;
				}
				cnt[y+dy[v]][x+dx[v]]+=cnt[y][x];
				q.add(new point(y+dy[v], x+dx[v]));
			}
		}
	}
}
  
```
</details>

## 모니터링

> 시간 터짐.... 문제조건 이거 맞는건가
> 서버를 연결리스트 형식으로 만들어 pq에 넣음 기준 sum
> 작업 추가 작업 시간 갱신시 누적합 테이블 time[cnt]+=time[cnt-1], 현재 서버의 총 작업시간 sum을 갱신(pq 정렬 속도) k log n
> server를 일반 node 배열로 카운딩소트하여 옮김 ---> k
> 입력받은 서버에서 입력받은 시간을 이분 탐색으로 탐색(입력받은 시간보다 크지 않으면서 가장 가까운. 누적 이분탐색 사용가능할듯) ---> q log k

<details>
<summary>code</summary>
  
  ```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.util.PriorityQueue;
import java.util.Scanner;

public class Remind04 {
	static class server implements Comparable<server>{
		int idx;
		int[] time=new int[100000];
		int sum;
		int cnt;
		public server(int idx) {
			super();
			this.idx = idx;
		}
		@Override
		public int compareTo(server o) {
			return Integer.compare(this.sum, o.sum);
		}
	}
	public static void main(String[] args) throws FileNotFoundException {
		System.setIn(new FileInputStream("remind04input.txt"));
		Scanner sc=new Scanner(System.in);
		int k=sc.nextInt();
		int n=sc.nextInt();
		int q=sc.nextInt();
		PriorityQueue<server> pq=new PriorityQueue<>();
		for(int i=1;i<=n;i++) {
			pq.add(new server(i));
		}
		for(int i=0;i<k;i++) {
			server temp=pq.poll();
			int input=sc.nextInt();
			temp.time[temp.cnt+1]=temp.time[temp.cnt]+input;
			temp.cnt++;
			temp.sum+=input;
			System.out.println(temp.idx+" "+temp.cnt+" "+temp.time[temp.cnt]+" "+input+ " "+i);
			pq.add(temp);
		}
		server[] list=new server[n+1];
		while(!pq.isEmpty()) {
			server temp=pq.poll();
			list[temp.idx]=temp;
		}
		int sum=0;
		for(int i=0;i<q;i++) {
			int num=sc.nextInt();
			int time=sc.nextInt();
			int idx=0;
			for(int j=list[num].cnt/2;j>=1;j/=2) {
				while(idx+j<=list[num].cnt&&time>list[num].time[idx+j]) {
					idx+=j;
				}
			}
			sum+=Math.max(0,list[num].time[idx+1]-time);
		}
		System.out.println(sum);
	}
}

  
  ```
</details>

## 사탕먹기

> 양쪽 LCS 
> []()


<details>
  		<summary>code</summary>
</details>

## 거미

> 다익스트라


<details>
<summary>code</summary>
  
```java
import java.util.HashSet;
import java.util.PriorityQueue;
import java.util.Queue;
import java.util.Scanner;
import java.util.Set;
import java.io.FileInputStream;

class Remind06
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
</details>

## 프리랜서

> 배낭으로 비용구함
> pq로 시작시간 시작시간이 같을경우 끝시간 빠른순서로 정렬
> 시작할때 cnt++, 시작시간 저장; 끝날때 cnt--, sum+=knapsack(현재-시작시간);

## 프로젝트

> 위상정렬+디피라는데 과연....

## 수열

> 이분탐색으로 찾고 세그먼트트리에 최대 최소 저장해놓기
