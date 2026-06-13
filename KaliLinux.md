# Kali Linux && 常用工具操作筆記

## 攻防思路
- 攻擊流程:
    - 信息收集 -> 是否存在既有漏洞
        - 有: 漏洞利用(攻擊)
        - 無: 漏洞挖掘 -> 漏洞利用 -> 權限維持 -> 內網滲透 -> 報告輸出

## 信息收集

### 網站目錄
    - 登入入口
    - 後臺入口
    - 數據庫下載地址
    - 敏感文件下載地址
    - 網站目錄架構
    - GIT/SVN洩漏
    - 代碼洩漏
    - ....

### 前端代碼
    - 代碼框架
    - 代碼組件
    - 代碼庫
    - 代碼注釋
    - 已知漏洞

### 後端代碼
    - 代碼框架
    - 代碼組件
    - 已知漏洞

### 數據庫
    - 數據庫分類
    - 已知漏洞

### 伺服器
    - IP/端口

### 子域名
- 子域名(或子域，Subdomain)在域名系統等級中，屬於更高一層的域。Ex: mail.example.com、a.example.com是example.com的子域，而example.com是頂級域名.com的子域
#### 子域名獲取方法
1. 爆破
2. 域傳輸漏洞
3. 證書子域名
4. robots.txt
5. HTTP頭跨域策略文件
6. 搜尋引擎
    - site: *baidu.com -www -baike
7. 其他搜尋引擎
    - https://crt.sh/
    - https://censys.io/
8. 公開數據
9. 工具
    - Maltego (Kali 自帶工具 需註冊並登入) -> 信息收集集大成工具
    - Sublist3r: https://github.com/aboul3la/Sublist3r
    - OneForAll: https://github.com/shmilylty/OneForAll

### 網站指紋識別
- 目錄掃描前，可以先了解該網站是用甚麼語法/框架編寫(以及版本)，可以先行了解該語法/框架是否存在既有漏洞做利用

#### 工具
- whatweb: Kali自帶CLI命令工具
- WhatRuns: Chrome插件

### 網站目錄
- 登入入口
- 後台入口
- 數據庫下載地址
- 敏感文件下載地址
- 網站目錄架構
- GIT/SVN洩漏
- 代碼洩漏
- ......

#### 如何獲取
- 爬蟲爬取
- 暴力掃描
- 搜尋引擎 (google、Shodan...)
    - site: [url]
- ......

#### 工具利用
1. Burp Suite
2. dirsearch
    - https://github.com/maurosoria/dirsearch

### 網頁漏洞掃描

#### 工具利用
- Jaeles
    - https://github.com/jaeles-project/jaeles
- nikto
    - https://github.com/sullo/nikto

### 網站WAF
- WAF(WEB APPLICATON FIREWALL)
#### 工具利用
- wafw00f
    - https://github.com/EnableSecurity/wafw00f

### 代理掃描

#### 工具
- proxychains-ng
    - https://github.com/rofl0r/proxychains-ng

### 網站CDN
- CDN(Contect Delivery Network)
- 先掃描網站確定是否有CDN，再探測網站真實伺服器IP
#### 掃描工具
- WhichCDN
    - https://github.com/Nitr4x/whichCDN

#### 獲取網站IP工具
- CloudFlair (針對CloudFlair)
    - https://github.com/christophetd/CloudFlair
- w8fuckcdn
    - https://github.com/boy-hack/w8fuckcdn

### 蜜罐原理
- 蜜罐: 網站上部屬陷阱，讓攻擊者進入陷阱

#### 蜜罐部屬工具
- HFish
    - https://github.com/hacklcx/HFish

### 信息收集-小結
- https://www.youtube.com/watch?v=d8xfCazLVPY&list=PLgZqc0esdeS9mbMWvAi5I7TWUWgaZLtpQ&index=23

## 漏洞挖掘

### 弱口令漏洞
- 利用已知的簡單口令(密碼)嘗試爆破並登入
    1. SSH
    2. FTP
    3. 3389 port
    4. 網頁登入框

#### 爆破工具利用
- Hydra (Kali自帶)
    - rockyou.txt: 常用密碼爆破字典
- Burp Suite(可做為web輸入框的弱口令爆破)
    - https://www.youtube.com/watch?v=Ad1SeQQmopc&list=PLgZqc0esdeS9mbMWvAi5I7TWUWgaZLtpQ&index=27

### 邏輯漏洞
- 例如: 商城購物可以直接從前端更改(數量、價格)
    1. 利用BurpSuite抓包並修改
    2. Forward並觀察回傳變化

### 敏感信息/文件洩漏
- Phpinfo
- 源碼/注釋洩漏
- 版本信息洩漏
- 備份文件洩漏
- GIT版本控制洩漏

#### 目錄遍歷(Directory traversal)漏洞
- 透過網頁獲取主機資料(圖片)時，修改獲取路徑達到獲取敏感信息目的

##### 漏洞測試方法
- 利用Burp Suite抓包並修改file路徑
- 參考資料: https://www.youtube.com/watch?v=UPvSuzBhztg&list=PLgZqc0esdeS9mbMWvAi5I7TWUWgaZLtpQ&index=34

