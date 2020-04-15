# [Java] (11) Java 物件導向-抽象類別、方法(abstract class)

## 抽象類別
* 說明
    * 抽象類別是一種無法具體化的類別
    * 是開發的構想，沒有詳實細節，並交給研發部門去實作
    * 抽象類別是有範本作用的父類別
    * 繼承他的子類別一定要依照他的規格(模型)來定義、實作
    * **抽象類別不能使用 new 來產生"物件實體"，只能被繼承**
* 宣告方式
    ```java=
    abstract class TypeName
    {
        //dataMember...
        //methodMemder...
    }
    ```
* 注意事項
    * 抽象類別內的方法成員，可以是一般方法成員、抽象方法，一般類別不能有抽象方法
    * 抽象方法只能宣告不能用```{}```實作
    * 抽象方法必須要用 ```abstract``` 宣告，其存取修飾子不能為 ```private```，因為子類別繼承時需要覆寫(override) 

## 抽象方法
* 說明
    * 抽象類別中的抽象方法必須由子類別來重新實做
    * 若子類別沒需要實作該方法，則必須也要宣告成**抽象類別**
    * 抽象方法只能宣告不能用```{}```實作
    * 抽象方法必須要用 ```abstract``` 宣告，其存取修飾子不能為 ```private```，因為子類別繼承時需要覆寫(override) 
* 宣告方式
    ```java=
    存取修飾元 abstract 傳回值 方法名稱(參數列...);
    ```
## 範例
* 
    ```java=
    abstract class Car
    {
        int speed;
        public abstract void addSpeed(int s);
        public static void message()
        {
            System.out.println("all car can speed up");
        }
    }
    
    class PiliCar extends Car
    {
        public void addSpeed(int s)
        {
            speed += s;
        }
    }
    
    class BMW extends Car
    {
        public void addspeed(int s)
        {
            speed += s*2;
        }
    }
    ```

###### tags: `Java 學習筆記`
