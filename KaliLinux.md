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
- Hydra






















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
