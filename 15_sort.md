# **C++ 筆記**  
## 排序 Sort  

常見的排序演算法有：  

* 泡泡排序 Bubble Sort  
* 選擇排序 Selection Sort  
* 插入排序 Insertion Sort  
* 快速排序 Quick Sort  
* 合併排序 Merge Sort  
* 堆積排序 Heap Sort  

等等  

---

## 1. 泡泡排序 Bubble Sort  

時間複雜度： $O(N^2)$  

想法：  

如果這個數字比右邊的大，交換兩位置，使較大的逐漸浮到右側，再縮小範圍進行下一回合  

圖示：  

![bubble](https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/fa2b3dcd-0b69-4073-ae86-c5e5d7747824)

說明：  

使用雙層迴圈，**外層迴圈** 控制回合數，**內層迴圈** 控制每一回合的比較次數  

**外層迴圈** 只需比較到倒數第二個數字( $n-1$ )就可以停止，因為 a[j+1] 會比較到最後一個數字  
**內層迴圈** $(n-1-i)$ 代表比較範圍會隨著已經排序好的數量增加而減少  

```cpp
for(int i=0; i<n-1; i++){
    for(int j=0; j<(n-1-i); j++){
        if(a[j]>a[j+1]){
            swap(a[j],a[j+1]);
        }
    }
}
```

---

## 2. 選擇排序 Selection Sort  

時間複雜度： $O(N^2)$  

想法：  

在未排序區中找最小值，放置在已排序區的末尾  

圖示：  

![selection](https://github.com/Vincenttainan/CppTeachingNote/assets/54768760/5d79c162-76bc-4dbe-b21a-7456fccf7380)

說明：  

使用雙層迴圈，**外層迴圈** 控制回合數，**內層迴圈** 控制每一回合的比較次數  

**外層迴圈** 比較到最後一個數字( $n$ )才停止，因為要檢查整個陣列  
**內層迴圈** 從 $(i+1)$ 開始代表比較範圍會隨著已經排序好的數量增加而減少，而 $i$ 以前的範圍則是已排序區  

```cpp
for(int i=0; i<n; i++){
    int min = i;
    for(int j=i+1; j<n; j++){
        if(a[j]<a[min]){
            min=j;
        }
    }
    swap(a[i],a[min]);
}
```







