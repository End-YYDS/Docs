### 取得所有使用者資訊

#### 位置

- Method: ==Get==
- URL: ==/api/chm/user==

#### 參數

無參數

#### 回傳

```json
{
  "Users": {
    "uid01":{
      "Username": String,
      "Group": [String],
      "Home_directory": String,
      "Shell": String,
    },
  },
  "Length": Users.len,
},
```

### 新增User

#### 位置

- Method: ==Post==
- URL: ==/api/chm/user==

#### 參數

```json
{
  "Username": String,
  "Group": [String],
  "Home_directory": String,
  "Shell": String,
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

### 更新整筆User

#### 位置

- Method: ==Put==
- URL: ==/api/chm/user==

#### 參數

更改整筆內容。

```json
{
  "uid01":{
    "Username": String,
    "Group": [String],
    "Home_directory": String,
    "Shell": String,
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

### 更新User單一內容

#### 位置

- Method: ==Patch==
- URL: ==/api/chm/user==

#### 參數

只更改其中一個欄位。

```json
{
  "uid01":{
    "Username": String,
    //"Group": [String],
    //"Home_directory": String,
    //"Shell": String,
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

### 刪除User

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/user==

#### 參數

```json
{
  "uid": id
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

### 取得所有群組資訊

#### 位置

- Method: ==Get==
- URL: ==/api/chm/group==

#### 參數

無參數

#### 回傳

```json
{
  "Groups": {
    "gid01":{
      "Groupname": String,
      "Users": [uid.username],
      //"Permission"
    },
  },
},
//data.Groups.gid01.users
```

### 新增Group

#### 位置

- Method: ==Post==
- URL: ==/api/chm/group==

#### 參數

```json
{
  "Groupname": String,
  "Users": [uid.username],
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
- URL: ==/api/chm/group==

#### 參數

更改整筆內容。

```json
{
  "gid01":{
    "Groupname": String,
    "Users": [uid.username],
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
- URL: ==/api/chm/group==

#### 參數

只更改其中一個欄位。

```json
{
  "gid01":{
    "Groupname": String,
    //"Users": [uid.username],
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
- URL: ==/api/chm/group==

#### 參數

```json
{
  "gid": id
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
