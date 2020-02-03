##1241 油田(DFS)

一道最常规的dfs题

注意以后不要再写八个段来搜了

dfs() 是正常的形式

``` cpp
#include <bits/stdc++.h>
using namespace std;
const int INF = 0x3f3f3f3f;
typedef long long ll;
#define maxn 1005
char wos[maxn][maxn];
char dir[8][2] = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
int ans=0;
void init(){
		memset(wos,'\0',sizeof wos);
		ans=0;
}
void dfs(int row,int col){
	for(int i=0;i<8;++i){
		if(wos[row+dir[i][0]][col+dir[i][1]]=='@'){
			wos[row+dir[i][0]][col+dir[i][1]]='*';
			dfs(row+dir[i][0],col+dir[i][1]);
		}
	}
}
int main(){
	int r, c;
	while (~scanf("%d %d", &r, &c)){
		if (r == 0 && c == 0)break;
		init();
		for(int i=1;i<=r;++i){
			for(int j=1;j<=c;++j){
				cin>>wos[i][j];
			}
		}
		int row=1,col=1;
		for(;row<=r;++row){
			for(;col<=c;++col){//遍历行列不要忘了col的重置
				if(wos[row][col]=='@'){dfs(row,col);ans++;}
			}
			col=1;
		}
		printf("%d\n",ans);
	}
	return 0;
}

```
