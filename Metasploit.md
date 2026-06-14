# Metasploit 筆記
- Metasploit是一個功能強大的工具，可以支援滲透測試的各個階段，從資訊收集到滲透後階段。

## 框架
- msfconsole：主命令列介面
- 模組：支援漏洞利用程式、掃描器、有效載荷等模組
- 工具：可協助漏洞研究的獨立工具，脆弱性評估或者說是滲透測試。包括:msfvenom、pattern_create 和 pattern_offset

## Msfconsole
- msfconsole: Metasploit控制台。控制台是與 Metasploit 框架的不同模組互動的主要介面。模組是 Metasploit 框架中的小型元件，旨在執行特定任務，例如利用漏洞、掃描目標或執行暴力破解攻擊。

### 其他模組
- Auxiliary (輔助): 支援模組，例如掃描器、爬蟲和模糊測試器
- Encoders (編譯): 對漏洞利用程式和有效載荷進行編碼，希望基於特徵碼的防毒解決方案能夠漏檢它們
- Evasion (規避): 雖然編譯器會對有效載荷進行編碼，但它們不應被視為直接試圖繞過防毒軟體。另一方面，「規避」模組則會嘗試這樣做，但成功率或高或低
- Exploits (漏洞利用): 漏洞利用程序，依目標系統整齊分類
- NOPs: NOP（無操作）指令其實什麼都不做。在 Intel x86 CPU 系列中，NOP 指令以 0x90 表示，表示 CPU 將在一個時脈週期內不執行任何操作。 NOP 指令通常用作緩衝區，以確保有效載荷大小的一致性
- Payloads (有效載荷): 有效載荷是在目標系統上運行的程式碼，Metasploit能夠發送不同的有效載荷，從而在目標系統上開啟 shell。
    - Adapters (適配器): 適配器用於封裝單一有效負載，將其轉換為不同的格式。例如，可以將一個普通的單一有效負載封裝在 PowerShell 適配器中，該適配器會產生一個 PowerShell 命令來執行該有效負載
    - Singles: 獨立的有效載荷（新增使用者、啟動 notepad.exe 等），無需下載其他元件即可運作
    - Stagers: 負責建立連接通道Metasploit以及目標系統。這在處理分階段有效載荷時非常有用。 「分階段有效載荷」會先在目標系統上傳一個分階段程序，然後再下載剩餘的有效載荷（階段）。這樣做的好處在於，與一次性發送的完整有效載荷相比，初始有效載荷的大小相對較小
    - Stages: 由部署者下載。這將允許您使用更大尺寸的有效載荷

- Post (後滲透): 在上述滲透測試過程的最後階段（即滲透後階段）非常有用

## 指令
- help [commands]: 可以單獨使用，也可以用於特定指令
- history: 查看先前輸入的指令
- use [exploit]: ex: use exploit/windows/smb/ms17_010_eternalblue
- show options: 查看此漏洞利用設定
- show: 命令可在任何上下文中使用，後跟模組類型（輔助模組、有效載荷模組、漏洞利用模組等），以列出可用模組
- back: 退回上一層
- info: 獲取任何模組的更多信息，也可後面接著模組路徑 Ex: info exploit/windows/smb/ms17_010_eternalblue
- search: 在 Metasploit Framework 資料庫中搜尋與給定搜尋參數相關的模組
- set [PARAMETER_NAME] [VALUE]: 設定
