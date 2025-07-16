## RestfulApi :

在 Apache Webserver 頁面中，點進單一電腦後

### 伺服器狀態監控

#### 位置

- Method: ==Get==
- URL: ==/api/server/ldap==

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
  "Connections": Int, // 目前連線數
  "Entries": Int, // 目前 LDAP 內的條目數
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
    "Access_log": [
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
        "Method": enum (BIND|SEARCH|ADD|DELETE|MODIFY|MODDN|COMPARE|UNBIND|EXTENDED), // LDAP 操作類型
        "Base_DN": String, // 操作的基準 DN（Distinguished Name）
        "Filter": String, // 搜尋條件（僅 SEARCH 相關操作會有）
        "Protocol": enum (LDAPv2|LDAPv3), // 使用的 LDAP 版本
        "Status": enum (Success|AuthFailed|NotFound|Error), // 操作結果
        "Response_Time_ms": Int // LDAP 操作耗時（毫秒）
      } // ...
    ],
    "Acclength": Access_log.len
  }
}
```

### 啟動伺服器

#### 位置

- Method: ==Post==
- URL: ==/api/server/ldap/action/start==

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
- URL: ==/api/server/ldap/action/stop==

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
- URL: ==/api/server/ldap/action/restart==

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
