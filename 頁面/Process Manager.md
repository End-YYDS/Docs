## RestfulApi :

### 取得所有電腦的 Process

#### 位置

- Method: ==Get==
- URL: ==/api/process/all==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs":{
    "uuid": {
      "Hostname": String,
      "Process": {
        "pname": {
          // "Description"
          "Status": Boolean,
          "Boot": Boolean
        }, ...
      },
      "Length": Process.len,
    }, ...
  },
  "Length": Pcs.len,
},
```

### 取得單一電腦的 Process

#### 位置

- Method: ==Post==
- URL: ==/api/process/one==

#### 參數

```Json
{
  "Uuid": String
}
```

#### 回傳

```json
{
  "Process": {
    "pname": {
      // "Description"
      "Status": Boolean,
      "Boot": Boolean
    }, ...
  },
  "Length": Process.len,
},
```

### 設定Process啟動

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/start==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process停止

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/stop==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process重新啟動

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/restart==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process開機自動開始

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/enable==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process開機時不自動開始

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/disable==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process開機自動開始 且 Process立即開始

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/start_enable==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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

### 設定Process開機時不自動開始 且 Process立即停止

#### 位置

- Method: ==Post==
- URL: ==/api/process/action/stop_disable==

#### 參數

```json
{
  "Uuid": String,
  "Process": String,
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
