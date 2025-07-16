## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/samba==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

```json
{
  "Hostname": String,
  "Status": enum (active|stopped), // 是否正在運行
  "Cpu": float,
  "Memory": float,
  "Connections": Int, // 當前連接到 Samba 伺服器的客戶端數量
  "Shares": [
    {
      "Name": String, // 共享名稱
      "Path": String, // 共享的本地路徑
      "Users": Int, // 目前正在訪問該共享的使用者數量
      "Permissions": String, // 設定的存取權限（如 read, write）
      "Status": enum (active|inactive) // 該共享的狀態
    } // ...
  ],
  "Logs": {
    "Samba_log": [
      {
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Client": String, // 客戶端 IP 和端口
        "Event": String, // 事件描述（如共享訪問、認證失敗等）
        "Level": enum (info|warn|error), // 記錄等級
        "Message": String // 具體訊息
      } // ...
    ],
    "Samba_log_Length": Int // Samba 日誌的條目數
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/samba/action/start==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 停止伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/samba/action/stop==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 重新啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/samba/action/restart==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
