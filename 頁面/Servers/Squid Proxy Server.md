## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/squid==

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
  "Connections": Int, // 當前活躍的代理連線數
  "Cache_Hits": Int, // 緩存命中數
  "Cache_Misses": Int, // 緩存未命中數
  "Requests_Processed": Int, // 總請求數量
  "Logs": {
    "Access_log": [
      {
        "Ip": String, // 客戶端 IP
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Method": String, // 請求方法（如 GET, POST）
        "URL": String, // 請求的 URL
        "Status": Int, // HTTP 狀態碼（如 200 成功，404 找不到）
        "Bytes_Served": Int, // 回應的位元組數
        "Referer": String, // 來源網站（如 "https://example.com"）
        "User_Agent": String // 使用者瀏覽器資訊
      } // ...
    ],
    "Access_log_Length": Int // Access_log 的條目數
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/squid/action/start==

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
- URL: ==/api/server/squid/action/stop==

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
- URL: ==/api/server/squid/action/restart==

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
