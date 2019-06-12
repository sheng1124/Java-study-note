# [Java] (00) Java 認識、機制探討、第一步
## CH0： java 簡介
### Java基礎概念
* I. JAVA特色
    * 由James Gosling於1991年開發的**物件導向程式**(OOP)
    * 其名取至印尼的爪哇島的爪哇咖啡
    * Java 繼承 C++ 的物件導向核心技術
    * 沒有指標
    * 擁有"跨平台"的的特性
        *  java的編譯器會把java原始程式檔(.java)轉成"位元碼"形態的類別檔(.class)
        *  位元碼本身不受任何硬體架構限制，透過Java虛擬機器(Java VM)直譯就能執行，即在不同作業系統都能執行相同程式碼
    * 多執行緒
    * 例外處理
        * 解決程式"執行時期"所產生的錯誤 ex: segmentation fault(core dumped)，在未提供例外處裡的語言，要找到錯誤不容易 
         
* II. JRE (java Runtime Environment)
    * 執行java應用程式所需的基本環境，所有的 Java 程序都要在 JRE 下才能運行
    * 任何系統上若要執行Java編寫的程式，需要用到的平台(軟體)
    * JRE 包含(不只)
        * 核心庫檔案、綜合庫檔案、使用者介面庫檔案
        * Java虛擬機器（JVM）
    * Java 主要的運行平台
        

    |          | Java SE(J2SE)   | Java EE(J2EE)     |Java ME(J2ME) |
    | -------- | --------        | ------------------|--------------|
    | 名稱      | Standard Edition(標準版)|Enterprise Edition(企業) |Micro Edition |
    | 版本功能  |普通              | 較強               |較弱           |
    | 版本定位  | Client端         | Server端           |行動裝置       |
    | 應用實例  | 薪資管理軟體       | 線上購物系統        |嵌入式機器      |
    | 關係      | SE 為 ME 父集    | EE 包含 SE 功能     |ME 為 SE 子集|


* III. JDK (Java Development Kit)
    * 用來開發 Java 程式的平台，包含 JRE 、 Java 應用程式開發工具
    *  JDK 的工具:
        *  是 Java 程序，需要 JRE 才能運行
        ![](https://i.imgur.com/UXFhCGe.png)

* IV. JDK 常用API(工具)
    * javac
        * Java 編譯器
    * java
        * 執行 Java 應用程式
    * javaw
        * 視窗模式的 Java 直譯器
    * appletviewer
        * Applet 直譯器
    * jar
        * java 壓縮工具
    * jbd
        * java 除錯工具
    * javah
        * 產生 C 語言可用的標頭檔(.h)
    * jacap 
        * java 反組譯

* V. SDK (Software Development Kit) ：軟件開發工具包
    * 用於為特定的軟體包、軟體框架、硬體平台、作業系統等，建立應用軟體的**開發工具**的集合
    * 各種不同類型的軟件開發，都可以有自己的 SDK
        * Windows SDK
        * DirectX SDK
        * iOS SDK (iPhone SDK)
        * Android SDK
        * Java SDK (同 JDK = Java Development Kit)
* VI Java Application v.s Java Applet
    * Java 程式主要分這兩種
    
    |          | Java Application| Java Applet |
    | -------- | --------------- | ----------- |
    | 名稱      | java 應用程式    | Java 小程式  |
    | 可獨立運行 | YES             | NO          |
    | 應用      | 視窗應用程式開發   | 網頁瀏覽器執行的 Web 內嵌應用程式|
    | 占用記憶體 | 大             | 小         |
    | 程式執行速度| 快             | 慢         |
    | 支援類別功能| 完整             | 普通，開發功能單一      |
    | 執行方式   | 命令列參數執行     | 瀏覽器開啟有宣告使用 Applet 的 HTML 文件執行|
 
 * VII 一些Java名詞(遇到、忘記再查)
     * Spring
     * Struts
     * Hibernate
     * Servlet
     * JavaFX Technology
     * JavaBeans
     * Web Services using JAX-RPC
     * N-tier
     * JCR (Java Content Repository)
     * JSP (Java Server Pages)
     * JDBC (Java Database Connectivity)
     * JCP (Java Community Process)
     * JAX (Java API for XML)
     * UML (Unified Modeling Language)
     * RMI (Remote Method Invocation)
     * JCA J2EE Connector Architecture)
     * MVC (Model-View-Controller)
     * ORM (Object-Relational Mapping)
     * JSF (JavaServer Faces)
     * EJB (Enterprise JavaBeans)
     * Ajax (Asynchronous JavaScript and XML)
