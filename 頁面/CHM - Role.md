## RestfulApi :

### 取得所有角色

#### 位置

- Method: ==Get==
- URL: ==/api/chm/role==

#### 參數

無參數

#### 回傳

```json
{
  "Roles": {
    "RoleName": String,
    "Permissions": int, // bit operation, like 0001 (1 << 0)
    "Color": int, // 前端自存enum表（0: Blue, 1: Red...)
    "Menbers": [int], // uid
    "Length": Menbers.len,
  },
},
```

### 取得所有使用者資訊

#### 位置

- Method: ==Get==
- URL: ==/api/chm/role/users==

#### 參數

無參數

#### 回傳

```json
{
  "Users": {
    "uid01": String,
  },
  "Length": Users.len,
},
```

### 建立角色（身份組）

#### 位置

- Method: ==Post==
- URL: ==/api/chm/role==

#### 參數

```json
{
  "RoleName": String,
  "Permissions": int, // bit operation, like 0001 (1 << 0)
  "Color": int, // 前端自存enum表（0: Blue, 1: Red...)
  "Menbers": [int], // uid
  "Length": Menbers.len,
},
```

#### 回傳

角色建立是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 刪除角色

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/role==

#### 參數

```json
{
  "RoleName": String,
},
```

#### 回傳

角色刪除是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 角色配置

#### 位置

- Method: ==Put==
- URL: ==/api/chm/role==

#### 參數

```json
{
  "Role": String,
  "Members": [int], // uid
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

### 編輯角色權限

#### 位置

- Method: ==Patch==
- URL: ==/api/chm/role==

#### 參數

```json
{
  "Role": String,
  "Permissions": int, // bit operation, like 0001 (1 << 0)
  "Color": int,
},
```

#### 回傳

回傳編輯是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
