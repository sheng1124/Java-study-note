# [Java] (15) Java 物件導向-內部類別

## 說明
* 所謂內部類別就是在類別中再定義一個類別，是類別中的類別，可分以下四種
    * 一般內部類別
    * 方法類別
    * 匿名類別
    * 靜態內部類別
* 又稱巢狀類別
* 注意事項
    * 內部類別無法擁有 static 成員，但靜態內部類別除外，可擁有 static 成員
    ![](https://i.imgur.com/rYgrCit.png)


## 一般內部類別
* 直接在類別中所宣告的次類別
* 一個外部類別可以有很多個內部類別
* 一個內部類別可以有很多次內部類別
* 架構
    ```java=
    public class MyOuter1
    {
        class MyInner1
        {
            class MyInnerAgain
            {
                ...
            }
        }
        
        private class MyInner2
        {
            ...
        }
    }
    
    class MyOuter2
    {
        ...
    }
    ```
## 生成內部類別物件
* 說明
    * 對其他類別來說，要使用某個類別的內部類別物件，要先透過外部類別的物件才能用，不可以直接用
    * 建立實體當然必需借 MyOuter 來幫忙
    * 對外部類別而言，內部類別就可以直接用
* 範例
    ```java=
    MyOuter ou = new MyOuter();
    MyOuter.MyInner in = ou.new MyInner();
    in.foo();
    ```
* 範例簡化
    * version 1
    ```java=
    MyOuter.MyInner in = new MyOuter().new MyInner();
    in.foo();
    ```
    * version 2
    ```java=
    new MyOuter().new MyInner().foo();
    ```
### 一般內部類別成員存取關係
* 範例
    ```java=
    class MyOuter
    {
        private static int sx = 9; //static member
        private int x = 7; //member of MyOuter
        
        class MyInner
        {
            private int x = 77; //member of MyInner
            
            public void foo()
            {
                int x = 777; //local 
                
                System.out.println("Local x = " + x);
                System.out.println("MyInner's x = " + this.x);
                System.out.println("MyOuter's x = " + MyOuter.this.x);
                System.out.println("MyOuter's static x = " + MyOuter.sx);
            }
        }
    }
    ```
* 說明
    * 內部類別可透過 外部類別.this 存取外部類別的成員
    * 外部類別.靜態成員 可直接存取
    
## 內部類別的編譯檔名與"$"之間的關係
* 類別再被編譯的時候，都會被編譯為一個 .class 檔
* 一個 .java 源碼可能會編譯出很多個 .class 檔，多個外部類別或內部類別
* 因此會透過 "$" 去表示類別的層次關係
* 以上例 MyOuter1 會編譯成 ```MyOuter.class``` ， ```MyOuter2 => MyOuter2.class``` ， ```MyInner1 => MyOuter1$MyInner1.class``` ， ```MyInnerAgain => MyOuter1$MyInner1$MyInnerAgain.class```

## 方法內部類別
* 說明
    * 即在方法中宣告的的類別
    * 若要建立"方法內部類別"物件實體，必須寫在宣告該"方法內部類別"之後
* 範例
    ```java=
    public class MethodInnerClass
    {
        void see()
        {
            //宣告 方法內部類別 MyInner
            class MyInner
            {
                void foo()
                {
                    System.out.println("Hello");
                }
            }
            //宣告結束
            
            //建立實體
            MyInner mi = new MyInner();
            mi.foo();
        }
    }
    ```
    * 編譯後方法內部類別的檔名是 MethodInnerClass$1MyInner.class
    * 其中1是流水序號


## 匿名內部類別(重要) Anonymous inner class
* 說明
    * 當需要繼承或實作某個介面並建立實體的需求時，通常這些"子類別"只會使用到一次，所以為了方便，可以不需要定義名稱，這就是匿名內部類別
    * 適用只在程式中用到一次，之後就不需再次使用的類別
    * 即沒有宣告名稱的類別，以 {...} 實作
    * 從JDK8開始，若介面僅定義一個抽象方法，可以使用Lambda來簡化這個程式的撰寫
* 範例
    * 實作介面 格式: ```new ClassName() {...};```
    ```java=
    interface Pet
    {
        String attr = "cute";
        void skill();
        void move();
    }
    
    public class AnonymousClass
    {
        public static void main(String[] args)
        {
            Pet P = new Pet()
            {
                public void skill()
                {
                    System.out.println("aaa");
                }
                public void move()
                {
                    System.out.println("run");
                }
            };//要加分號
            
            p.skill();
            p.move();
        }
    }
    ```
    * 當介面只有定義一個抽象方法時，可用 Lambda 來簡化
    ```java=
    Some s = () ->
    {
        System.out.println("run");
    };
    ```
* 匿名類別實體檔名
    * 因為匿名類別沒有類別名稱，所以檔名會是
    * 外部類別名稱$流水序號(1,2~,n)
    * ex: AnonymousClass.class 、 AnonymousClass$1.class
* 匿名多型的問題
    * 匿名類別的實作可以創造並實作自己的方法，語法上沒問題
    * 若上個範例修改
    ```java=
    ...
    {
        ...
        public void sound()
        {
            Systm.out.println("喵");
        }
    }
    ...
    ```
    * 語法上沒問題，但使用上看待 p 的物件的資料型別是 Pet 類別，即匿名類別的父類別
    * 在 Pet 類沒有定義 sound() 方法，所以 p 物件在 Pet 的資料型別上無法使用 sound() 方法
    * 若要使用，就要先轉型，轉成 p 物件匿名類別的型別才能用，但是轉型需要知道該類別的名子為何
    
## 靜態內部類別
* 說明
    * 靜態類別是在宣告類別時加上了 static 的關鍵字
    * 使其物件實體配置在記憶體的 Global 區塊中，而不是在 Heap 中，因此又稱頂層類別
    ![](https://i.imgur.com/d0nnBlU.png)
    * 內部靜態類別就如同 static 變數一樣，他只屬於某一個類別，並不是類別中的實體
    * 靜態內部類別本身並沒有指到外部類別的 this 指標，但非 static 成員仍有 this 指標指向靜態內部自己的類別
    * 靜態內部類別是唯一可以擁有 static 、 non-static 成員的內部類別
    * 外部類別的 static 也被宣告在 global 裡，所以可以互相看見並存取
    * 靜態內部類別可建立實體
* 範例
    ```java=
    class MyOuterClass
    {
        static class StaticInnerClass
        {
            public void fooA(){...}
            
            public static void fooB(){...}
        }
    }
    ```

###### tags: `Java 學習筆記`
