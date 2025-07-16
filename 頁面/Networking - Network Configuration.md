## Network Interface

### 取得所有資訊

#### 位置

- Method: ==Get==
- URL: ==/api/network/net==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs":{
    "uuid":{
      "Networks": {
        "nid":{
          // "Name": String,
          "Type": enum (虛擬 or 實體),
          "Ipv4": String,
          "Netmask": String,
          "Mac": String,
          "Broadcast": String,
          "Mtu": Int, //封包大小
          "Status": enum (Up or Down) //開關啟動與否
        },...
      },
      "Length": Networks.len
    },...
  },
  "Length": Pcs.len
},
```

### 新增Network Interface

#### 位置

- Method: ==Post==
- URL: ==/api/network/net==

#### 參數

```json
{
  "Nid": String,
  "Type": enum (虛擬 or 實體),
  "Ipv4": String,
  "Netmask": String,
  "Mac": String,
  "Broadcast": String,
  "Mtu": Int,
  "Status": enum (Up or Down)
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 刪除Network Interface

#### 位置

- Method: ==Delete==
- URL: ==/api/network/net==

#### 參數

```json
{
  "Nid": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 編輯單一項目

#### 位置

- Method: ==Patch==
- URL: ==/api/network/net==

#### 參數

```json
{
  "Type": enum, // 底下項目
  // "Type": enum (虛擬 or 實體),
  // "Ipv4": String,
  // "Netmask": String,
  // "Mac": String,
  // "Broadcast": String,
  // "Mtu": Int,
  // "Status": enum (Up or Down)
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 編輯整筆項目

#### 位置

- Method: ==Put==
- URL: ==/api/network/net==

#### 參數

```json
{
  "Type": enum (虛擬 or 實體),
  "Ipv4": String,
  "Netmask": String,
  "Mac": String,
  "Broadcast": String,
  "Mtu": Int,
  "Status": enum (Up or Down)
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 啟動Network Interface

#### 位置

- Method: ==Post==
- URL: ==/api/network/net/action/up==

#### 參數

```json
{
  "Nid": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 關閉Network Interface

#### 位置

- Method: ==Post==
- URL: ==/api/network/net/action/down==

#### 參數

```json
{
  "Nid": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

## Routing and Gateways

### 取得路由表資訊

#### 位置

- Method: ==Get==
- URL: ==/api/network/route==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs":{
    "uuid":{
      "Routes": {
        "destination":{
          "Via": String, //下一個要接收的封包是誰
          "Dev": String, //裝置
          "Proto": String, //來源
          "Metric": Int, //優先度 數值越低優先度越高
          "Scope": String, //虛擬網卡
          "Src": String, //路由來源ip
        },...
      },
      "Length": Routes.len,
    },...
  },
  "Length": Pcs.len
},
```

### 新增router

#### 位置

- Method: ==Post==
- URL: ==/api/network/route==

#### 參數

```json
{
  "Destination": String,
  "Via": String,
  "Dev": String,
  "Proto": String,
  "Metric": Int,
  "Scope": String,
  "Src": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 刪除router

#### 位置

- Method: ==Delete==
- URL: ==/api/network/route==

#### 參數

```json
{
  "Destination": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 編輯單一項目

#### 位置

- Method: ==Patch==
- URL: ==/api/network/route==

#### 參數

```json
{
  "Destination": String,
  "Type": enum, // 底下項目
  // "Via": String,
  // "Dev": String,
  // "Proto": String,
  // "Metric": Int,
  // "Scope": String,
  // "Src": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 編輯整筆項目

#### 位置

- Method: ==Put==
- URL: ==/api/network/route==

#### 參數

```json
{
  "Destination": String,
  "Via": String,
  "Dev": String,
  "Proto": String,
  "Metric": Int,
  "Scope": String,
  "Src": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

## Hostname and DNS Client

### 取得所有資訊

#### 位置

- Method: ==Get==
- URL: ==/api/network/dns==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs": {
    "uuid": {
      "Hostname": String,
      "DNS": {
        "Primary": String,
        "Secondary": String,
      },
    },
  },
},
```

### 更改Hostname

#### 位置

- Method: ==Patch==
- URL: ==/api/network/dns==

#### 參數

```json
{
  "Uuid": String, // hostname
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 更改DNS Server IP

#### 位置

- Method: ==Put==
- URL: ==/api/network/dns==

#### 參數

若只改了Primary，Secondary直接沿用取得到的舊資訊。

```json
{
  "Primary": String,
  "Secondary": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
