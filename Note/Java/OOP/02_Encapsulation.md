# **Java 筆記**  
## 封裝 encapsulation  

封裝是物件導向程式設計（OOP）中四大特性之一  

1. 封裝  
2. 繼承  
3. 多型  
4. 抽象  

主要目的是保護資料，避免外部直接存取物件內部的屬性  

### 存取控制修飾詞 Access Modifiers  

Java 提供 `private`、`public`、`protected` 控制變數與函式的存取權限  

|   修飾詞    | 同一類別 | 同一 package | 子類別 | 其他類別 |
|:-----------:|:--------:|:------------:|:------:|:--------:|
|  `public`   |   True   |     True     |  True  |   True   |
| `protected` |   True   |     True     |  True  |  False   |
|  `private`  |   True   |    False     | False  |  False   |
| (無修飾詞)  |   True   |     True     | False  |  False   |

1. `public`：公開  
    任何地方都可以存取  
    ```java
    class Person {
        public String name;
    }

    public class Main {
        public static void main(String[] args) {
            Person p=new Person();
            p.name="Vincenttainan";
            System.out.println(p.name);
        }
    }
    ```
    小問題：這種方式不安全，因為外部可以直接改變 `name` 值  
    
2. `private`：私有  
    只有類別內部能存取，外部無法直接修改  
    ```java
    class Person {
        private String name;
    }

    public class Main {
        public static void main(String[] args) {
            Person p=new Person();
            p.name="Vincenttainan";
            // Error：無法直接存取 private 屬性
        }
    }
    ```
    解決方案：使用 `getter` 和 `setter` 方法來存取  
    
3. `protected`：受保護  
    同一個 `package` 內或子類別（`extends`）可以存取，但其他類別不能  
    ```java
    class Person {
        protected String name;
    }

    class Student extends Person {
        public void showName(){
            System.out.println("My name is "+name);
        }
    }

    public class Main {
        public static void main(String[] args) {
            Student s = new Student();
            s.name = "Vincenttainan";
        }
    }

    ```

### `getter` 和 `setter` 方法  

讓 `private` 屬性可以被安全地讀取（`getter`）或修改（`setter`）  

```java
class Person {
    private String name;

    // getter
    public String getName(){
        return name;
    }

    // setter
    public void setName(String name){
        this.name=name;
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.setName("Vincenttainan");
        System.out.println(p.getName());
    }
}
```

#### 為什麼要用 getter/setter？  

1. 封裝資料，不允許直接存取 `private` 屬性  
2. 控制輸入，可以檢查資料是否合法  
3. 擴展性，未來可以加入更多邏輯而不影響原本程式  

### 加入條件驗證  

可以在 `setter` 方法內加上條件判斷，確保輸入合法  

```java
class Person {
    private int age;

    public int getAge(){
        return age;
    }

    public void setAge(int age){
        if(age>0){
            this.age=age;
        }
        else{
            System.out.println("Age needs > 0");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        p.setAge(-5);
        // Not available
        p.setAge(25);
        // Available
    }
}
```

