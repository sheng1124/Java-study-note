# [Java] (04) Java 控制流程

## if-else
* if - else if - else
    ```java=
    if(boolean-expresson)
    {
        //...
    }
    else if(boolean-expresson)
    {
        //...
    }
    else
    {
        //...
    }
    
    ```
* if(...) ， ()只能放布林運算式
    ```java=
    if(a=0) //error a=0 value is 0 not False
    {
        //...
    }
    ```
## switch-case
* switch
    ```java=
    switch(expression:x) //x must be byte,char,short,int
    {
    case 1:
        //...    
    break;
    
    case 2:
        //...
    break;
    
    case 3:
    case 4:
        //...
    break;
    
    default :
        //...
    break;
    }
    ```
## for loop
* for-loop 
    ```java=
    for(initialization; boolean-expression; stepping)
    {
        //statement
    }
    ```
* for/in (for-each)
    ```java=
    for(元素資料型別 代表每個元素的變數 : 母體集合) // for e in [list]
    {
        //statement
    }
    
    for(string e : exams)
    {
        System.out.println(e);
    }
    ```
## While Loop
* While
    ```java=
    while(boolean expression)
    {
        //statement
    }
    ```
* do-While
    ```java=
    do
    {
        //statement
    }while(boolean expression);
    ```


## break、 continue
* break
    * 中斷迴圈、離開 switch 敘述
* continue
    * 略過當前至迴圈結尾的程式碼，跳躍到 stepping 敘述，並重頭執行一次迴圈 

## loop label
* loop label
    * 我們可以為 loop 加上 label 來命名
    * 搭配 break、continue 可以做更多流程控制
    ```java=
    OuterLoop: //label 外層迴圈 
    for(int i = 0; i < 100; i++)
    {
        InnerLoop: //label 內層迴圈
        for(int j = 0; j < 100; j++)
        {
            if(...) break InnerLoop;
            if(...) break OuterLoop;
            if(...) continue InnerLoop;
            if(...) continue OuterLoop;
        }
    }
    ```


###### tags: `Java 學習筆記`
