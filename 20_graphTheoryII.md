# **C++ 筆記**  
## 圖論 Graph Theory II  

> ### [閹割版本 BFS ( TOJ 44 )](https://toj.tfcis.org/oj/pro/44/)  
> ### 輸入說明  
> 輸入第一行 $N, M$  (N, M≤ 1000)
> 接著有 $N$ 行，每行 $M$ 個 $0$ 或 $1$ 字元，表迷宮狀態  
> 最末行為 $x_1, \  y_1, \  x_2, \  y_2$ ，為起點與終點座標  
> 左上角為 $(0, 0)$ ，右下角 $(N−1, M−1)$  
> 原點在左上方，向下為 $x$ 軸正向，向右為 $y$ 軸正向  
> ### 輸出說明  
> 輸出 $(x_1, y_1) ∼ (x_2, y_2)$ 的距離  
> 若兩點之間沒有通路，則輸出 $−1$
> ### 輸入限制  
> $N, M \leq 1000$  
> ### 範例輸入  
> ```  
> 3 4  
> 0 0 1 0  
> 0 1 1 0  
> 0 0 0 0  
> 0 1 2 3  
> ```  
> 
> ### 範例輸出  
> ```  
> 6  
> ```  
> 
> ### 註  
> ```  
> 2 1 X 9  
> 3 X X 8  
> 4 5 6 7  
> ```  
> $7-1=6$ 所以距離為 $6$  

先把所有的輸入存起來  
```cpp
int n,m;
int x1,y1,x2,y2;
bool arr[1005][1005];

int main(){
	cin>>n>>m;
	for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cin>>arr[i][j];
		}
	}
	cin>>x1>>y1>>x2>>y2;
}
```

因為是閹割版的 bfs ，所以只需考慮要向 **上下左右** 走就可以了  
```cpp
int dx[4]={1,-1,0,0};
int dy[4]={0,0,1,-1};
```

還有因為將地圖是唯一格一格的，所以只要檢查當前的那格有沒有走過，和走訪是否合法就可以了  
```cpp
int vis[1005][1005];

bool check(int x,int y){
	if(x>=0&&x<n&&y>=0&&y<m&&arr[x][y]==0&&vis[x][y]==0){
		return 1;
	}
	else{
		return 0;
	}
}
```

接下來，因為這一題要求輸出最短距離，所以要用 bfs 來運算，而 bfs 就需要用到 queue 了  
```cpp
queue<pair<int,int> > q;
pair<int,int> _p;

int main(){
	//code
	_p.first=xme;
	_p.second=yme;
	q.push(_p);
}
```

bfs 的部分  
```cpp
void bfs(int x,int y){
	while(!q.empty()){
	    _p=q.front();
		int nowx=_p.first;
		int nowy=_p.second;
		q.pop();
		for(int i=0;i<4;i++){
			int todox=nowx+dx[i];
			int todoy=nowy+dy[i];
			if(check(todox,todoy)){
			    _p.first=todox;
			    _p.second=todoy;
				q.push(_p);
				vis[todox][todoy]=vis[nowx][nowy]+1;
			}
		}
	}
}

int main(){
	//code
	vis[xme][yme]=1;
	bfs(xme,yme);
	cout<<vis[xdoor][ydoor]-1<<endl;
}
```

### 完整程式碼  
```cpp
#include<bits/stdc++.h>
using namespace std;

queue<pair<int,int> > q;
pair<int,int> _p;
int n,m;
int dx[4]={1,-1,0,0};
int dy[4]={0,0,1,-1};
bool arr[1005][1005];
int vis[1005][1005];
int xme,yme,xdoor,ydoor;

inline bool check(int x,int y){
	if(x>=0&&x<n&&y>=0&&y<m&&arr[x][y]==0&&vis[x][y]==0){
		return 1;
	}
	else{
		return 0;
	}
}

inline void bfs(int x,int y){
	while(!q.empty()){
	    _p=q.front();
		int nowx=_p.first;
		int nowy=_p.second;
		q.pop();
		for(int i=0;i<4;i++){
			int todox=nowx+dx[i];
			int todoy=nowy+dy[i];
			if(check(todox,todoy)){
			    _p.first=todox;
			    _p.second=todoy;
				q.push(_p);
				vis[todox][todoy]=vis[nowx][nowy]+1;
			}
		}
	}
}

int main(){
	cin>>n>>m;
	for(int i=0;i<n;i++){
		for(int j=0;j<m;j++){
			cin>>arr[i][j];
		}
	}
	cin>>xme>>yme>>xdoor>>ydoor;
	_p.first=xme;
	_p.second=yme;
	q.push(_p);
	vis[xme][yme]=1;
	bfs(xme,yme);
	cout<<vis[xdoor][ydoor]-1<<endl;
}
```

---
