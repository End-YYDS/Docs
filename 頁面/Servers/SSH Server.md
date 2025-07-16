## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/ssh==

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
  "Cpu": float, // CPU 使用率
  "Memory": float, // 記憶體使用率
  "Connections": Int, // 當前活躍的 SSH 連線數
  "Last_Login": {
    "User": String, // 最後登入的使用者
    "Date": {
      "Year": Int,
      "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
      "Day": Int,
      "Time": {
        "Hour": Int,
        "Min": Int
      }
    },
    "Ip": String // 最後登入的 IP 地址
  },
  "Logs": {
    "Auth_log": [
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
        "User": String, // 使用者名稱
        "Action": enum (login|logout|failed_login), // 行動類型
        "Result": enum (success|failure), // 連線結果
        "Ip": String, // 客戶端 IP 地址
        "Message": String // 附加訊息（例如登入失敗原因）
      } // ...
    ],
    "Auth_log_Length": Int // Auth_log 條目數量
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/ssh/action/start==

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
- URL: ==/api/server/ssh/action/stop==

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
- URL: ==/api/server/ssh/action/restart==

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
