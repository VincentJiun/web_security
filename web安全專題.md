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

2. 具體怎麼操作

3. 工具利用
    - Burp Suite