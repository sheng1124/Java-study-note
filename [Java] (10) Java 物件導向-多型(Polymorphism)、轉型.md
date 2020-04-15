# [Java] (10) Java 物件導向-多型(Polymorphism)、轉型
## 多型(Polymorphism)
* 說明
    * 多型操作指的是使用同一個操作介面，以操作不同的物件實例
    * 在不知道用的是哪種物件的情況下，可用共同的抽象類別去看待，再用介面去執行該物件的行為，而不需要判斷這是哪一種物件並實作特定的方法
        * 鳥、蟲會飛，所以鳥、蟲是一種會飛的生物，包括鳥、蟲，因此會飛的東西就是一種繼承的關係，是鳥、蟲的抽象類別，"飛"是一種籠統的說法，並沒有交代要如何飛，因此飛是一種操作介面，而鳥飛、蟲飛，則需要由鳥、蟲去實現飛行的方式，藉由多型，"這個東西"飛，獲取該要求的物件就會執行各自相應的方法，在不知道是哪種物件的情況，就不需要判斷這個東西是否為鳥，就執行鳥飛...
    * 多型操作在物件導向上是為了降低對操作介面的依賴程度，進而增加程式架構的彈性與可維護性
        * ex 用動物(型別)的觀點看待老虎(實體)，用動物的介面去操作老虎。就可以把要求抽象化，老虎的跑 簡化成 這個動物跑
        ```java=
        Animal a = new Tiger();
        a.run(); // a.tigerRun() => a.run()
        a = new Lion();
        a.run(); // a.lionRun() => a.run()
        ```
    * 當要對不同物件操作時，或不知道是哪個物件要操作，可以直接宣告父類別的型別去看待可能不知道是哪個型別的子物件，就可以做抽象的操作，而不用特別針對每個物件做操作
        ```java=
        public void executeATK(Animal temp)
        {
            temp.attack();
        }
        
        public void demo()
        {
            Bird b = new Bird();
            Tiger t = new Tiger();
            
            executeATK(b);
            executeATK(t);
        }
        ```
    * 物件變數因宣告時的觀點不同，所能操作的資源也不同
    * 程式在執行時會根據不同的物件選擇適當的方法來執行
    * 參考: https://caterpillar.gitbooks.io/javase6tutorial/content/c8_2.html
* 規則
    * 只能用自己的或父層級的觀點去看待實體
    * 即實體必須是參考型別的子類別或是同一個類別
    * 子類別範圍大於父類別，子類別的參考若參考到只有父類別的實體，會因為參考不到內容(範圍太小)，導致編譯錯誤
* 覆寫機制
    * 即程式在執行時會根據不同的物件選擇適當的方法來執行
    * 當執行參考類別的方法時，若實體類別(子類別)有同名的方法，會執行實體物件的方法，即覆寫機制
    ```java=
    Animal a = new Tiger();
    a.move(); // call Tiger's move() methond 
    ```
## 轉型
* 說明
    * 物件變數因宣告時的觀點不同，所能操作的資源也不同
    * 若想暫時改變物件變數的觀點，可以透過轉型來解決
    * 轉型仍會觸發物件本身的覆寫機制，即可能不會呼叫轉型類別的方法
    * 轉型並非改變物件本身的型態，而是改變參考型別的型態
    * 並不會切割物件實體本身，只是更改其參照的指標
* 強制型別轉換
    * 要轉型的目的類別名稱要用小括號圈住，這種寫法叫強制型別轉型
    ```java=
    Animal a = new Tiger();
    a.move();
    ((Tiger)a).skill(); //將 a 的觀點看成 Tiger
    ```
    * 強轉有風險，若轉的型別非同個繼承底下的型別，將會出錯
    ```java=
    Animal a = new Tiger();
    a.move();
    ((Bird)a).skill(); //將 a 的觀點看成 Bird
    ```
    * 仍可以編譯，但會發生物件型別轉換的例外，並崩潰
    ![](https://i.imgur.com/BbD7OcT.png)

* instanceof
    * 為了避免上述問題，有個運算子能在執行期測試能否轉換物件
    * ```物件變數 instanceof 類別名稱```
    * instanceof 的回傳值是 boolean 
    * true  表示該物件可轉型到參考類別
    * false 表示該物件不可以轉型到該參考類別
    ```java=
    if(a instanceof Bird)
    {
        ((Bird)a).move();
    }
    else
    {
        System.out.println("can't change to Bird");
    }
    ```
## 多型與屬性
* 儘管以父類別的角度看子物件，呼叫只有父類別定義的方法，並不會去存取子類別覆寫的同名屬性
* 若子類別覆寫父類別的方法/屬性，以父類別的角度看子物件，存取屬性會存取父類別的，使用方法會觸發子物件的覆寫機制，就會呼叫子類別實作的方法，存取的屬性將會是子類別的屬性
    ```java=
    class Father
    {
        String name = "Father";
        String getName()
        {
            return name;
        }
        String greeting()
        {
            return "class Father";
        }
    }
    
    class Son extends Father
    {
        String name = "Son";
        String greeting()
        {
            return "class son";
        }
    }
    ```
    ```java=
    Father f = new Son();
    System.out.print(f.greeting()); // class son
    System.out.print(f.name); // Father
    System.out.print(f.getName()); // Father
    ```
## 多形與轉型
* 真正實作方法是由物件決定
    ```java=
    this.name; //Son
    super.name; //Father
    
    ((Son)this).name; //Son
    ((Father)this).name; //Father
    
    ((Son)this).greeting(); //class Son
    ((Father)this).greeting(); //class Son
    ```
* 轉型不會影響物件的覆寫機制，即不會改變物件實作的方法
    ```java=
    Son a = new Son();
    System.out.println(((Father)a).greeting()); // class son
    ```
* 轉型 -> 物件呼叫方法 -> 物件方法的覆寫機制 -> 呼叫該方法
## 多型與 static 成員
* 以不同的觀點看待物件，若呼叫、存取類別 static 成員，會以那個參考型別的類別的 static 成員為主
    ```java=
    class A
    {
        static String staticName = "A";
        
        static String staticMethod()
        {
            return "class A";
        }
    }
    
    class B extends A
    {
        static String staticName = "B";
        
        static String staticMethod()
        {
            return "class B";
        }
    }
    ```
    ```java=
    A b = new B();
    System.out.println(b.staticName); //A
    System.out.println(b.staticMethod()); //class A
    ```
## is-a 、 has-a
* is a
    * 是一種上下關係，也就是繼承的關係
    * 老虎是一種動物、電腦是一種電子產品
* has a
    * 有一個，表示類別中的成員變數
    * 電腦有CPU、RAM...
* is a、 has a 關係
    ```java=
    class Machine
    {
        ;
    }
    
    class Computer extends Machine // is a
    {
        CPU theCPU; // has a
        RAM theRAM; // has a
        HD theHD; // has a
    }
    ```
    
###### tags: `Java 學習筆記`
