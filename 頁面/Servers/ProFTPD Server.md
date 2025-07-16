## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/ftp==

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
  "Connections": Int, // 當前 FTP 活躍連線數
  "Sessions": [
    {
      "Ip": String, // 連線客戶端 IP
      "Username": String, // 已認證的使用者名稱
      "Login_Time": {
        "Year": Int,
        "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
        "Day": Int,
        "Hour": Int,
        "Min": Int
      },
      "Current_Dir": String, // 當前工作目錄
      "Status": enum (Idle|Uploading|Downloading|Disconnected), // 當前狀態
      "Transfer": {
        "Type": enum (Upload|Download),
        "File": String, // 檔案名稱
        "Size": Int, // 檔案大小 (Bytes)
        "Speed": Int // 速度 (Bytes/s)
      }
    } // ...
  ],
  "Logs": {
    "Error_log": [
      {
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Week": enum (Mon|Tue|Wed|Thu|Fri|Sat|Sun),
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Module": String,
        "Level": enum (debug|info|notice|warn|error|crit|alert|emerg),
        "Pid": Int,
        "Client": String, // 發送請求的 IP 和 Port
        "Message": String
      } // ...
    ],
    "Errlength": Error_log.len,
    "Access_log": [
      {
        "Ip": String,
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Username": String, // 登入使用者
        "Action": enum (Login|Logout|Upload|Download|Delete|Rename), // FTP 行為
        "File": String, // 操作的檔案名稱（若適用）
        "Size": Int, // 檔案大小（若適用，Bytes）
        "Status": enum (Success|Failed) // 操作結果
      } // ...
    ],
    "Acclength": Access_log.len
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/ftp/action/start==

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
- URL: ==/api/server/ftp/action/stop==

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
- URL: ==/api/server/ftp/action/restart==

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
