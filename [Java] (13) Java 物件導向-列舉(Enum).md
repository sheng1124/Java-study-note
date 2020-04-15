# [Java] (13) Java 物件導向-列舉(Enum)

## 列舉(Enum)
* 說明
    * 所謂列舉（Enumeration）型別，就是以關鍵字enum開始加上一個列舉名稱，並以大括號括住要群組管理的常數
    * 大括號中每一個元素稱為列舉元（enumerator），預設上列舉元從第一個開始的實際數值是0，然後依次遞增，透過物件方法 ordinal() 可取得常數物件的序號
    * 在 Java 中無法指定數值，由0依次遞增
    * 宣告列舉之後，您可以用它來指定列舉變數 ```Week x = Week.Sun;```
    * 常數的賦予是透過列舉內的建構子，保存在列舉物件的屬性裡，透過方法存取
    * 列舉元是物件不是基本型別，是列舉自己的型別，不是其他的基本型別、String
    * 其他物件可透過列舉的方法來取用這些列舉元的值
    * 實際上列舉是一種類別，可單獨寫也可當成內部類別
    * 列舉編譯時會加上 final 修飾，所以無法被繼承
    * 用來當作內部類別時，編譯器會自動加上 static、final
    * 列舉元編譯器會加上 public static final
    * public 列舉 .java 要與檔名相同
   
* 語法
    ```java=
    存取修飾字 enum Typename
    {
        Typename物件1, Typename物件2.....
    }
    ```
    * Typename物件1 其內容為 "Typename物件1"，因為 Typename(String s, int i) 建構子
    
* 範例
    ```java=
    enum Week
    {
        Sunday, Monday, Tuesday, Wednesday, Tursday, Firday, Saturday 
    }
    
    public class Test
    {
        public static void main(String[] args)
        {
            System.out.println(Week.Sunday); //輸出 Sunday，直接存取 Week類別屬性，其內容就是物件的名子
            
            Week test = Week.Firday;
            
            System.out.println(test); //輸出Firday，目前的列舉物件存的是Firday 常數
             System.out.println(test.ordinal()); //輸出 5
        }
    }
    ```
* 範例(設定常數)
    ```java=
    enum Week
    {
        Sunday(7), Monday(1), Tuesday(2), Wednesday(3), Tursday(4), Firday(5), Saturday(6);//每個都是 Week 型別
        
        private final intergerValue; //設定常數要存的地方，被建構就無法再修改值，因為 final
        
        Week() //多載不用設定常數的列舉元
        {
        
        }
        
        Week(int i) //建構子多載
        {
            intergerValue = i; //每個 Week 物件會有一個 intergerValue 的屬性，及我們要使用的常數值
        }
        
        public int getValue() //透過物件的方法存取常數值
        {
            return intergerValue;
        }
        
        public static int getValue(int i) //類別方法，藉由編號取的常數值
        {
            return (Week.values())[i].intergerValue;
        }
        
        public static Week getName(int i) //類別方法，藉由編號取的名稱
        {
            return (Week.values())[i];
        }
        
    }
    
    public class Test
    {
        public static void main(String[] args)
        {
            System.out.println(Week.Sunday); //輸出 Sunday，直接存取 Week類別屬性，其內容就是物件的名子
            System.out.println(Week.Tursday.getValue()) //輸出 4
            System.out.println(Week.getValue(0)) //輸出 7
            System.out.println(Week.getName(1)) //輸出 Sunday
            
            Week a = Week.Sunday;
            System.out.println(a); // Sunday
            System.out.println(a.getValue()); // 7
            System.out.println(a.orindal()); // 0
        }
    }
    ```
    * 編譯器會加上東西，所以並非是完整的程式碼
