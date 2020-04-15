# [Java] (09) Java 物件導向-繼承 (this、super)
## 繼承
* 所謂繼承是指類別物件的資源可以延伸和重複使用
* 子 is a 父
* 延伸類別的存取範圍必須受限於父類別的存取修飾字
* 語法
    ```[子類別宣告] + extends + [父類別名稱]```
* 父類別又稱超類別(super class)或基礎類別
* 子類別又稱擴充類別
    ```java=
    class Father
    {
        //...
    }
    
    class Son extends Father
    {
        //...
    }
    ```

## 繼承關係下的建構子
* 預設建構式的執行順序
    * 爺 -> 父 -> 子
* 當子類別建構時，預設會呼叫父類別的預設建構子
    * 先建構父類別再建構子類別
    * 即在子類別的建構子第一行加上 super(); 也就是呼叫父類別的無帶參數建構子
    ```java=
    class Son extends Father
    {
        Son()
        {
            super(); //呼叫 Father 類的預設建構子
        }
    }
    ```
* 若父類別的建構子是帶有參數的
    ```java=
    class Father
    {
        protected String name_;
        Father(String name)
        {
            name_ = name;
        }
    }
    
    class Son extends Father
    {
        Son()
        {
            System.out.println(name_);
        }
    }
    
    public class Ex
    {
        public static void main(String[] args)
        {
            Son aa = new Son(); //error
        }
    }
    ```
    * 將會編譯錯誤
    ![](https://i.imgur.com/Te4OAl1.png)
* 解決帶父類別建構子帶參數的情形
    1. 直接在父類別實作無帶參數的建構子
    2. 在子類別上，用 super() 呼叫父類別有帶參數的建構子
    ```java=
    class Father
    {
        protected String name_;
        Father(String name)
        {
            name_ = name;
        }
    }
    
    class Son extends Father
    {
        Son()
        {
            super("default");
            System.out.println(name_);
        }
        Son(String s)
        {
            super(s);
            System.out.println(name_);
        }
    }
    
    public class Ex
    {
        public static void main(String[] args)
        {
            Son aa = new Son();
            Son bb = new Son("bb");
        }
    }
    ```
## This 、 super 關鍵字
* this
    * this 是一個參考(Reference)，在C++是指標
    * this 參考到目前程式執行中的物件
    * 就是自己本身
* super
    * super 是參考到子物件的父物件的範圍
    * 也就是說使用父物件本身繼承過來的 屬性、方法、建構子
    * 必須在繼承關係的運作下才有意義
    * super([引數串列]) 呼叫父類別建構式
    * super.data 存取父類別的資料成員
    * super.method([引數串列]) 呼叫父類別方法
* 應用
    ```java=
    class Father
    {
        public void talk
        {
            Sysytem.out.println("father");
        }
    }
    
    class Son extends Father
    {
        private int money;
        
        public void getMoney(int money)
        {
            this.money += money;
        }
        
        public void talk()
        {
            System.out.println("son");
        }
        
        public void go()
        {
            this.talk();
            super.talk();
        }
    }
    ```
* 注意事項
    * 避免同時呼叫 this()、super() 建構子在同一個函式或建構子區塊中
    * static 成員中並沒有 this 、 super 的參照，不可以在 static 成員中使用
        * static 並非真正的物件
###### tags: `Java 學習筆記`
