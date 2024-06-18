# **C++ 筆記**  
## 時間複雜度 Time Complexity  

複雜度是用來表示一個東西的成長趨勢  
我們想知道這個東西跟什麼相關  
而那些又會怎麼影響這個東西  

舉例來說：$f(x) = x$ 跟 $g(x) = x^{2}$：  

<img width="525" alt="截圖 2024-06-17 上午11 27 00" src="https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/a6a8c67b-f5d0-4e2d-9322-c544a408280d">

可以看到 $g(x)$ 成長的比 $f(x)$ 快,而他們都受到 $x$ 的影響  

但如果是 $h(x) = \frac{1}{2}\cdot(x^2 + x)$：  

<img width="525" alt="截圖 2024-06-17 上午11 35 43" src="https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/51dea337-5d0d-48d8-9c20-7272dd26c7c1">

## Big O Notation

定義  
> 對於兩個函數 $f(x)$,$g(x)$  
如果能找到一個正實數 $k$ 及某個正實數 $x_0$  
使得對於所有 $x \geq x_0$ 都有 $f(x) \leq k \times g(x)$  
我們就說 $f(x) \in O(g(x))$ 或 $f(x) = O(g(x))$  

粗略的說就是如果 $g(x)$ 在乘上某個常數 $k$ 之後可以在 $x_0$ 以後  
永遠超過 $f(x)$,我們就可以說 $f(x) = O(g(x))$  
這個符號給了我們一個方法：  
如果 $f(x) = O(g(x))$,他在很大很大的時候,成長的樣子會跟 $g(x)$ 很像。  

可以看到即便 $h(x)$ 含有跟 $f(x)$ 類似的成分,但最終還是被 $\frac{1}{2}x^{2}$ 支配而看起來像 $g(x)$  

換句話說，我們可以發現一個很常會對的經驗法則：  

> 推論：  
> 對於一個函數 $f(x)$  
> 我們只要把長最快的那些項留下來  
> 然後把常數都拿掉得到 $g(x)$  
> 那就會有 $f(x) = O(g(x))$  

## 常見複雜度  

* $O(1)$  
常數時間，如果一個東西被說是 $O(1)$，那表示不論輸入多少，都只需要花一樣的時間  
例如 int 的加減乘除，輸入一個 int，都是常數時間，畢盡 int 的大小固定了，所需的時間也就固定了  

* $O(\log N)$  
對數時間，雖然它的成長很慢，例如例如二分搜的複雜度，當要搜尋的長度變大 $2$ 倍， $log_2 N$ 才會多 $1$ ，但不能忽略不計  

* $O(N)$  
線性時間，這個東西跟輸入 $(N)$ 成長的一模一樣快  
例如輸入一個陣列就只要線性時間  

* $O(2^N)$ , $O(3^N)$ $\cdots$  
指數時間，這東西只要輸入多 $1$ 就會倍數成長  
成長數度非常快，比所有多項式還快（在 $N$ 很大的情況下）  

## 範例

```cpp
int arr[1000005];

int main(){
    int n;
    cin >> n;
    for(int i=0; i<n; i++){
        cin >> arr[i];
    }
}
```
> 上面的程式碼總共進行了 $n+1$ 次的輸入  
> 因為輸入時間是常數的  
> 所以複雜度是 $O(n)$

```cpp
int arr[1005][1005];

int main(){
    int n,m;
    cin >> n >> m;
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            cin >> arr[i][j];
        }
    }
}
```
> 上面的程式碼總共進行了 $n \times m+2$ 次的輸入  
> 所以複雜度是 $O(nm)$  

根據上面的迴圈範例可以發現，當做了 $O(N)$ 次花費 $O(M)$ 的事  
複雜度剛好是 $O(N \times M)$  

```cpp
int arr[30],cnt;

int main(){
    int n,k;
    cin >> n >> k;
    //迴圈1
    for(int i=0; i<n; i++){
        cin >> arr[i];
    }
    //迴圈2
    for(int mask=0; mask<(1<<n);i++){
        int sum=0;
        for(int i=0; i<n; i++){
            if((mask>>i)&1){
                sum+=arr[i];
            }
        }
        if(sum==k){
            cnt++;
        }
    }
    cout << cnt << endl;
}
```
> 上面的演算法中，第一個迴圈需要 $O(n)$  
> 第二個迴圈跑了 $2^n$ 次，每次花 $O(n)$ 檢驗  
> 所以總複雜度是 $O(2^n \times n)$  

這是一掌簡單的圖表  
<img width="525" alt="截圖 2024-06-17 下午3 30 20" src="https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/c0110f19-e071-4ccb-89e6-d5ce1a8472b1">

