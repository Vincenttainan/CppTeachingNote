# **Java 筆記**  
## 陣列與字串 array And String  

這邊將會介紹兩個重要的結構：  
1. 陣列 `array[]`  
2. 字串 `String`  

## 1. 陣列 `array[]`  

### 陣列的宣告與初始化  

Java 陣列的語法宣告方式如下：  

```java
int[] a={1,2,3,4,5};   // 宣告並初始化

int[] b=new int[5];    // 宣告
```

### 存取陣列元素  

Java 元素的索引一樣是從 `0` 開始  

## 2. 字串 `String`  

### 字串的宣告與初始化  

```java
String str1 = "Hello";                // 在字串池中內存放字串
String str2 = new String("Hello");    // 強制建立一個字串物件
```

|     操作     |                 方法                  |
|:------------:|:-------------------------------------:|
| 取得字串長度 |            `str.length()`             |
|   字串串接   | `str1 + str2` 或 `str1.concat(str2)`  |
| 取得特定字元 |          `str.charAt(index)`          |
|   字串切割   |           `str.split(" ")`            |
|  轉換大小寫  |`str.toUpperCase()` / `str.toLowerCase()`|
| 檢查是否相等 |          `str1.equals(str2)`          |
|  擷取子字串  |      `str.substring(start, end)`      |

## 範例  

### 程式碼  
```java
String str="Vincenttainan";
System.out.println(str.length());
System.out.println(str.toUpperCase());
System.out.println(str.substring(0,7));
```

### 輸出  
```
13
VINCENTTAINAN
Vincent
```

## 注意  

### 字串與字串物件  

1. 字串  

```java
String str1 = "Hello";
```

這種方式使用字串池（String Pool） 來管理字串：  

* 字串池是 Java 內建的一塊記憶體空間，專門儲存字面值字串（被 `""` 包起來的字串）  
* 如果該字串已存在於字串池中，則會共用該物件  
* 效能較佳，因為 Java 會自動幫助重複利用相同的字串物件  

2. 字串物件  

```java
String str2 = new String("Hello");
```

這種方式則強制建立一個新的 `String` 物件：  

* 不使用字串池，而是在 Heap（堆區記憶體） 中建立 `String` 物件  
* 即使字串池裡已經存在了，這個 `new` 方式依然會產生一個新的物件  
* 這會造成額外的記憶體開銷，因此不建議使用，除非需要一個新的 `String` 物件  

### 字串內容物相等  

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");
String str4 = new String("Hello");
```

這邊使用兩種方式創建字串  

#### 程式碼  
```java
System.out.println(str1==str2);
System.out.println(str1==str3);
System.out.println(str3==str4);
```

#### 輸出  
```java
true
false
false
```

這邊使用 `==` 來比較兩字串  
但因為 `==` 在 Java 中只會比較兩者的記憶體位置  

* `str1==str2`：  
    這裡因為 `str1` 和 `str2` 都存在在字串池內，指向相同的物件  
    所以輸出為 `true`  
* `str1==str3`：  
    因為 `str3` 是 `new` 創建出來的，所以與 `str1` 記憶體位置不同  
    所以輸出為 `false`  
* `str3==str4`：  
    因為 `str3` 和 `str4` 都是 `new` 創建出來的，所以記憶體位置皆不同  
    所以輸出為 `false`  

#### 程式碼  
```java
System.out.println(str1.equals(str2));
System.out.println(str1.equals(str3));
System.out.println(str3.equals(str4));
```

#### 輸出  
```java
true
true
true
```

這邊使用 `.equals()` 來比較兩字串  
而因為 `.equals()` 會直接比較兩者內容是否相同  
所以三者皆會輸出 `true`  

### 字串取值改值  

在 Java 中，String 是不可變的  
所以取值改值都要特別處理  

#### 取值  

不能使用 `str[0]` 來直接存取單個字元  
必須使用 `str.charAt(index)` 方法來存取  

```java
String str="Vincenttainan";
System.out.println(str.charAt(0));
```

這是因為 Java 的 `String` 不是陣列，而是物件  
所以不能用 `[]` 存取字元  

#### 改值  

`String` 沒辦法改值  
要改成 `StringBuilder` 才可以使用  

```java
StringBuilder str=new StringBuilder("Vincenttainan");
str.setCharAt(0,'v');
System.out.println(str);
```
