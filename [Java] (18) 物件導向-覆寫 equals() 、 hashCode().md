# [Java] (18) 物件導向-覆寫 equals() 、 hashCode()
## equals()
* 說明
    * equals()用來比較兩個物件
    * 兩個物件的相等是一個 business 的問題，甚麽是物件的相等，應該由設計者去決定
    * 所以我們需要去覆寫 equals() 決定這個物件的相等條件
* Object 類別的 equals()
    * 僅比較兩個物件的記憶體參照位置
    * 和實際物件的變數/屬性毫無關聯
* 範例
    ```java=
    class Ball
    {
        String tradeMark;
        String kind;
        String color;
    
        Ball(String t, String k, String c)
        {
            tradeMark = t;
            kind = k;
            color = c;
        }
    
        public boolean equals(Object obj)
        {
            if(this == obj) return true;
            if(obj != null && getClass() == obj.getClass())
            {
                if(obj instanceof Ball)
                {
                    Ball ball = (Ball)obj;
                    if(tradeMark.equals(ball.tradeMark) && kind.equals(ball.kind) && color.equals(ball.color))
                    {
                        return true;
                    }
                }
            }
            return false;
        }
    }
    ```
* 覆寫 equals() 的基本原則
    * 仍要使用"=="來判斷，也許兩個要比較的物件是同一個實體
    * 要比較兩個隸屬於同一個 class 的物件，可以用 getClass（）來判斷

## hashCode()
* 說明
    * hashcode 可以想成是物件的座號，用來做物件定址以方便找到標的物件
    * 對同一個物件呼叫 hashCode() 其回傳值必須一樣
    * 若兩個物件被 equals() 定義是相等的，則 hashCode() 也必須是一樣
* 參考
    * equals() & hashCode() in Java
        * https://medium.com/joe-tsai/equals-hashcode-4480f4580be4 

###### tags: `Java 學習筆記`