### 命令注入(OS command injection)漏洞
- 是一種常見的網頁注入攻擊行為，若管理者未在網站的輸入表單中正確過濾敏感字元，攻擊者有則可能透過這些進入點，將指令傳送至Server本機中執行後，再將執行結果透過動態網頁語言輸出，藉此獲取機敏資訊或執行未經授權的任意指令。




# 常用工具介紹
## NMAP
- 功能: 活耀IP、端口、端口服務、操作系統掃描
- 流程: 目標確認 -> 主機發現 -> 端口掃描 -> 掃描技術 -> 探測服務 -> 探測防火牆 -> 性能優化 -> 報告書出

### 指令
- 在cmd視窗打入nmap，即可跳出全部的指令說明
#### 常用指令
```cmd
nmap [target_ip/domain]
```
- 掃描命令
    - -iL ip.txt: 從文字檔中批量讀取目標
    - -iR [數量]: 隨機掃描
    - -A: 掃描完整訊息
    - --script script_file: 腳本掃描
    - -n/-R: 不做/總是DNS解析 (預設: Sometimes) 
- 端口掃描
    - -p [連接埠]: 掃描特定連接埠(如 -p 80)、範圍或多個連接埠(ex: 80,8080 or 1-65535)
        - -p *: 掃描全部 65,535 個連接埠
    - --top-ports [數量]: 掃描排名前幾名的熱門連接埠

- 主機發現與 Ping 技術
    - 在掃描連接埠前，Nmap 預設會先 Ping 目標
    - -Pn: (跳過發現)將所有主機視為在線，適合應對屏蔽 Ping 的防火牆
    - -sP: (Ping 掃描)僅確認主機是否在線，不掃描連接埠
    - 不同協議的 Ping：包含 TCP SYN Ping (-PS)、TCP ACK Ping (-PA)、UDP Ping (-PU)、ICMP Echo Ping (-PE)、ICMP 時間戳 Ping (-PP) 等，用以繞過不同的過濾規則

- 掃描方式
    - -sS: (TCP SYN 掃描)預設且最受歡迎的掃描，不完成三向交握，較為隱蔽（但現代防火牆仍可偵測）
    - -sT: (TCP Connect 掃描)建立完整連接，通常用於非 root 用戶或 IPv6 目標
    - -sU: (UDP 掃描)針對 DNS、DHCP 等 UDP 服務進行探測
    - -O: (作業系統偵測)透過 TCP/IP 指紋識別目標的作業系統類型
    - -sV: (服務版本偵測)辨識特定連接埠上運行的軟體供應商與版本號碼

- 效能、時序與規避技術
    - 時序模板 (-T0 到 -T5)：調整掃描速度，從極慢（隱蔽）到極快

- 輸出
    - -oN file: 輸出正常文件格式

## Burp Suite






## 識別密碼哈希
### Linux密碼
- Linux密碼哈希值儲存在 中/etc/shadow，通常只有 root 使用者才能讀取。它們以前儲存在 中/etc/passwd，所有人都可以讀取。
- 加密密碼欄位包含雜湊後的密碼短語，該密碼短語由四個部分組成：前綴（演算法 ID）、選項（參數）、鹽值和雜湊值 -> $prefix$options$salt$hash

- 前綴:
    - $y$: yescrypt 是一種可擴展的雜湊方案，是新系統中的預設和建議選擇
    - $gy$: gost-yescrypt 使用 GOST R 34.11-2012 雜湊函數和 yescrypt 雜湊方法
    - $7$: scrypt 是一種基於密碼的金鑰衍生函數
    - $2b$...$2y$、$2a$、$2x$: bcrypt 是一種基於 Blowfish 分組密碼的雜湊演算法，最初是為 OpenBSD 開發的，但也由最新版本的 FreeBSD、NetBSD、Solaris 10 及更高版本以及一些 Linux 發行版所支援
    - $6$: sha512crypt 是一種基於 SHA-2 的雜湊演算法，輸出 512 位，最初是為 GNU libc 開發的，常用於（較舊的）Linux系統
    - $md5: SunMD5 是一種基於哈希的演算法MD5該演算法最初是為 Solaris 開發的
    - $1$: md5crypt 是一種基於 MD5 演算法的雜湊演算法，MD5 演算法最初是為 FreeBSD 開發的

### 現代Linux密碼範例
```
root@TryHackMe# sudo cat /etc/shadow | grep strategos
strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4:19965:0:99999:7:::
```
- 欄位之間用冒號分隔。重要的欄位包括用戶名、哈希演算法、鹽值和哈希值。第二個欄位的格式為$prefix$options$salt$hash：
    - y表示所使用的哈希演算法，yescrypt
    - j9T是傳遞給演算法的一個參數
    - 76UzfgEM5PnymhQ7TlJey1所用的鹽
    - /OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4是哈希值

### 微軟Windows密碼
- MS Windows 密碼使用雜湊演算法進行加密NTLM是 MD4 的一種變體。它們在視覺上與 MD4 完全相同，MD5哈希值，因此使用上下文來確定哈希類型非常重要。
- 在微軟Windows系統中，密碼雜湊值儲存在安全帳戶管理員（SAM）中。微軟Windows會盡量阻止一​​般使用者匯出這些雜湊值，但像mimikatz這樣的工具可以繞過微軟Windows的安全機制。值得注意的是，SAM中的雜湊值分為NT雜湊值和LM雜湊值。


todo: 35