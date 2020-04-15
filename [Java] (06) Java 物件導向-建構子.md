# [Java] (06) Java 物件導向-建構子
## 建構子(Constructor)
* 說明
    * 建構子是物件建立時所執行的函式
    * 即初始化物件的方式
* 特性
    * 沒有回傳值
    * 名稱與類別相同
    * 建構子可以多載
* 語法
    ```java=
    public class Mytest
    {
        int size_;
        public MyTest() //預設建構子
        {
            size_ = 0;
        }
        
        public MyTest(int size)
        {
            size_ = size;
        }
    }
    ```
## 預設建構子(default Constructor)
* 說明
    * 類別一定要有建構子
    * 若程式沒有明確定義建構子，Java 會在編譯期自動加入，加入的就稱之為預設建構子
    * 若給定成員變數初值，就會設為預設建構子的預設值
    * 預設建構子不帶參數列
* 語法
    ```java=
    public class MyTest
    {
        int size_ = 99;
        public MyTest(){ }//=> size_ = 99;
    }
    ```
## 解構子
* 說明
    * java 沒有解構子，取而代之的是回收機制


###### tags: `Java 學習筆記`
