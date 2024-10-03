# **C++ 筆記**  
## 動態規劃 DP II  

這篇接下來要講的是 DP 的一些基礎優化和一些方法  

---

### 滾動DP  

回到之前討論的這個問題，現在他被加強過了：  

> ## ex.ex. 背包問題（改）  
> 你有 $N$ 個物品跟一個可以裝下重量 $W$ 的背包，每個物品有重量 $w_i$ 跟價值 $v_i$  
> 在背包裡的總重量 $W$ 的條件下，最大化總價值  
> $1 \leq N \leq 100; 1 \leq W \leq 10^5; 1 \leq v_i \leq 10^9$  
> 
> ### **記憶體限制 $O(W)$**  

觀察我們原本的 DP 式：  
* $dp(i, j)$ ：考慮完前 $i$ 個物品，重量是 $j$ 的最大價值  
* $dp(i, j)$ = $max \{ dp(i-1, j), dp(i-1; j-w_i) \}$  
* $dp(0, j)$ = $0, (j \geq 0)$  

我們發現當 $i-1$ 被用來算 $i$ 之後，就不會再被算到了  
所以可以僅僅利用兩個陣列交替使用，就能算完全部的 DP 值  

```cpp
int dp[2][100005];

for(int i=1; i<=n; i++){
    for(int j=0; j<=w; j++){
        if(j>=w[i]){
            dp[i%2][j]=max(dp[(i-1)%2][j],dp[(i-1)%2][j-w[i]]);
        }
        else{
            dp[i%2][j]=dp[(i-1)%2][j];
        }
    }
}
```

在這題裡面，我們甚至能更進一步的壓縮：  
觀察到當 $dp(i+1, j+w_i)$ 算完之後，我只需要用來更新自己就好  
所以可以更進一步的把第二個迴圈倒過來，優化到只有一維的陣列：  

```cpp
int dp[100005];

for(int i=1; i<=n; i++){
    for(int j=w; j>=w[i]; j--){
        dp[j]=max(dp[j], dp[j-w[i]]);
    }
}
```

這個技巧就好像是 DP 的陣列滾動的被使用了，可以壓縮記憶體跟增加計算 DP 的快取優勢  
但要小心的是，並不是所有情況都可以如此滾動，需要仔細思考才能使用  

---

### 回溯 DP 解  

再回到這個問題，現在我們除了想知道答案，還需要一個構造：  

> ## ex.ex2. 背包問題（改2）  
> 你有 $N$ 個物品跟一個可以裝下重量 $W$ 的背包，每個物品有重量 $w_i$ 跟價值 $v_i$  
> 在背包裡的總重量 $W$ 的條件下，最大化總價值  
> ### **並輸出方案**  
> $1 \leq N \leq 100; 1 \leq W \leq 10^5; 1 \leq v_i \leq 10^9$  

我們的轉移代表什麼意義？  
$dp(i, j) = max \{ dp(i-1, j), dp(i-1; j-w_i) \}$  
紀錄轉移來源 $\rightarrow$ 構造一組解  

回頭看看轉移式：  
$dp(i, j) = max \{ dp(i-1, j), dp(i-1; j-w_i) \}$  
$dp(i, j) = max \{ 放, 不放 \}$  

所以最後我們可以發現  
從 $dp(N, W )$ 開始遞迴下去，往轉移的來源走直到碰到基底  

---

### 矩陣轉移

從之前的例題可以發現，大部分的 DP 再向下一層推算時  
所需要的都只會是前幾層的數值  

這時回想高中所教的矩陣，發現恰好可以應用在其上面  

以費氏數列為例：  
* $f(n)=f(n-1)+f(n-2)$  
* $f(0)=1,f(1)=1$  

改成數學是其實就可以變成：  

$$\left[
\begin{array}{cc}
f(n) & f(n-1) \\
\end{array}
\right]
\left[
\begin{array}{cc}
1 & 1 \\
1 & 0 \\
\end{array}
\right]=
\left[
\begin{array}{cc}
f(n)+f(n-1) & f(n)
\end{array}
\right]=
\left[
\begin{array}{cc}
f(n+1) & f(n)
\end{array}
\right]$$  

又  

$$\left[
\begin{array}{cc}
f(n+1) & f(n) \\
\end{array}
\right]
\left[
\begin{array}{cc}
1 & 1 \\
1 & 0 \\
\end{array}
\right]=
\left[
\begin{array}{cc}
f(n+1)+f(n) & f(n+1)
\end{array}
\right]=
\left[
\begin{array}{cc}
f(n+2) & f(n+1)
\end{array}
\right]$$  

所以可以推論出  

$$\left[
\begin{array}{cc}
f(n) & f(n-1) \\
\end{array}
\right]
\left[
\begin{array}{cc}
1 & 1 \\
1 & 0 \\
\end{array}
\right]
\left[
\begin{array}{cc}
1 & 1 \\
1 & 0 \\
\end{array}
\right]=
\left[
\begin{array}{cc}
f(n+2) & f(n+1)
\end{array}
\right]$$  

最後可得  

$$\left[
\begin{array}{cc}
f(n) & f(n-1) \\
\end{array}
\right]
\left[
\begin{array}{cc}
1 & 1 \\
1 & 0 \\
\end{array}
\right]^k=
\left[
\begin{array}{cc}
f(n+k) & f(n-1+k)
\end{array}
\right]$$  

為什麼要改成矩陣的乘法呢？  
以後講到快速冪時  
就可以將原本 $O(N)$ 的時間複雜度改成 $O(log(N))$ 了  


