# [Java] (16) Java final 關鍵字

## final 關鍵字
* 說明
    * 用來修飾類別、方法、屬性、區域變數
* 修飾類別
    * 表示該類別不可再被繼承
* 修飾方法
    * 表示該方法不能讓子類別覆寫，可以呼叫不能覆寫
* 修飾屬性/變數
    * 類似 c++ 的 const 修飾字
    * 表示該屬性/變數經定義就不可以再被更改，使用之前要有初值
    * 若物件屬性沒有在宣告的時候設定初值，則必須再透過建構子初始化
    * 在建構子或方法中可用 blank final variable，即變數宣告時不用設定初值，但使用上必須要經過初始化
    ```java=
    class FinalSample
    {
        FinalSample()
        {
            final int val;
            val = 6;
        }
        void method1()
        {
            final int val;
            val = 7;
        }
    }
    ```

* 小細節
    * interface 的屬性都會被強制修飾成 final ，所以無法更改該屬性


###### tags: `Java 學習筆記`
