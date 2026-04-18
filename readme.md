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

2. 






