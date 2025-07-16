# Add, Remove PC

## RestfulApi :

### 新增管理主機

#### 位置

- Method: ==Post==
- URL: ==/api/chm/pc/add==

#### 參數

```json
{
  "Ip": String, // 實體ip
  "Password": String,
},
```

#### 回傳

回傳是否成功

錯誤回傳錯誤原因：

1. 此 ip 無安裝 Agent 無法添加
2. 密碼錯誤

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 取得所有主機

#### 位置

- Method: ==Get==
- URL: ==/api/chm/pc/all==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs": {
    "uuid": {
      "Hostname": String,
      "Ip": String,
    }, …
  },
  "Length": Pcs.len,
}
//Pcs.id
```

### 取得特定主機

#### 位置

- Method: ==Get==
- URL: ==/api/chm/pc/specific==

#### 參數

```Json
{
  "Uuids": [String]
}
```

#### 回傳

```json
{
  "Pcs": {
    "uuid": {
      "Hostname": String,
      "Ip": String,
    }, …
  },
  "Length": Pcs.len,
}
//Pcs.id
```

### 刪除管理主機

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/pc==

#### 參數

```json
{
  "Uuids": [String],
  "Passwords" [String],
},
```

#### 回傳

回傳是否成功

```json
{
  "uuid":{
    "Type": enum (OK or ERR),
    "Message": String,
  }, ...
},
```

### Reboot

#### 位置

- Method: ==Post==
- URL: ==/api/chm/pc/reboot==

#### 參數

```json
{
  "Uuids": [String],
},
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### Shutdown

#### 位置

- Method: ==Post==
- URL: ==/api/chm/pc/shutdown==

#### 參數

```json
{
  "Uuids": [String],
},
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

# PC Group

## RestfulApi :

### 取得所有PC群組資訊

#### 位置

- Method: ==Get==
- URL: ==/api/chm/pcgroup==

#### 參數

無參數

#### 回傳

```json
{
  "Groups": {
    "vxlanid": { // VXLAN id
      "Groupname": String,
      "Pcs": [uuid.hostname],
    }, …
  },
  "Length": Groups.len,
}
//Pcs.id
```

### 新增Group

#### 位置

- Method: ==Post==
- URL: ==/api/chm/pcgroup==

#### 參數

```json
{
  "Groupname": String,
  "Describe": String,
},
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 更新整筆Group

#### 位置

- Method: ==Put==
- URL: ==/api/chm/pcgroup==

#### 參數

更改整筆內容。

```json
{
  "vxlanid":{
    "Groupname": String,
    "Pcs": [uuid.hostname],
  },
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

### 更新Group單一內容

#### 位置

- Method: ==Patch==
- URL: ==/api/chm/pcgroup==

#### 參數

只更改其中一個欄位。

```json
{
  "vxlanid":{
    "Groupname": String,
    //"Pcs": [uuid.hostname],
  },
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

### 刪除Group

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/pcgroup==

#### 參數

```json
{
  "vxlanid": id
},
```

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
