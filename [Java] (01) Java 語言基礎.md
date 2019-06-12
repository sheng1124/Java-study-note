# [Java] (01) Java 語言基礎
## Program 程式
* 還沒有被載入到記憶體的程式碼
* 編譯過的位元碼 (bytecode) 或是機器碼
## Process 程序
* 載入到記憶體的程式碼，等待或被 CPU 執行的程式碼
* 不同的 Process 共享電腦的資源(硬體)，但不共用，溝通較複雜
* 多工允許兩個以上的 process 同時執行，原理是把 cpu time 分割成 Time Slice 分給不同的 process 用，上一個執行 A process，下次執行 B process，看起來就像同時執行
## Thread 執行緒
* Process 的一部份，為 CPU 分配資源、接受排程的單位，一個 Process 可有多個 Thread
* 不同 Thread 並行執行達到分時多工的效果，其實是透過 CPU 排程，使得程式碼交錯執行看起來像一起執行
* 不同 Thread 可執行在不同的核心上，達到平行加速的效果
* 不同 Thread 共用 Process 的記憶體，溝通有同步問題
* 以 Java SE 為例，應用程式從起始的入口 main 開始執行，這就是主執行緒 (Main Thread)
* 如果程式內沒有創建其他 Thread，則稱為單一執行緒；若是程式內有主動創建 Thread，則稱為多執行緒 (Multithreading)
* Java 的 Thread 由 JVM 管理
## 程式進入點
* 只要是程式都會有第一個執行且唯一的起點
* 即程式進入點
    ```java=
    public static void main(string[] args)
    {
    
    }
    ```
## Java 程式結構
* Java 是物件導向語言
* 當我們要描述一個物件的時候
* 勢必要敘述他的 **屬性** 與 **行為**
    ```java=
    class Puppy
    {
        //屬性
        static String dogType = "拉不拉多";//類別變數
        String dogName = "小黃";//物件變數
        String dogColor = "米黃";
        //行為
        void talk()//物件方法
        {
            System.out.println("汪");
        }
        static void move()//類別方法
        {
        //.....;
        }
        
        Puppy()//建構子
        {
        //....;
        }
    }
    ```
* 完整的 Java 程式結構與對應名稱
    ```java=
    class myClass
    {
        類別屬性、物件屬性
        類別方法()、物件方法()
        建構子()
    }
    ```
* 類別的成員加上 static 修飾元就變成該類別所有物件的共同屬性與方法
## 類別(class)、屬性(attribute)、方法(method)
* 類別
    * 物件的藍圖、集合，ex: "狗"是類別，"小黃"是一個屬於狗的物件
    * 宣告格式
    ``` [存取修飾元] + 宣告類別 + 名稱 + {類別內容與主體}```
    * ex: ```public class HelloWorld {...}```
* 屬性
    * 可稱變數，即類別的與物件的資產
* 方法
    * 類別、物件的行為 
* 類別成員
    * 即屬性和方法
    * 用 '.' 存取類別成員 
## 套件(package) 與 import

* package 機制，它就像是一個管理容器，可以將定義的名稱區隔管理在 package 下，而不會有相互衝突的發生，就像是獨立的個體，類似 c++ 名稱空間
* 使用 "package" 關鍵字來建立 package 以管理我們所定義的類別
    ```java=
    package water;
    public class Fish
    {
        public static String name = "魚";
    }
    ```
    * 待編譯器編譯好之後，會有 water 的資料夾，資料夾底下會有 Fish.class 檔案
* 套件是為了區隔各個套件名稱，但也可以使用不同套件內的類別
    1. 打上路徑: ```套件名稱.類別名稱.類別屬性或方法```
        ex: ```String fishName = water.Fish.name``` ，```water.Fish.name``` 為類別屬性
    2. 透過 import 來定義 ```import 套件名稱```
        ex: ```import water.*``` ， ```String fishName = Fish.name```
    3. classpath(類別路徑)        
* import 即類似 c++ ```#include<>``` + ```using```
* class、package、import 宣告先後順序
    * package -> import -> class
    ```java=
    package water.*;
    import java.io.*;
    class MyTest
    {
    
    }
    ```
* 使用 import 並不會影響效能
## 存取修飾元
* 說明: 存取修飾元(Modifier)是用來宣告 類別、屬性、方法(建構子) 可被存取的權限，分四個等級: private、default(無修飾元)、protected、public
    | 存取修飾元 | 權限說明 |
    | -------- | -------- |
    | private  | 同一個 class 的成員才可以存取|
    | public  | 皆可存取|
    | default  | 同一個 package 可存取，不同類別要繼承|
    | protected | 同一個 class 的成員才可以存取|
    
* 存取修飾元的可視範圍
    | 存取修飾元 | 同一 class | 同一 package 中 |子類別|不同的 package|
    | -------- | -------- | -------- |-|-|
    |private|Yes|-|-|-|
    |default|Yes|Yes|-|-|
    |protected|Yes|Yes|Yes|要有繼承關係|
    |public|Yes|Yes|Yes|Yes|
* 類別(class)只能用 public 與 default 來修飾，寫一個別人宣告不了的物件沒意義，若是內部類別，上述四種可用

## Java 撰寫慣例
* 制定類別(class) 名稱
    * 慣例會將類別名稱的第一個英文字大寫
* 命名屬性
    * Camel-Case(駝峰式命名法)
* 方法
    * Camel-Case(駝峰式命名法)
    * 開頭最好是動詞
## 參考
* Program、Process 和 Thread
    * https://blog.marksylee.com/2016/09/13/java-interview-01-program-process-thread/
###### tags: `Java 學習筆記`
