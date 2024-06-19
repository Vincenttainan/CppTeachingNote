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
