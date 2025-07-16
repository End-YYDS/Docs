## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/apache==

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
  "Memory": float, // 使用率
  "Connections": Int,
  "Logs": {
    "Error_log": [
      {
        "Date":{
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Week": enum (Mon|Tue|Wed|Thu|Fri|Sat|Sun),
          "Time": {
            "Hour": Int,
            "Min": Int,
          }
        },
        "Module": String,
        "Level": enum (debug|info|notice|warn|error|crit|alert|emerg),
        "Pid": Int,
        "Client": String, // 發送請求的 IP 和 Port
        "Message": String,
      }, // ...
    ],
    "Errlength": Error_log.len,
    "Access_log": [
      {
        "Ip": String,
        "Date":{
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int,
          }
        },
        "Method": String, // 請求方法 如GET POST
        "URL": String, // 客戶端請求的 URL
        "Protocol": String, // 協議
        "Status": Int, // HTTP 狀態碼（如 200 成功，404 找不到）
        "Byte": Int, // 回應大小
        "Referer": String, // 來源網站（如 "https://example.com"）
        "User_Agent": String, // 使用者瀏覽資訊
      }, // ...
    ],
    "Acclength": Access_log.len,
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/apache/action/start==

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
- URL: ==/api/server/apache/action/stop==

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
- URL: ==/api/server/apache/action/restart==

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
