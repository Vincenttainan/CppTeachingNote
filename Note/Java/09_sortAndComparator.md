# **Java 筆記**  
## 內建排序與自訂排序 sortAndComparator  

### `Arrays.sort()`  

`Arrays.sort()` 是 Java 標準庫提供的排序方法  
適用於 **基本型別陣列** 和 **物件陣列**  

#### 排序基本型別陣列  

```java
public class SortExample{
    public static void main(String[] args){
        int[] numbers={5, 2, 8, 1, 3};
        Arrays.sort(numbers);
        System.out.println(Arrays.toString(numbers));
         // [1, 2, 3, 5, 8]
    }
}
```

`Arrays.sort()` 使用 快速排序(Dual-Pivot Quicksort) 或 TimSort  
視情況選擇最佳演算法  

#### 排序物件陣列  

```java
public class SortStringArray{
    public static void main(String[] args){
        String[] words={"banana", "apple", "cherry"};
        Arrays.sort(words);
        System.out.println(Arrays.toString(words));
        // [apple, banana, cherry]
    }
}
```

對於 String 陣列  
預設是依 **字母順序**(Lexicographical Order)來排序  

### `Comparator`  

#### 使用 `Comparator` 排序物件  

排序非基本型別的物件時  
必須使用 `Comparator` 來指定排序邏輯  

```java
class Person{
    String name;
    int age;
    
    public Person(String name, int age){
        this.name=name;
        this.age=age;
    }
    
    @Override
    public String toString(){
        return name+" ("+age+")";
    }
}

public class ComparatorExample{
    public static void main(String[] args){
        List<Person> people=new ArrayList<>();
        people.add(new Person("Alice", 25));
        people.add(new Person("Bob", 30));
        people.add(new Person("Charlie", 20));
        
        people.sort(Comparator.comparingInt(p->p.age));
        System.out.println(people);
        // [Charlie (20), Alice (25), Bob (30)]
        
        people.sort(Comparator.comparingInt((Person p)->p.age).reversed());
        System.out.println(people);
        // [Bob (30), Alice (25), Charlie (20)]
    }
}
```

#### 排序 `String` 陣列  

```java
public class SortByStringLength{
    public static void main(String[] args){
        String[] words={"apple", "banana", "kiwi", "cherry"};
        
        Arrays.sort(words, Comparator.comparingInt(String::length));
        System.out.println(Arrays.toString(words));
        // [kiwi, apple, cherry, banana]
        
        Arrays.sort(words, Comparator.comparingInt(String::length).reversed());
        System.out.println(Arrays.toString(words));
        // [banana, cherry, apple, kiwi]
    }
}
```

### `Collections.sort()`  

`Collections.sort()` 與 `Arrays.sort()` 類似，但適用於 `List`  

```java
public class SortListExample{
    public static void main(String[] args){
        List<Integer> numbers=Arrays.asList(5, 2, 8, 1, 3);
        Collections.sort(numbers);
        System.out.println(numbers);
        // [1, 2, 3, 5, 8]
    }
}
```

如果要降序排序，可以使用 `Comparator.reverseOrder()`  

```java
Collections.sort(numbers, Comparator.reverseOrder());
```

或者直接使用 `List.sort()`：  

```java
numbers.sort(Comparator.reverseOrder());
```

### 總結  



## 總結  

| **方法**               | **適用範圍**                          | **主要用途**                            |  
|----------------------|--------------------------------|--------------------------------|  
| `Arrays.sort()`      | 陣列 (`int[]`, `String[]`, `Object[]`) | 排序基本型別或物件陣列               |  
| `Collections.sort()` | `List<T>`                      | 排序 `List` (可配合 `Comparator`) |  
| `List.sort()`        | `List<T>`                      | 直接使用 `Comparator` 來排序 `List`  |  
| `Comparator.comparing()` | `List<T>` / 陣列                 | 自訂比較方式 (ex: 依數值大小、字串長度) |  
