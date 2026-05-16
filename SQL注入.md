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

### 支持注入類型:
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

### 基本用法
```cmd (kali)
sqlmap -u "target_url?id=1"
```
- windows版本指令: python sqlmap.py sqlmap -u "target_url?id=1"
- -u: 後面接目標URL地址以及參數名
- --dbs: 獲取該主機所有的數據庫
- --dbms=mysql: 指定數據庫類型
- -D "DB_Name": 指定數據庫
- --table: 獲取該數據庫全部的數據表
- -T "Table_Name": 指定數據表
- --col: 顯示所有列
- -C "col_name1, col_name2": 指定列顯示內容
- --dump: 顯示資料內容


## SQL注入常見類型

