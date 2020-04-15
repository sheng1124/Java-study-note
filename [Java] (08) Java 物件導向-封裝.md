# [Java] (08) Java 物件導向-封裝
## 封裝
* 封裝是物件狀態的隱藏過程
* 將類別內部的屬性和方法包裝起來
* 外部需要透過介面來取得內部的資料
## 存取權限、存取修飾元
* 說明: 存取修飾元(Modifier)是用來宣告 類別、屬性、方法(建構子) 可被存取的權限，分四個等級: private、default(無修飾元)、protected、public
    | 存取修飾元 | 權限說明 |
    | -------- | -------- |
    | public  | 皆可存取|
    | default  | 同一個 package 可存取，不同類別要繼承|
    | protected | 同一個 class 的成員才可以存取|
    | private  | 同一個 class 的成員才可以存取|
    
* 存取修飾元的可視範圍
    | 存取修飾元 | 同一 class | 同一 package 中 |子類別|不同的 package|
    | -------- | -------- | -------- |-|-|
    |private|Yes|-|-|-|
    |default|Yes|Yes|-|-|
    |protected|Yes|Yes|Yes|要有繼承關係|
    |public|Yes|Yes|Yes|Yes|
* 類別(class)只能用 public 與 default 來修飾，寫一個別人宣告不了的物件沒意義，若是內部類別，上述四種可用

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
###### tags: `Java 學習筆記`
