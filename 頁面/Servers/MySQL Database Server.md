## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/mysql==

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
  "Connections": Int, // 目前活躍的資料庫連線數
  "Databases": Int, // 資料庫數量
  "Queries_per_sec": float, // 每秒查詢數
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
    "Query_log": [
      {
        "Ip": String,
        "Date":{
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "User": String, // 執行查詢的使用者
        "Database": String, // 執行查詢的資料庫名稱
        "Query": String, // SQL 查詢語句
        "Query_Type": enum (SELECT|INSERT|UPDATE|DELETE|CREATE|DROP|ALTER), // SQL 操作類型
        "Duration_ms": Int, // 執行時間（毫秒）
        "Status": enum (Success|Error|Timeout), // 查詢執行結果
        "Affected_Rows": Int // 影響的資料行數
      } // ...
    ],
    "Querylength": Query_log.len
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/mysql/action/start==

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
- URL: ==/api/server/mysql/action/stop==

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
- URL: ==/api/server/mysql/action/restart==

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
