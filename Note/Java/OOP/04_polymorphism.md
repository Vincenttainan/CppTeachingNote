# **Java 筆記**  
## 多型 polymorphism  

### 什麼是多型？  

多型是 OOP 中重要的特性之一  
允許相同的函式或物件  
在不同情境下表現出不同的行為  

多型主要分為兩種：  

1. 編譯時期多型（函式重載 Overloading）  
2. 執行時期多型（函式覆寫 Overriding）  

### 函式重載（Method Overloading）編譯時期多型  

#### 概念：  

同一個類別中，可以有多個同名函式，但參數不同  

#### 條件：  

函式名稱相同，但參數需不同：  
1. 參數數量不同  
2. 參數類型不同  
3. 參數順序不同  

回傳值不同不算函式重載  

#### 範例：  

```java
public class Main {
    public static void main(String[] args) {
        System.out.println(Adder.add(1,2));
        System.out.println(Adder.add(1.1,2.3));
        System.out.println(Adder.add("Vincent","tainan"));
    }
}

public class Adder{
    public static int add(int a,int b){
        return a+b;
    }
    public static double add(double a,double b){
        return a+b;
    }
    public static String add(String a,String b){
        return a+b;
    }
}
```

```
3
3.4
Vincenttainan
```

### 函式覆寫（Method Overriding）執行時期多型  

#### 概念：  

子類別 **覆寫** 父類別 的函式，改變其行為  

#### 條件：  

1. 方法名稱相同  
2. 參數列表相同  
3. 存取權限不能比父類別更嚴格（可以更寬鬆）  
4. 加上 `@Override` 註解（推薦，非強制）  

#### 範例：  

```java
public class Main {
    public static void main(String[] args) {
        Animal anAnimal=new Animal();
        anAnimal.makeSound();
        Dog aDog=new Dog();
        aDog.makeSound();
        Animal anAnimalDog=new Dog();
        // 父類別變數指向子類別物件
        anAnimalDog.makeSound();
    }
}

class Animal{
    void makeSound(){
        System.out.println("Animal's sound");
    }
}

class Dog extends Animal{
    @Override
    void makeSound(){
        System.out.println("Woof, woof");
    }
}
```

```
Animal's sound
Woof, woof
Woof, woof
```

### 父類別與子類別關係  

#### 父類別變數可以指向子類別物件  

這是多型最重要的概念之一  
讓我們可以使用 **父類別變數存取子類別的行為**  
但只能存取父類別內已經定義的成員（除非有覆寫 @Override）  

例如：  

```java
public class Main {
    public static void main(String[] args) {
        Animal anAnimalDog=new Dog();
        // 合法的
        Dog anDogAnimal=new Animal();
        // 不合法的
    }
}

class Animal{
    void makeSound(){
        System.out.println("Animal's sound");
    }
}

class Dog extends Animal{
    @Override
    void makeSound(){
        System.out.println("Woof, woof");
    }
}
```

### 用 `instanceof` 判斷類型  

如果希望確認某個物件的實際類型，可以使用 `instanceof`  

```java
public class Main {
    public static void main(String[] args) {
        Animal anAnimalDog=new Dog();
        if(anAnimalDog instanceof Animal){
            System.out.println("It is an Animal");
        }
        if(anAnimalDog instanceof Dog){
            System.out.println("It is a Dog");
        }
    }
}

class Animal{
    void makeSound(){
        System.out.println("Animal's sound");
    }
}

class Dog extends Animal{
    @Override
    void makeSound(){
        System.out.println("Woof, woof");
    }
}
```

```
It is an Animal
It is a Dog
```

### `super` 關鍵字與多型  

在子類別的覆寫方法中  
如果還是想呼叫父類別的方法，可以用 `super`  

```java
public class Main {
    public static void main(String[] args) {
        Dog aDog=new Dog();
        aDog.makeSound();
    }
}

class Animal{
    void makeSound(){
        System.out.println("Animal's sound");
    }
}

class Dog extends Animal{
    @Override
    void makeSound(){
        super.makeSound();
        System.out.println("Woof, woof");
    }
}
```

```
Animal's sound
Woof, woof
```
