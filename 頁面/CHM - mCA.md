### 取得有效憑證列表

#### 位置

- Method: ==Get==
- URL: ==/api/chm/mCA/valid==

#### 參數

無參數

#### 回傳

```json
{
  "Valid": {
    "Name": String, //通用名稱
    "Signer": String,
    "Period": String, //有效期間
  },
  "Length": Valid.len,
},
```

### 取得已吊銷憑證列表

#### 位置

- Method: ==Get==
- URL: ==/api/chm/mCA/revoke==

#### 參數

無參數

#### 回傳

```json
{
  "Revoke": {
    "Number": String, //序號
    "Time": String, //吊銷當下的時間
    "Reason": String,
  },
  "Length": Revoke.len,
},
```

### 吊銷憑證

#### 位置

- Method: ==Post==
- URL: ==/api/chm/mCA/action/revoke==

#### 參數

```json
{
  "Name": String, //通用名稱
  "Reason": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
