# [Java] (02) Java 資料型別、陣列

## Java 中的資料型態
* Primitive Type (基本資料型態)
    * 共 8 種：int、short、long、byte、float、double、boolean、char
    * 通過如 ```int a = 3; long b = 123L;```的方式宣告
    * 程式碼區塊執行完就扔掉(生命週期有限)
    * 運算速度快，但長度與內容受限
* Class Type(類別型態) / Reference Type(參考型態)
    * 其他大都屬於此類別，如 Integer、String、Long 以及**自行定義的類別**
    * 相似 C 的指標
    * 都需要用 new 去創建，如 ```User user = new User("Mark");```
    * 動態配置，生命週期未知

## 記憶體的儲存空間配置( JVM 記憶體管理)
* Global 儲存媒體
    * 存 Static 的類別成員變數
* Stack 儲存媒體
    * Stack 是用來儲存函數路徑及區域變數
    * 內容為 Primitive Type、Reference Type(物件的位址)
    * 當有新的物件產生時，Heap 會建立該物件，則會產生指到該物件的位址的變數，存到 Stack
    ![](https://i.imgur.com/EI4GyDN.png)
    * 每一個 Thread 都擁有自己的 Stack
* Heap 儲存媒體
    * 存放物件的實體，Reference Type 指到的內容
    * 當宣告一個 Reference Type ，將會把該變數存到Stack，此時沒有內容
    * 用 new 產生一個物件的實體大小，**將會把該物件存到 Heap**，剛剛宣告的 Reference Type 會指到該物件
* Stack 和 Heap 是 JVM 記憶體儲存資料或指令的區域，和其他同名的東西無關

## 基本資料型別 分類
* 分為四類
    | 資料類別 | 資料型態 | 位元組數 |初始值 |資料範圍|
    | -------- | -------- | -------- |- |-|
    | 字元     | char(Unicode)| 2    |'\u0000' |'\u0000' ~ '\uFFFF'|
    | 整數    | byte| 1    |0 |-128 ~ 127|
    | 整數    | short| 2    |0 |-32768 ~ 32767|
    | 整數    | int| 4    |0 |-2^31 ~ 2^31-1|
    | 整數    | long| 8    |0L |-2^63 ~ 2^63-1|
    |浮點數   |float|4|0.0F|-3.4E+38 ~ 3.4E+38|
    |浮點數   |double|8|0.0D|-1.7E+308 ~ 1.7E+308|
    |布林值   |boolean|1|false|true 或 false|
* 備註
    * 系統會給初始值，不用擔心其初值不穩定
    * char 可用 ASCII
    ```java=
    char c5 = 65;//ASCII(65) => A
    ```
    * boolean 只能是 true 或 false
    ```java=
    boolean b1 = 0; //Compiler error
    ```
## 基本資料型別的資料轉換
* 隱含式的轉換(Implicit Casting)
    * 小轉大，以較小的資料放到較大的資料中
    * 無風險，系統會自動轉型
* 強行式的轉換(Explicit Casting)
    * 大轉小，以較大的資料放到較小的資料中
    * 風險大，需要在系統中指定
    * 原則上是切割資料
* 範例
    ```java=
    int i = 1;
    double d;
    d = i; //Implicit Casting
    
    i = d; //error
    i = (int)d; //Explicit Casting
    
    float f; 
    f = 2.5; //error
    f = (double)2.5; //Explicit Casting
    f = 2.5f; //Explicit Casting ， f 是轉型字元
    ```
    * 整數的 hard-coded 預設是 int
    * 浮點數的 hard-codde 預設是 double
## Java 參考資料型別
* Primitive Type 以外的資料型別都是 Reference Type ex: 陣列、字串、自定義類別
### 陣列
* 陣列宣告
    ```java=
    int[] i;
    int i[];
    int [] i;
    int []i;
    
    String[] s;
    String s[];
    String [] s;
    String []s;
    ```
* 宣告之後需要用 new 來產生物件實體
    ```java=
    int[] i = new int[5];
    int[] j = new int[ ]{1, 2, 3, 4, 5};
    int[] k = {1, 2, 2, 4, 5};
    int[] l = new int[5]{1, 2, 3, 4, 5}; //不合法的初值宣告，被宣告的陣列物件會優先以{}內元素個數來配置記憶體空間
    ```
    * new 之後會自動設定初始值， int 初始值為 0
    * 手動設定初值: ```{初值1,初值2}```
* 修改內容
    * ```[]``` 為索引運算子(indexing operator)，用來指向陣列物件中每個元素
    ```java=
    i[0] = 5;
    i[1] = 6;
    ```
### 多維陣列
* 在 Java 多維陣列可分為對稱型陣列、非對稱型陣列，即陣列中的陣列
* 對稱型陣列(Rectangular)
    ```java=
    int[][] x = new int[2][3]; //2x3
    int[][] y = { {1, 2, 3}, {4, 5, 6} }; //2x3
    ```
* 非對稱型陣列(Non-Rectangular)
    ```java=
    int[][] x = new int[2][];
    x[0] = new int[3];
    x[1] = new int[1]; // x == {{0,0,0},{0}}
    int[][] y = { {1, 2, 3}, {4, 5} };
    ```
* 陣列宣告是從左至右的方式初始陣列大小
    ```java=
    int[][] m1 = new int[2][]; //合法
    int[][] m2 = new int[][3]; //不合法
    ```
* 陣列 Resize
    * 在 Java 中，產生的陣列不能重新定義大小
    * 若用 new 重新產生陣列，原來的陣列仍在 heap 中，物件將參考至新的陣列
    * 舊的物件將會被資源回收機制 Garbage Collection 所回收
### 字串
* Strings 為一個 Reference Type，實際上是 char 陣列
* Strings 和 char 比較
    | 比較項目 | Strings | Char |
    | -------- | -------- | -------- |
    | 資料型別     |  Reference Type    |  Primitive Type    |
    | 表示方式     |  "雙引號"    |  '單引號'    |
    | 抽象表現     |  類別    |  16 bit unicode    |
    |比較運算|equals()|==|
    |內容是否可變|不可變|可變|
* String 的 == 比較運算是比較兩者存在 stack 的位址
    ```java=
    String s1 = new String("Java");
    String s2 = new String("Java");
    
    s1 == s2; //return false
    
    String s3 = "Java"; //String Literal
    String s4 = "Java"; //String Literal
    
    s3 == s4; //return true
    ```
* String new 宣告
    * 一般宣告會各自在 heap 中擷取一塊記憶體來存放字串內容
    * 參考的位置一定不同
    ```java=
    String s1 = new String("Java");
    String s2 = new String("Java");
    ```
    ![](https://i.imgur.com/Ef4LOJT.png)

* String Literal 宣告
    * 為了提升 String 的使用效率，在 Heap 中為 String 物件建造一個虛擬的 String pool 來存放 String ，放在 String pool 中的物件是可以共用的
    * 用 String pool 的方式宣告 String ，所建立的實體會被放在 String pool 中
    * 如果宣告的字串內容已在 String pool ，會參考到同一個位址
    ```java=
    String s1 = "Java"; //String Literal 宣告
    String s2 = "Java"; // s1、s2 參考到一樣的位址
    ```
    ![](https://i.imgur.com/kWvv8bR.png)
* String 的內容是不可變的
    * 當字串再記憶體中被建立，該記憶體的內容就不允許被改變
    ```java=
    String s1 = "java";
    String s2 = "java";
    s1 == s2; //True
    s1 = s1 + "SCJP";
    s1 == s2; //False
    ```
    ![](https://i.imgur.com/SmsYtSB.png)



## 參考資料
* Java 中的資料型態
    * https://blog.marksylee.com/2016/09/14/java-interview-02-jvm-stack-heap/
###### tags: `Java 學習筆記`