* 注意事項
    1. 列舉無法被實體化(列舉定義外面)
    ![](https://i.imgur.com/AGnqQQ0.png)
    * 只能參考到 (static)列舉元
    ![](https://i.imgur.com/HQw7JsM.png)
    2. 其他類別無法繼承 Enum ，列舉也無法被繼承
    3. 列舉可以透過 implements 實作其他介面
    
## 關於列舉
1. enum Week{...} 是一個延伸類別，他在編譯時期會自動繼承 Enum 這個抽象類別
2. 編譯過的列舉類別會有 final 的特性，即無法被繼承
3. 列舉的建構子由編譯器自行產生，權限是 private
4. 列舉元編譯過都是 public static final
5. 列舉內容值(編號)初始後就無法更改，與宣告順序一樣
6. 列舉可用 == 、 equals() 來比較
7. 編譯器會自動超載 valueOf() 類別方法，自動實作 values() 類別方法
8. 可以自行改寫列舉中的 toString() 來改變顯示狀態
* 列舉 Week 反編譯
    ```java=
    public final class Week extends Enum
    {
        private Week(String s, int i)
        {
            super(s, i)
        }
        
        public static final Week Sunday;
        public static final Week Monday;
        public static final Week Tuesday;
        
        private static final Week $VALUES[];
        
        public static final Week[] values()
        {
            return (Week[])$VALUES.clone();
        }
        
        public static Week valueOf(String s)
        {
            return (Week)enum.valueOf(Week, s);
        }
        
        static // static initializer
        {
            Sunday = new Week("Sunday", 0);
            Monday = new Week("Monday", 1);
            Tuesday = new Week("Tuesday", 2);
            
            $VALUES = 
            (
                new Week[] 
                {
                    Sunday, Monday, Tuesday
                }
            );
        }
    }
    ```
## 使用列舉
* 透過 . 運算子取得內容值
    ```java=
    Week a = Week.Sunday;
    ```
* 透過 values() 取得列舉內容
    * values() 將回傳列舉陣列 Week[]，可透過該陣列取得資料
    ```java=
    for(Week e : Week.values())
    {
        System.out.print(e + ", ")
    }
    ```
* 透過 valueOf(String s) 取得特定列舉元的值，s 是要找的列舉元名稱
    * vakueOf 是一個超載的方法，可自己設定
    ```java=
    System.out.println(Week.valueOf("Sunday"));
    ```
* 覆寫 toString()
    ```java=
    enum Grade
    {
        A{
            public String toString(){ return "Great"; }
        },
        B,
        C,
        D
    }
    ```
    * 我們可以透過改寫 toString() 來改變 System.out.println(Grade.A) 所回應的內容，因為在 println() 會執行預設的 toString() 的方法，即回應列舉元的名字
    * 改寫的方式是透過匿名內部類別的撰寫方法來加以實作，稱之為因值而異的類實作(Value-Specific Class Bodies)
* 透過 ordinal() 取出列舉序號
    ```java=
    int a = Week.Sunday.ordinal();
    Week x = Week.Tursday;
    int b = x.ordinal();
    ```
## 列舉 switch、==、equals()
* 與 switch 搭配
    ```java=
    Week test = Week.Firday;
    
    switch(test)
    {
        case Monday:
            System.out.println("not");
        break;
        
        case Firday:
            System.out.println("yes");
        break;
    }
    ```
* == 使用， 不可與非列舉元比較
    ```java=
    Week test = Week.Sunday;
    
    if(test == Week.Sunday) // (test == 0) => ERROR
    {
        System.out.println("yes");
    }
    ```
* 用 equals() 比較，可與非列舉元比較
    ```java=
    Week test = Week.Sunday;
    
    if(test.equals(Week.Sunday))
    {
        System.out.println("yes");
    }
    
    if(test.equals(0))
    {
        System.out.println("no");
    }
    else
    {
        System.out.println("yes2");
    }
    ```
## 列舉建構子、屬性
* 列舉中加入方法、建構子、屬性
    * 我們可以在列舉中加入final屬性，用來當作常用的常數
    * 設定常數需要考慮如何初始化(建構)、取用(方法)
    * 設定完列舉元要加上分號 ;
    * 在列舉中，建構子的存取權限是 private，編譯器會自動加上修飾
    ```java=
    enum Week
    {
        Sunday(7), Monday(1), Tuesday(2), Wednesday(3), Tursday(4), Firday(5), Saturday(6);//每個都是 Week 型別
        
        private final intergerValue; //設定常數要存的地方，被建構就無法再修改值，因為 final
        
        Week() //多載不用設定常數的列舉元
        {
        
        }
        
        Week(int i) //建構子多載
        {
            intergerValue = i; //每個 Week 物件會有一個 intergerValue 的屬性，及我們要使用的常數值
        }
        
        public int getValue() //透過物件的方法存取常數值
        {
            return intergerValue;
        }
        
        public static int getValue(int i) //類別方法，藉由編號取的常數值
        {
            return (Week.values())[i].intergerValue;
        }
        
        public static Week getName(int i) //類別方法，藉由編號取的名稱
        {
            return (Week.values())[i];
        }
        
    }
    
    public class Test
    {
        public static void main(String[] args)
        {
            System.out.println(Week.Sunday); //輸出 Sunday，直接存取 Week類別屬性，其內容就是物件的名子
            System.out.println(Week.Tursday.getValue()) //輸出 4
            System.out.println(Week.getValue(0)) //輸出 7
            System.out.println(Week.getName(1)) //輸出 Sunday
            
            Week a = Week.Sunday;
            System.out.println(a); // Sunday
            System.out.println(a.getValue()); // 7
            System.out.println(a.orindal()); // 0
        }
    }
    ```
## 在列舉中實作 abstract 方法
* 透過匿名內部類別的撰寫方式可以實作列舉定義的 abstract 方法
* 所有的列舉元都必須自行透過覆寫的機制實作 abstract 方法
```java=
public enum test
{
    a
    {
        int op(int x){ return x; }
    },
    b
    {
        int op(int x){ return x * 2; }
    };
    
    abstract int op(int x);
}
```
###### tags: `Java 學習筆記`
