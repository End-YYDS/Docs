![[Crontab UI Flow.gif]]

## RestfulApi :

### 獲取所有排程表內容

頁面初始化時取得crontab(排程表)的內容

#### 位置

- Method: ==Get==
- URL: ==/api/cron/all==

#### 參數

無參數

#### 回傳

```json
{
  "Jobs": {
    "id01":{
      "Name": String,
      "Command": String,
      "Schedule": {
        "Minute": Int,
        "Hour": Int,
        "Date": Int,
        "Month": Int,
        "Week": Int,
      },
      "Username": String,
    },
    "id02":{
      "Name": String,
      "Command": String,
      "Schedule": {
        "Minute": Int,
        "Hour": Int,
        "Date": Int,
        "Month": Int,
        "Week": Int,
      },
      "Username": String,
    }, …
  },
  "length": Jobs.len // 2
}
// Jobs.name01.Command
```

### 新增資料

添加新的一筆資料

#### 位置

- Method: ==Post==
- URL: ==/api/cron==

#### 參數

```json
{
  "Name": String,
  "Command": String,
  "Schedule": {
    "Minute": Int,
    "Hour": Int,
    "Date": Int,
    "Month": Int,
    "Week": Int,
  },
  "Username": String,
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

### 刪除

#### 位置

- Method: ==Delete==
- URL: ==/api/cron==

#### 參數

```json
{
  "id": id
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

### 更新

#### 位置

- Method: ==Put==
- URL: ==/api/cron==

#### 參數

```json
{
  "id01":{
    "Name": String,
    "Command": String,
    "Schedule": {
      "Minute": Int,
      "Hour": Int,
      "Date": Int,
      "Month": Int,
      "Week": Int,
    },
    "Username": String,
  },
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

### 匯入

#### 位置

- Method: ==Post==
- URL: ==/api/cron/action/import==

#### 參數

```json
{
  file,
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

### 匯出

#### 位置

- Method: ==Post==
- URL: ==/api/cron/action/export==

#### 參數

無參數

#### 回傳

回傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": file,
},
```
