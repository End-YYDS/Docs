## RestfulApi :

在 DHCP Server 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/dhcp==

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
  "Leases": Int, // 目前 DHCP 伺服器已分配並仍有效的 IP 租約數量
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
        "Client": String, // 請求的設備 IP（Client）
        "Message": String
      } // ...
    ],
    "Errlength": Error_log.len,
    "Lease_log": [
      {
        "Client_IP": String, // 分配的 IP
        "MAC": String, // 客戶端的 MAC 地址
        "Date": {
          "Year": Int,
          "Month": enum (Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec),
          "Day": Int,
          "Time": {
            "Hour": Int,
            "Min": Int
          }
        },
        "Action": enum (offer|ack|decline|release|inform), // DHCP 操作
        "Lease_Time": Int, // 租約時間（秒）
        "Server_IP": String, // 伺服器 IP
        "Message": String
      } // ...
    ],
    "Leaselength": Lease_log.len
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/dhcp/action/start==

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
- URL: ==/api/server/dhcp/action/stop==

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
- URL: ==/api/server/dhcp/action/restart==

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
