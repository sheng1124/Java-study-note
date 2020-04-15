# [Java] (12) Java 物件導向-介面(interface)
## 介面(interface)
* 前言
    * 一個子類別為何只能繼承一個父類別(in Java)?
    * 難道不能再繼承另一個父類別嗎?
    * 為了要達到這種可多重繼承的機制，必須透過介面(interface)來實現
* 說明
    * 介面是類別的一種，他是用戶端與類別之間的溝通管道，用戶端可以是很多種，但類別的介面就一種
    * 相同的介面可讓程式撰寫有一定規範可循，對外可讓很多類別使用，彼此之間不用任何關聯，只要遵循相同界面的規範即可
    * 因此介面的使用特性和抽象(Abstract)類別很相似，介面要求使用(implements)的類別必須實作指定的方法，不同的類別就可以透過相同的介面來溝通(彼此都知道這個方法需要那些參數、回傳什麼，儘管實作內容不一樣)
    * Java 的類別只能繼承一個爸爸，但可以實作多個介面
* 注意事項
    * 介面不可以繼承一般類別，一般類別不可繼承介面
    * 介面的存取權限只能是 default、public，內部介面無此限制
    * 介面內的成員在編譯時，會加上型態敘述如下
    * 介面屬性必須自行給定初始值，介面屬性型態為 public static final
    * 介面方法不可以實作，必須用分號結束宣告，介面方法型態為 public abstract
    * (PS)Java 中的方法若沒有實做內容必須要用 abstract 來修飾，但在介面裡編譯時會加入，所以不用加 abstract 修飾
* 介面的定義
    * 要定義介面時，必須使用保留字 interface
    ```java=
    public interface A
    {
        void doA();
    }
    ```

## 介面與抽象類別的不同
1. 資料成員與方法成員的不同
    * 抽象類別的內容至少要有一個抽象方法，不過可允許一般的方法
    * **介面不允許擁有一般的方法**
    * 介面定義在編譯時，就會把所有方法變成 public abstract 的型態，屬性則為 public static final 的型態
    * 因此介面的方法宣告必須為 public
    
2. 階層關係的不同
    * 不同層級(爺、父、子)的類別可以實作相同的介面
    * 基礎類別不會回過來繼承父類別(繼承自己)，只有子類別會繼承父類別 
3. 效率的不同
    * 介面屬於執行期的動態查詢，比較沒效率

## 介面的多重繼承
* 說明
    * Java 中的一般類別不能多重繼承
    * 但是介面可以多重繼承 **多個介面**
    * 介面不可以繼承一般類別，一般類別不可繼承介面
* 範例
    ```java=
    介面 extends 介面類別1, 介面類別2, 介面類別3...
    ```
## 範例
* 
    ```java=
    interface A
    {
        public void doA();
    }

    interface B
    {
        public void doB();
    }

    interface C extends A, B
    {
        public void doC();
    }

    class Father implements A, B
    {
        public void doA()
        {
            System.out.println("father A");
        }
    
        public void doB()
        {
            System.out.println("father B");
        }
    }

    class Son extends Father
    {
        public void doA() //override
        {
            System.out.println("son A");
        }
    }

    class GrandSon extends Son implements C
    {
        public void doC()
        {
            System.out.println("grandSon C");
        }
    }

    class Girl implements C
    {
        public void doA()
        {
            System.out.println("girl A");
        }
    
        public void doB()
        {
            System.out.println("girl B");
        }
    
        public void doC()
        {
            System.out.println("gril C");
        }
    }
    
    ```
* 圖解
    ![](https://i.imgur.com/KQu4BmD.png)

###### tags: `Java 學習筆記`