### Java 的執行平台架構與運作原理

* I Java平台架構
    * 基本上由 JDK/JRE 和作業系統組成
    * ![](https://i.imgur.com/2VbSTj7.png)
    * Java Language
        * Java 程式語言部分
    * Tools & Tool APIs
        * 工具，ex:編譯器
    * Deployment Technologies
        * 部屬技術部分
    * JVM
        * Java虛擬機器
    * User Interface Toolkits
        * 使用者介面工具
    * Integration Libraries
        * 整合程式庫
    * Other Base Libraries
        * 其他基底程式庫
    * lang and util Base Libraries
        * 語言和工具基底程式庫
* II JVM運作機制
    * JVM(Java Virtual Machine)
        * JVM 經由 JRE 模擬，所有 java 程式在 JVM 中執行
        * JVM 執行經由編譯過 java code 的 Bytecode
        * 不同的 OS 有不同的 JVM 來對應解釋，所以 bytecodes 能夠不受作業系統限制    
    * Java 編譯示意圖
        * ![](https://i.imgur.com/wEQ2vJH.png)
        * 不同的作業系統有個別的直譯方式，所以不同系統的JVM不一定相同，JVM又稱Java直譯器
    * JVM 流程圖
        * ![](https://i.imgur.com/Zxi07ug.png)

        (PS: 一般透過命令提示字元開啟 Java 程式，可透過製作批次檔 .bat 來執行，就像雙擊可執行檔一樣)


### JAVA Framework 類型介紹 (未完成)
* Spring Framework
* Hibernate Framework
* Struts Framework
###
     
## CH1 編寫 Java
### Java in Linux
* 安裝JDK
    ```linux=
    sudo apt-get update
    ```
    ``` linux=
    sudo apt-get install default-jdk
    ```
* 檢查 Java 版本
    ```linux=
    java -version
    ```
* 編輯 filename.java 檔案
    ``` linux=
    gedit /path/filename.java
    ```
    ![](https://i.imgur.com/uvPCeiW.png)
* 編譯
    ```linux=
    javac /path/filename.java
    ```
* 執行
    ```linux=
    java /path/filename.java
    ```

### Java in Windows
* 下載 jdk
* 安裝 jdk
* 環境變數設定

### Java 環境的相關重要檔案
* javac
    * 編譯程式，將 .java -> .class
* java
    * 解譯(直譯)程式，執行 .class 檔
* javap
    * 反組譯，.class -> .java 
* appletviewer
    * 執行 Java Applet 程式
 
### 使用記事本編寫 Java
* 編寫程式碼
    ![](https://i.imgur.com/uvPCeiW.png)
* 編譯
    * windows
    ```windows=
    C:\>javac path\name.java
    ```
    * Linux
    ```linux=
    javac /path/filename.java
    ```
 * 執行
    * windows
    ```windows=
    C:\>java path\name.java
    ```
    * Linux
    ```linux=
    java /path/filename.java
    ```
 
## CH2：Java 的整合開發環境(IDE)開發工具簡介
### NetBeans
* 官方網站
    * https://netbeans.org/
* Wiki
    * https://zh.wikipedia.org/wiki/NetBeans
### Eclipse
* 官方網站
    * http://www.eclipse.org/
* Wiki
    * https://zh.wikipedia.org/wiki/Eclipse
* 主流的開發 Java 的工具
* 編寫Java流程
    * 新專案
    ![](https://i.imgur.com/eLbxzzO.png)
    ![](https://i.imgur.com/WTOzLnZ.png)
    ![](https://i.imgur.com/6j5T6Nt.png)
    
    * 新增 Class 檔
    ![](https://i.imgur.com/odpki3S.png)
    ![](https://i.imgur.com/PsvRE31.png)
    
    * 載入專案
    ![](https://i.imgur.com/WNJPpxZ.png)
    ![](https://i.imgur.com/clkuahy.png)



 
### Jbuilder
* 官方網站
    * https://web.archive.org/web/20041110030013/http://www.borland.com/jbuilder/
* Wiki
    * https://zh.wikipedia.org/wiki/JBuilder
### Java 專案類型
* Java Application
    * 用來開發一般普通的 Java 程式，用來開發DOS命令的程式可用此專案
* Java Desketop Application
    * 用來開發 Java 視窗應用程式，IDE會加入視窗的套件
* Java Class Library 
    * 用來開發 Java 的類別庫，通常用來開發一些常用的程式模組，供其他程式引用


###### tags: `Java 學習筆記`
