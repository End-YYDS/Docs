## RestfulApi :

## CHM 系統 Logs

### 取得所有 Logs

#### 位置

- Method: ==Get==
- URL: ==/api/logs/sys==

#### 參數

無參數

#### 回傳

```Json
{
  "Logs": {
    "id": {
      "Month": String,
      "Day": Int,
      "Time": {
        "Hour": Int,
        "Min": Int,
      },
      "Direction": String, // 方向 A to B
      "Type": String, // 類別
      "Messages": String,
    }, ...
  },
  "Length": Logs.len,
}
```

### 篩選條件取得 Logs

#### 位置

- Method: ==Get==
- URL: ==/api/logs/sys/query==

#### 參數

```Json
{
  "Search": enum("Month", "Day", "Time", "Direction", "Type"),
  "Parameter": String, // 參數
}
```

#### 回傳

```Json
{
  "Logs": {
    "id": {
      "Month": String,
      "Day": Int,
      "Time": String,
      "Direction": String, // 方向 A to B
      "Type": String, // 類別
      "Messages": String,
    }, ...
  },
  "Length": Logs.len,
}
```

## 取得被控端 Logs

### 取得所有主機

以供使用者選擇

#### 位置

- Method: ==Get==
- URL: ==/api/logs/pc/all==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs": {
    "uuid":  String, ... // hostname
  },
  "Length": Pcs.len,
}
//Pcs.id
```

### 取得個別被控端 Logs

#### 位置

- Method: ==Get==
- URL: ==/api/logs/pc==

#### 參數

```Json
{
  "Uuid": String,
}
```

#### 回傳

```json
{
  "Logs": {
    "id": {
      "Month": String,
      "Day": Int,
      "Time": String,
      "Hostname": String,
      "Type": String, // 類別
      "Messages": String,
    }, ...
  },
  "Length": Logs.len,
},
```

### 篩選條件取得 Logs

#### 位置

- Method: ==Get==
- URL: ==/api/logs/pc/query==

#### 參數

```Json
{
  "Uuid": String,
  "Search": enum("Month", "Day", "Time", "Hostname", "Type"),
  "Parameter": String, // 參數
}
```

#### 回傳

```Json
{
  "Logs": {
    "id": {
      "Month": String,
      "Day": Int,
      "Time": String,
      "Hostname": String,
      "Type": String, // 類別
      "Messages": String,
    }, ...
  },
  "Length": Logs.len,
}
```

- 系統內logs
  error 正常執行紀錄 有通過 controller 都要記錄 grpc restfulapi
  只要經過 controller 就會有 log
  取得每台logs
  讀系統日誌
