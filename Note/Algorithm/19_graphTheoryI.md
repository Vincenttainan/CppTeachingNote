# **C++ 筆記**  
## 圖論 Graph Theory I  

## 基礎知識  

什麼是圖？~~.jpg .png~~  

這才是圖  

<img width="452" alt="截圖 2024-07-17 上午10 02 59" src="https://github.com/user-attachments/assets/cc4ff615-3028-41bc-8661-d40014358245">

一張圖是由數個 **頂點** 和數個 **邊** 所組成  
像上圖就是由 $6$ 個 **頂點** 和 $5$ 個 **邊** 所組成  

而又因為圖的性質分為許多種圖  

---

## 圖論術語  

1. 邊 (edge)  
由兩個頂點連線而成，分為有向邊與無向邊  
有時上面會有權重，常代表時間 or 花費  

* 有向邊 : 只能走一個方向  
* 無向邊 : 可以來回  

<img width="452" alt="截圖 2024-07-17 上午10 11 39" src="https://github.com/user-attachments/assets/6783ce2a-339b-4092-807a-e187c9c7efb4">

2. 度數 (degree)  

* 無向圖中：連接這個點的邊數  
* 有向圖中：按照邊的方向分為**入度**與**出度**  
    * 入度：幾條邊可以進入這個點  
    * 出度：幾條邊可以出去這個點  

3. 相鄰 (adjacent)  
兩點間有一條邊連接  

4. 路徑 (path)  
一個頂點序列 相鄰兩頂點都有邊相連  

5. 環 (cycle)  
一條不重複走過頂點的路徑且起點=終點  

6. 迴路 (circuit)  
一條不重複走過邊的路徑且起點=終點  

7. 重邊 (multiple edge)  
一張圖中有兩條或以上一樣的邊  

8. 自環 (loop)  
自己的頂點可以經過一條邊走到自己  

9. 連通 (connected)  
若 $u , v$ 之間有一條路徑則為連通  

---

## 圖的類型  

主要分為有向圖與無向圖  

### 有向圖  
圖中都是有向邊  
<img width="452" alt="截圖 2024-07-18 上午9 46 20" src="https://github.com/user-attachments/assets/c4f28b58-d261-458d-8ec8-23caaaa08234">  

* 圖中沒有環 : 有向無環圖 (DAG)  
* 圖中有環 : 有向圖  

### 無向圖  

1. 簡單圖  
不存在自環與重邊  
<img width="452" alt="截圖 2024-07-18 上午9 51 11" src="https://github.com/user-attachments/assets/6f3d8246-d806-4a4f-9235-e34680ad32db">  

2. 連通圖  
圖中任兩點間都可以經由一些邊抵達  
<img width="452" alt="截圖 2024-07-18 上午9 51 11" src="https://github.com/user-attachments/assets/6f3d8246-d806-4a4f-9235-e34680ad32db">  

3. 樹 (tree)  
一張沒有環且連通的圖  
<img width="452" alt="截圖 2024-07-18 上午9 52 38" src="https://github.com/user-attachments/assets/89157f71-3427-4da6-a18b-3aec6502e521">  

4. 完全圖  
任兩點間都有一條邊  
<img width="452" alt="截圖 2024-07-18 上午9 54 28" src="https://github.com/user-attachments/assets/193f2a50-9f14-4cfd-935e-ab6bcfe5003e">  

5. 二分圖
可以將這張圖的頂點分為兩個集合  
滿足所有邊的兩個頂點都在不同集合  
<img width="452" alt="截圖 2024-07-18 上午9 57 23" src="https://github.com/user-attachments/assets/453b3f47-9cda-4776-879c-7450e1dadc5a">  

---

## 存圖  
~~Ctrl+S~~  

* 鄰接矩陣  
* 鄰接串列  

### 鄰接矩陣  
開 $V*V$ 的陣列， $G[u][v]$ 表示 $u , v$ 之間的 邊數 或 權重  
空間複雜度 $V*V$  
但可以 $O(1)$ 加邊刪邊  

### 鄰接串列  
開 $V$ 個 vector ，將第 $i$ 個點可以到達的點 push 進去第 $i$ 個 vector  
<img width="708" alt="截圖 2024-07-18 上午10 07 28" src="https://github.com/user-attachments/assets/6a08ab30-c503-4b8d-8958-b2eca915a30b">  
空間複雜度 $O(V+E)$  
加邊時間複雜度 $O(1)$ , 刪邊時間複雜度 $O(V)$  
如果有特別情況需要刪邊 可把 vector 改成 set  
加邊時間複雜度 $O(logV)$ , 刪邊時間複雜度 $O(logV)$  

### 實作  
```cpp
int n,m;
vector<int>G[N];

int main(){
	cin>>n>>m;
	for (int i=1;i<=m;i++){
		int u,v; cin>>u>>v;
		G[u].push_back(v);
		G[v].push_back(u);
	}
	return 0;
}
```

---

## 遍歷  

* DFS (深度優先搜索)  
* BFS (廣度優先搜索)  

<img width="660" alt="截圖 2024-07-19 上午9 39 23" src="https://github.com/user-attachments/assets/135a9e4f-f8cd-4219-a2ff-5ae60479257a">  

### DFS  
如同走迷宮，找到一條新路就一路走下去，當沒路時則原路返回  
所以只須紀錄這頂點是否有走過，每走到一個頂點就標記為走過  
當發現點有標記過就不要再走，沒標記過就走下去  

[DFS運作](https://www.youtube.com/watch?v=7fujbpJ0LB4&t=80)  

特殊性質：之後會提到很多  

### DFS 實作  
通常以遞迴實作  
除非有題目卡 overflow ，再改用 stack  
```cpp
void dfs(int p){
    vis[p]=1;
    for(auto i:G[p]){
        if(!vis[i]){
            dfs(i);
        }
    }
}
```

### BFS  
一口氣把可以走的路都放進清單中  
再一條一條慢慢拿出來走  
跟DFS一樣標記每個點是否走過  
如果走過就不用再放進清單內了  

[BFS運作](https://www.youtube.com/watch?v=oDqjPvD54Ss&t=90s)  

特殊性質 : 可以發現若邊不帶權，走到的路徑長度會是最短路徑  

### BFS 實作  
通常以 queue 做為清單來實作  
```cpp
void bfs(int u){
    queue<int>q;
    q.push(u);
    vis[u]=1;
    while(!q.empty()){
        int v=q.front();
        q.pop();
        for(auto i:G[v]){
            if(!vis[i]){
                vis[i]=vis[v]+1;
                q.push(i);
                q.pop();
            }
        }
    }
}
```


