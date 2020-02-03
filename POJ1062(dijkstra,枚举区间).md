# POJ 1062 昂贵的聘礼

[题目](https://vjudge.net/problem/POJ-1062#author=0)

  这本来是一道常规的dijkstra题,但他有个等级的规则
  
  关键是接触了低等级的不能和高等级再接触
  
  这里有点DFS的味道

  这里用枚举区间的方法(在最短路问题中,规定可以走的路)
  这里要实现搜索,需要多次dijkstra(所以他的maxn只有100)

  需要把dijkstra写成函数,返回每次的dis值

  这样就需要初始化的注意
```
#include<iostream>
#include<cstring>
#include<stdio.h>
using namespace std;
const int INF=0x3f3f3f3f;
int dis[105];
bool vis[105];
int ple[105];
int wos[105][105];
int M,N;
int Min(int x,int y){
	return x>y ? y:x;
}
int dij(){
	for(int i=1;i<=N;++i){//init
		dis[i]=wos[0][i];
	}
	int min,pos;
	while(vis[1]){
		min=INF;
		pos=0;
		for(int i=1;i<=N;++i){
			if(min>dis[i] && vis[i]==true){
				min=dis[i];
				pos=i;
			}
		}
		vis[pos]=false;
		for(int i=1;i<=N;++i){
			if(vis[i]==true){
				dis[i]=Min(dis[i],min+wos[pos][i]);
			}
		}
	}
	return dis[1];
}
int main(){
	scanf("%d %d", &M, &N);
	for(int i=0;i<=N;++i){
		for(int j=0;j<=N;++j){
			if(i==j)wos[i][j]=0;
			else wos[i][j]=INF;
		};
	}
	int P,L,X,T,V;
	for(int i=1;i<=N;++i){
		scanf("%d %d %d",&P,&L,&X);
		wos[0][i]=P;
		ple[i]=L;
		while(X--){
			scanf("%d %d",&T,&V);
			wos[T][i]=V;
		}
	}
	int ans=INF;
	for(int i=1;i<=N;i++){
		int minLevel = ple[i];
		for(int j=1;j<=N;j++){
			if(ple[j] - minLevel > M || minLevel > ple[j])
				vis[j] = false;
			else{
				vis[j]=true;
			}
		}
		int now = dij();
		ans = Min(ans,  now);
	}
	printf("%d\n",ans);
	return 0;
}
```



多次的最短路-->搜索
