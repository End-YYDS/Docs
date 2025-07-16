    ## RestfulApi :

## Module

### 取得模組清單

#### 位置

- Method: ==Get==
- URL: ==/api/chm/setting/module==

#### 參數

無參數

#### 回傳

```json
{
  "Modules": {
    "module01": {
      "Name": String,
      "Version": String,
      "Loadstatus": enum (Load or Notload),
      "Enablestatus": enum (Enable or Disable),
    },
    "module02": {
      "Name": String,
      "Version": String,
      "Loadstatus": enum (Installed or Notinstall),
      "Enablestatus": enum (Enable or Disable),
    },
  },
  "Length": Modules.len,
},
```

### 加載模組

模組是個file(.zip)。
上傳模組檔案到後端，並由後端加載並啟用。
可以多個模組一起加載

#### 位置

- Method: ==Post==
- URL: ==/api/chm/setting/module==

#### 參數

```json
{
  "Modules": [file],
},
```

#### 回傳

回傳成功加載、加載失敗的模組名稱有哪些。

```json
{
  "Module": {
    "Load": [String],
    "Notload": [String],
    "Load_Length": Load.len,
    "Notload_Length": Notload.len,
  },
},
```

### 更新整個模組

update模組的版本。

#### 位置

- Method: ==Put==
- URL: ==/api/chm/setting/module==

#### 參數

更改整筆內容。

```json
{
  "Modules": [file],
}
```

#### 回傳

回傳是否成功

```json
{
  "Module": {
    "Success": [String],
    "Fail": [String],
    "Success_Length": Success.length,
    "Fail_Length": Fail.length,
  },
},
```

### 針對模組自己本身的設定做更新

更改模組本身的setting 跟配置，每個模組的config不會一樣。

#### 位置

- Method: ==Patch==
- URL: ==/api/chm/setting/module==

#### 參數

```json
{
  "Modules": file,
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

### 刪除模組

可以多個模組一起刪除

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/setting/module==

#### 參數

```json
{
  "Modules": [file],
},
```

#### 回傳

回傳是否成功

```json
{
  "Module": {
    "Delete": [String],
    "Notdelete": [String],
    "Delete_Length": Delete.length,
    "Notdelete_Length": Notdelete.length,
  },
},
```

### 模組啟用

#### 位置

- Method: ==Post==
- URL: ==/api/chm/setting/module/action/enable==

#### 參數

```json
{
  "Modules": [String],
},
```

#### 回傳

回傳是否成功

```json
{
  "Module": {
    "Success": [String],
    "Fail": [String],
    "Success_Length": Success.length,
    "Fail_Length": Fail.length,
  },
},
```

### 模組停用

#### 位置

- Method: ==Post==
- URL: ==/api/chm/setting/module/action/disable==

#### 參數

```json
{
  "Modules": [String],
},
```

#### 回傳

回傳是否成功

```json
{
  "Module": {
    "Success": [String],
    "Fail": [String],
    "Success_Length": Success.length,
    "Fail_Length": Fail.length,
  },
},
```

## IP Access Control

### 取得IP Access Control表單

只限制IP，不限制user進入。

#### 位置

- Method: ==Get==
- URL: ==/api/chm/setting/ip==

#### 參數

無參數

#### 回傳

預設全部的IP都能進入。

```json
{
  "Mode": enum (None),
  "Lists": None,
},
```

開白名單

```json
{
  "Mode": enum (White),
  "Lists": {
    "did01": {
      "Name": String,
      "Ip": String,
    },
    "did02": {
      "Name": String,
      "Ip": String,
    },
  },
},
```

開黑名單

```json
{
  "Mode": enum (Black),
  "Lists": {
    "did01": {            //did是database裡的id
      "Name": String,
      "Ip": String,
    },
    "did02": {
      "Name": String,
      "Ip": String,
    },
  },
},
```

### 新增IP

可以選擇要新增至黑名單或是白名單。

#### 位置

- Method: ==Post==
- URL: ==/api/chm/setting/ip==

#### 參數

```json
{
  "Mode": enum (White, Black),
  "Name": String,
  "Ip": String,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 刪除IP

可選擇要從黑名單或是白名單刪除。

#### 位置

- Method: ==Delete==
- URL: ==/api/chm/setting/ip==

#### 參數

```json
{
  "Mode": enum (White, Black),
  "Did": id,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

## 設定警告數值

### 取得所有設定值

初始值為0

#### 位置

- Method: ==Get==
- URL: ==/api/chm/setting/values==

#### 參數

無參數

#### 回傳

```json
{
  // "Temperature": Float,
  "Cpu_usage": Float,
  "Disk_usage": Float,
  "Memory": Float,
  "Network": Float,
},
```

### 更改監控數值

更改單一的也整筆更新。

#### 位置

- Method: ==Put==
- URL: ==/api/chm/setting/values==

#### 參數

```json
{
  "Cpu_usage": Float,
  "Disk_usage": Float,
  "Memory": Float,
  "Network": Float,
},
```

#### 回傳

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

## Backup config
