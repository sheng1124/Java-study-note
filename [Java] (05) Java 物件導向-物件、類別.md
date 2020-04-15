# [Java] (05) Java 物件導向-物件、類別
## 好的設計有哪些?
* 一個好的設計有以下優點：
    1.Testing. (容易測試)
    2.Porting. (容易移植到其他平台)
    3.Maintenance (容易後續維護)
    4.Extension (容易增加新功能)
    5.Reorganization (容易重新組織)
    6.Understanding (容易了解的程式碼)
## 程序導向(Procedure-oriented Programming)
* 傳統的程式設計思維
* 將資料和處裡方法分開思考，用功能性去區別不同的函式
    ![](https://i.imgur.com/2HEZ0lI.png)
* 用『功能』來切程式，最後再由一個 main() 來統一管理
* 資料、方法關聯性高，不適合獨立設計
* 新增一個不同性質的資料，可能所有的函式、流程要為了這個資料重寫 
    * ex:新增一個 vip 帳戶，deposit() 需提供一些優惠，所以須"改" if(...)...;
    * 需常常修改 => 維護更不容易
* 當程式規模越大，當需求增加、變更修改，維護越不容易，牽一髮而動全身

## 物件導向(Object-oriented programming)
* 將資料與處裡方法一起思考並封裝成一個獨立的物體
* 用『物件』來切程式，各個物件自動自發的負責自己的『功能』，不需 main() 管理。
* 各個物件、主程式之間必須透過抽象介面溝通
    * 各個物件之間無法直接存取對方資料，彼此獨立
* 物件導向設計的目的是為了減少需求改變所造成的影響
* 物件導向就是希望當你有新的需求時，可以不必去更改原來的程式，只要繼續新增你的需求即可，不用更改原來的程式，就不會有維護的問題
* 物件導向怎麼做到不用更改原來的程式的?就是靠『多型』，所以物件的『多型』才是物件導向的精隨，所以同一個程式，只要其所能處理的物件屬於同一個繼承體系，則不須修改程式就能正常執行
    ![](https://i.imgur.com/0uXrwL8.png)
* 解釋何謂物件導向程式設計
    * 物件導向設計是一個程式的設計架構，傳統上的程式架構是採用結構化的處裡流程，即所有的資料處理都是由主程式負責，若是新增不同性質的資料，相關的資料處理函式可能都要因為這個新的性質，需要修改或重寫，就要更動到原本設計好的函式，分工也會很模糊，當程式規模越大，需求改變或增加，維護、更新越不容易，很容易因為牽一髮而動全身。
    * 物件導向就是一種新的寫程式的思考模式，它將資料和處理方法封裝成一個獨立的物體，在主程式、其他物件之間都需要透過抽象介面去操作物件、影響物件內容，而不是直接存取物件的內容，這樣就可以避免在介面之外直接變更到物件的內容，彼此之間就會各自獨立，這樣的目的是為了減少當需求改變所造成的影響，避免因為改變而更動其他設計好的程式碼，即使當需要新增功能時，我們也可以透過繼承、多型的方式去新增額外的物件或功能，盡量去減少改變原本的程式碼，在維護上會比傳統上輕鬆，分工也可以很明確。

## 類別 Class
* 何謂 Class
    * 類別是物件的模板、藍圖，是靜態沒有實體(instance)的概念
    * 類別定義了物件的資料型態，如屬性、方法
* 物件
    * 即類別的實體
    * 是真實存在於記憶體的實體，它是動態的，會隨時間改變狀態或消失
    * 架構和行為不變

## 類別宣告
* 一個 .java 可以有多個類別(default)，但在 .java 檔中只能宣告一個 public 的類別
* 且主類別名稱必須與檔名相同
    ```java=
    //Myclass.java 類別定義
    public class Myclass //主類別 
    {
        public static void main(String[] args)
        {
        //...
        }
    }
    
    class defaultMyclass
    {
    
    }
    
    /* error: class MyclassB is public, should be declared in a file named MyclassB.java
    public class MyclassB
    {
        //...
    }
    */
    ```
## 屬性
* 類別屬性
    * 用 static 去修飾的變數
    * static 變數是指，屬於同一類別物件的共同變數，即類別屬性
    * 程式執行時就存在
* 物件屬性
    * 沒有 static 修飾的變數
    * 各個物件獨自擁有的變數即物件屬性
    * 在生成物件之前不存在
## 方法
* 類別方法
    * 用 static 去修飾的方法
    * 類別方法即是具有名稱空間的函式
    * 程式可以直接呼叫類別方法，而不透過產生物件來呼叫方法
    ```java=
    public class Myclass
    {
        public static main()
        {
            //....
        }
    }
    ```
* 物件方法
    * 沒有 static 修飾的方法
    * 描述物件的行為，也是外部存取物件內部資料的方法
    * 即物件的介面
## Static 成員、 non-Static 成員
* static 成員就是類別屬性、類別方法
    * static 僅可以直接存取 static 成員，若要存取 non-static 必須創建物件才行
    * 在 static 成員中根本沒有隱含的 this 參考指標指向物件，不能呼叫物件方法
* non-static 成員就是物件屬性、物件方法
    * non-static 可以直接存取 static、non-static 成員
    * non-static 成員必須先有物件，才能夠存取物件的成員
## 建立物件實體
* 宣告、定義
    ```java=
    //類別名稱 變數名稱 = new 類別名稱(建構子)
    public class Test
    {
        String s = "hello";
        public static void main(String[] args)
        {
            Test t = newTest();
            System.out.println(t.s);
        }
    }
    ```
    * 用 new 來配置一個實體的記憶體空間給物件
    * new 會回傳一個參考值，以便指定給相對應物件變數
## 存取物件內容
* . 運算子
    * 用 物件.屬性 、物件.方法() 去存取
* 物件方法一定要用 . 存取 
## this
* this 即物件自己本身
    * 在物件方法中，因為沒有唯一的物件名稱，不知如何存取物件本身其他的物件方法
    * 即有一個 this 變數指到物件本身
    ```java=
    class Persion
    {
        private int age;
        public void SetAge(int age) // same name
        {
            this.age = age;
        }
    }
    ```
## 參考資料
* 程序導向和物件導向的思維主要區別在哪裡? (OO)
    * https://www.cnblogs.com/oomusou/archive/2007/04/24/724963.html
* 什麼是物件導向(Object Oriented)? (OO) (C/C++) (.NET) (C#) (Database) (Visual FoxPro)
    * https://www.cnblogs.com/oomusou/archive/2007/01/13/619310.html
* 每週10道Java面試題：物件導向, 類載入器, JDBC, Spring 基礎概念 原文網址
    * https://itw01.com/YY2V3E6.html 
* 物件導向基礎：何謂類別(Class)？何謂物件(Object)？
    * https://blog.miniasp.com/post/2009/08/27/OOP-Basis-What-is-class-and-object
* 面試 Interview 考題 test part 1
    * http://wcodominique.blogspot.com/2014/02/interview-test-part-1.html  
###### tags: `Java 學習筆記`
