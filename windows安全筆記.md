# 網路安全筆記

# 破解windows系統密碼

## 漏洞1: 利用5次shift漏洞破解win7密碼

### 1-1 漏洞
1. 在尚未登入系統時，連續按5次shift鍵，彈出程序 c:\widows\system32\sethc.exe
2. 部分win7以及win10系統在未進入系統時，可以通過系統修復漏洞竄改系統文件名
    - 註: 如果win7、win10系統已修補漏洞2，則無法利用

### 1-2 相關知識
1. cmd工具路徑
    - c:\windows\system32\cmd
2. 用戶帳號密碼儲存位置
    - c:\windows\system32\config\SAM
3. 修改帳戶密碼
    - net user 用戶名 新密碼
4. 創建一個新帳戶
    - net user 用戶名 密碼 /add
5. 刪除用戶
    - net user 用戶名 /del
6. 提升管理員
    - net localgroup administrators 用戶名 /add

### 1-3 流程
- https://www.youtube.com/watch?v=UDrj_jsQ0HY&list=PLLoeRTvFkQhs_BFrlc-mlOVp7omTitbWq&index=88


