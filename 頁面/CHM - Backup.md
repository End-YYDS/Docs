## RestfulApi :

### 備份系統資料

立即備份

#### 位置

- Method: ==Post==
- URL: ==/api/chm/backup==

#### 參數

```Json
{
  "Type": enum: [Remote,Local],
  "Name": String,
}
```

#### 回傳

備份是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
  "File": if Type is Local
},
```

### 取得備份資料

取得近五次備份資料

#### 位置

- Method: ==Get==
- URL: ==/api/chm/backup==

#### 參數

無參數

#### 回傳

回傳檔案名稱 日期 時間

```json
{
  "Datas": [
    {
      "Name": String,
      "Date": {
        "Year": Int,
        "Month": Int,
        "Day": Int
      },
      "Time": {
        "Hour": Int,
        "Min": Int,
      }
    }, //...
  ],
  "Length": Data.len,
}
```

（統一用物件 使用方法：）

```Json
for i in data.Data:
  i.Name...
```

### 還原備份資料

#### 位置

- Method: ==Post==
- URL: ==/api/chm/backup/reduction==

#### 參數

```Json
{
  "Type": enum: [Remote,Local],
  "Name" | "File" : String, if Remote, else if Local
}
```

#### 回傳

還原是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
