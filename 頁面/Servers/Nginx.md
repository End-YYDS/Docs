## RestfulApi :

在 Nginx 頁面中，點進單一電腦後

### 伺服器狀態監控

Apache 主要關心 **當前連線數**，但 Nginx 的 **事件驅動架構** 允許它同時處理大量連線，因此額外包含：

- `Active`：目前存活的連線數
- `Accepted`：累計接受的連線數
- `Handled`：實際處理的連線數（通常與 Accepted 相等）
- `Requests`：總請求數

#### 位置

- Method: ==Get==
- URL: ==/api/server/nginx==

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
  "Connections": {
    "Active": Int,  // 當前活動連線數
    "Accepted": Int,  // 總共接受的連線數
    "Handled": Int,  // 已處理的連線數
    "Requests": Int   // 總請求數
  },
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
        "Worker_Id": Int, // Nginx 多進程運行時的 Worker ID
        "Client": String, // 發送請求的 IP 和 Port
        "Message": String,
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
            "Min": Int,
          }
        },
        "Method": String, // 請求方法 如 GET、POST
        "URL": String, // 客戶端請求的 URL
        "Protocol": String, // 協議版本
        "Status": Int, // HTTP 狀態碼
        "Byte": Int, // 回應大小
        "Referer": String, // 來源網站
        "User_Agent": String, // 瀏覽器或 API 客戶端資訊
        "Upstream": String, // 反向代理時的後端伺服器位址
        "Request_Time": float, // 處理請求所花的時間（秒）
        "Upstream_Response_Time": float, // 反向代理請求的後端響應時間
      } // ...
    ],
    "Acclength": Access_log.len,
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/nginx/action/start==

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
- URL: ==/api/server/nginx/action/stop==

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
- URL: ==/api/server/nginx/action/restart==

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
