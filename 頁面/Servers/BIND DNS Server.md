## RestfulApi :

在 BIND DNS Server 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/bind==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

- Queries
  - `Total`（總查詢次數）：可以知道伺服器的負載情況
  - `NXDOMAIN`（無此網域）：如果此數據異常高，可能表示錯誤配置或攻擊
  - `REFUSED`（拒絕請求）：監控是否有過多的非法查詢

```json
{
  "Hostname": String,
  "Status": enum (active|stopped), // 是否正在運行
  "Cpu": float, // 佔用 CPU %
  "Memory": float, // 佔用記憶體 %
  "Connections": Int, // 目前處理的請求數量
  "Queries": {
    "Total": Int, // 總查詢次數
    "Success": Int, // 成功解析次數
    "NXDOMAIN": Int, // 查詢失敗（無此網域）次數
    "REFUSED": Int // 伺服器拒絕回應的次數
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
        "Module": String, // 出錯的模組（如 resolver、cache、zone）
        "Level": enum (debug|info|notice|warn|error|crit|alert|emerg),
        "Pid": Int, // 進程 ID
        "Client": String, // 發送查詢的 IP 和 Port
        "Message": String // 錯誤訊息
      } // ...
    ],
    "Errlength": Error_log.len,
    "Query_log": [
      {
        "Client": String, // 發送查詢的 IP 和 Port
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Query": String, // 查詢的網域名稱
        "Type": enum (A|AAAA|CNAME|MX|NS|PTR|SOA|TXT|SRV|DNSKEY), // DNS 查詢類型
        "Response": String, // 回應的 IP 或其他紀錄
        "Status": enum (NOERROR|NXDOMAIN|SERVFAIL|REFUSED), // 回應狀態
        "Duration": float // 查詢時間（毫秒）
      } // ...
    ],
    "Qrylength": Query_log.len
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/bind/action/start==

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
- URL: ==/api/server/bind/action/stop==

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
- URL: ==/api/server/bind/action/restart==

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
