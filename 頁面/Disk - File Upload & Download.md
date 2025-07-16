![[Admin權最大.jpeg]]

## RestfulApi :

## 實體主機

### 取得所有主機

#### 位置

- Method: ==Get==
- URL: ==/api/file/pdir/pcs==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs": {
    "uuid": String, // hostname
  },
  "Length": Pcs.len,
}
//Pcs.id
```

### 取得單一主機資料夾

#### 位置

- Method: ==Get==
- URL: ==/api/file/pdir/one==

#### 參數

```json
{
  "uuid": {
    "Directory": String, // 預設根目錄
  }
}
```

#### 回傳

```json
{
  "Files": {
    "filename": {
      "Size": float,
      "Unit": enum (B|KB|MB|GB),
      "Owner": String,
      "Mode": String,
      "Modified": String,
    }, ...
  },
  "Length": Files.len,
}
```

### 上傳檔案 ( 指定PC )

（要做進度條）

#### 位置

- Method: ==Post==
- URL: ==/api/file/pdir/action/upload==

#### 參數

```json
{
  "Uuid": String, // 目標主機 uuid
  "File": [file],
}
```

#### 回傳

上傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 下載檔案

#### 位置

- Method: ==Post==
- URL: ==/api/file/pdir/action/download==

#### 參數

```json
{
  "Uuid": String, // 目標主機 uuid
  "Filename": String,
}
```

#### 回傳

下載是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

## 虛擬目錄

### 取得虛擬目錄

#### 位置

- Method: ==Get==
- URL: ==/api/file/vdir==

#### 參數

無參數

#### 回傳

```json
{
  "Path": String,
}
```

### 上傳檔案 ( for all PC )

（要做進度條）

#### 位置

- Method: ==Post==
- URL: ==/api/file/vdir/action/upload==

#### 參數

```json
{
  "File": [file],
}
```

#### 回傳

上傳是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 下載檔案

#### 位置

- Method: ==Post==
- URL: ==/api/file/vdir/action/download==

#### 參數

```json
{
  "Filename": String,
}
```

#### 回傳

下載是否成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
