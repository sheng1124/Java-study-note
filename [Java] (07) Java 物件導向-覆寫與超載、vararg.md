# [Java] (07) Java 物件導向-覆寫與超載、vararg

## 覆寫(Overriding)
* 覆寫
    * 覆寫是發生在繼承關係中，子類別自行實作一個同名的方法來取代父類別所提供的方法
    * 程式在執行中會執行子類別的方法，而不執行父類別的同名方法
    ```java=
    public class Father 
    {
        void speak()
        {
            System.out.println("father talk");
        }
    }
    
    public class Son extends Father
    {
        void speak()
        {
            System.out.println("son talk");
        }
    }
    ```
* 建構子的覆寫 => 參考繼承
* 有例外事件的覆寫
* 覆寫的回傳型態
    * 回傳型態必須是相同 或 原方法傳回型別的子類別(javaSE 5.0 之後)
    ```java=
    class Skill {}
    
    class AdvSkill extends skill {}
    
    class Animal
    {
        Skill A;
        public Skill getSkill()
        {
            A = new Skill();
            return A;
        }
    }
    
    class Dog extends Animal
    {
        AdvSkill a;
        public AdvSkill getSkill()
        {
            a = new AdvSkill();
            return a; //原方法傳回型別的子類別
        }
    }
    ```
* 靜態成員的限制
    * static 方法只可以使用 static 資料和方法
    * 類別有 static 方法成員，子類別不可以有相同名稱、參數的 non-static 方法
    * 即子類別不能覆寫父類別 static 方法成員，除非要加上 static
    ```java=
    class A
    {
        static int a = 123;
        static void show()
        {
            System.out.println("ooo");
        }
    }

    class B extends A
    {
        int a = 356;
        void show()
        {
            System.out.println("iii"); // error
        }
    }
    ```
* 注意事項
    1. 覆寫發生在有繼承關係的類別中
    2. 方法名稱宣告必須相同
    3. 若有回傳值，該回傳型態必須是相同 或 原方法傳回型別的子類別
    4. 參數列必須相同
    5. 存取權限不可小於原方法
    6. 當原方法發生例外事件，覆寫也可引發例外事件
        * 但這個例外事件(子)要包含在原方法所引發的例外事件內(相等或不寫)
## 遮蔽(Hide)
* 屬性的覆寫機制
    * 屬性的覆寫機制稱為 遮蔽
    * 仍可用 super 關鍵字存取父類別的屬性
    ```java=
    class Animal
    {
        int legs;
    }
    class Dog extends Animal
    {
        int legs; //Hide
    }
    ```

## 超載(Overloading)
* 超載是指同一種方法可以產生不同的實作
* 依傳入不同的參數、數量來實作相異的程式碼
* 可分方法的超載、建構子的超載
* Java 沒有 operator 的多載
* 相同參數列，就變成覆寫
* 子類別也可超載父類別(要注意實作的要求是覆寫或超載以免寫錯)
    ```java=
    // 方法超載
    public void aMethod(){};
    public void aMethod(int a){};
    public void aMethod(int a, int b){};
    // 建構子超載
    public Base(){};
    public Base(String a){};
    public Base(String a, String b){};
    ```

## vararg-建構變長的參數
* N個參數的參數列-傳統作法
    * 要實現 N 個參數列傳統上是傳入陣列 int[]
    ```java=
    public int calc(int [] list)
    {
        int sum = 0;
        for(int i = 0; i < list.length; i++)
        {
            sum += list[i];
        }
        return sum;
    }
    ```
    * 使用上有點麻煩
    ```java=
    objectName.calc(new int[] {1,2,3,4});
    ```
* Vararg
    * 有這機制我們可以隨意增長方法中的參數
    * 寫法 ```method(int... s)```
    ```java=
    public int newCalc(int... list)
    {
        int sum = 0;
        for(int e : list)
        {
            sum += e;
        }
        return sum;
    }
    ```
###### tags: `Java 學習筆記`
