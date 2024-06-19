# **C++ 筆記**  
## STL Standard Template Library  

STL 的全名是 Standard Template Library，中文為標準模板庫  
STL 提供了很多方便的容器跟算法，可以省下很多時間  

---

1. 迭代器與型別模板  
2. vector  
3. deque  
4. stack  
5. queue  
6. array  
7. bitset  
8. priority_queue  
9. set/map  
10. unordered_set/map  
11. pair/tuple  

---

## 1. 迭代器與型別模板  

型別模板是相對好理解的東西：它的用途是可以`只需要寫一個通用在所有你想支援的範圍內，就可以自動支援`  

以 vector 為例，如果你想要 vector 裡面裝著 T 這種類型，就只要宣告成  

```cpp
vector<t> name;
```

而迭代器則是可以想像成代表一個位置的東西  
有了它就可以直接存取它代表的元素  

如果你現在有一個迭代器 `iter`：  

* `*iter` 就可以取得這個迭代器的值  
* `++iter` 或 `next(iter)` 就可以取得下一個人  
* `--iter` 或 `prev(iter)` 就可以取得上一個人  
* `iter + k` 就可以取得下 `k` 個人  
* `iter - k` 就可以取得上 `k` 個人  
* `容器.begin()` 就可以取得最前面的人  
* `容器.end()` 就可以取得表示結束的那個人，通常會是最後一個人的下一個人，而他是不能取值的  

但要注意不是每個容器都可以進行這邊所有的操作，要視容器的特性而定  

因為型別模板的關係，迭代器的變數類型名稱通常很長，以 vector 為例  
```cpp
vector<int> v;
...
vector<int>::iterator iter=v.begin();
...
```

這時候就可以讓編譯器自動幫我們抓  
```cpp
vector<int> v;
...
auto iter=v.begin();
...
```

---

## 2. vector

vector 是一個可以動態變動大小的陣列  
支援隨機存取  
在陣列尾端新增、刪除 $O(1)$  
任意插入、刪除 $O(size)$  
交換兩個內容 $O(1)$  

vector 的原理相當簡單：  
`一開始空間是 1，當不夠用了就要一塊 2 倍大小的空間然後全部搬過去`  

大概就是下圖這樣  

<img width="843" alt="截圖 2024-06-19 上午11 51 56" src="https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/d647c5ef-6e7e-4d27-b71a-b9bd83a89ed8">  

這樣整體來講只要 $O(size)$ 就能完成所有在尾端加入的工作，均攤一個元素是 $O(1)$  

原因是總共的成本最多是  
$size + size + \frac{1}{2} \cdot size + \frac{1}{4} \cdot size \cdots \leq 3 \cdot size = O(size)$  

至於刪除跟中間插入就是直接暴力了  

* `v.push_back(k)`：把元素 `k` 加到 `v` 的尾巴，必要時會進行記憶體配置  
* `v.pop_back()`：移除 `v` 尾巴的元素  
* `v.insert(iter, k)`：在 `iter` 位置插入元素 `k`  
* `v.erase(iter)`：移除`iter`位置元素  
* `v.erase(star, end)`：移除某一段範圍的元素  
* `v.clear()`：清空容器 `v` 裡所有元素  
* `v.size()`：回傳目前容器 `v` 的長度  
* `v.empty()`：回傳容器 `v` 是否為空  
* `v[i]`：隨機存取容器 `v` 索引值為 `i` 的元素，跟陣列一樣索引值從 0 開始  

```cpp
vector<int> v={1, 2, 3};
                        // 1, 2, 3
v.push_back(4);
                        // 1, 2, 3, 4
auto iter=v.begin();
v.insert(iter+2,999);
                        // 1, 2, 999, 3, 4
v.pop_back();
                        // 1, 2, 999, 3
v.erase(iter);
                        // 2, 999 ,3
cout<<v.size()<<endl;   // output:3
cout<<v.empty()<<endl;  // output:0
v.erase(iter,iter+2);
                        // 3
v.clear();
                        // 
```

基本上，`vector` 已經可以當基本的陣列用了，還有更多的功能  
但是缺點是 `vector` 有些狀況下存取會比普通陣列慢，新增元素常數也稍大，需要稍微小心  



