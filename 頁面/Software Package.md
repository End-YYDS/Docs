## RestfulApi :

### 取得軟體清單

#### 位置

- Method: ==Get==
- URL: ==/api/software==

#### 參數

無參數

#### 回傳

```json
{
  "Pcs":{
    "uuid":{
      "Packages": {
        "package01": {
          "Version": String,
          "Status": enum (Installed or Notinstall),
        },
        "package02": {
          "Version": String,
          "Status": enum (Installed or Notinstall),
        },
      },
    }, …
  },
},
```

### 安裝軟體套件

新增套件

#### 位置

- Method: ==Post==
- URL: ==/api/software==

#### 參數

```json
{
  "uuid": [String],
  "Packages": [String],
},
```

#### 回傳

回傳是否成功
如果在內部database找不到就裝類似的，再回傳訊息說安裝了什麼軟件

```json
{
  "Packages": {
    "package01": {
      "Installed": [uuid],
      "Notinstalled": [uuid]
    },
  },
  "Length": Packages.len,
},
```

### 刪除

#### 位置

- Method: ==Delete==
- URL: ==/api/software==

#### 參數

```json
{
  "uuid": [String],
  "Package": [String],
}
```

#### 回傳

回傳是否成功

```json
{
  "Packages": {
    "package01": {
      "Installed": [uuid],
      "Notinstalled": [uuid]
    },
  },
  "Length": Packages.len,
},
```

### 更新(待定

{{說明這個api的用途}}

#### 位置

- Method: =={{選擇需要的方法}}==
- URL: =={{主路由 Ex: /api/{{test}}/}}==

#### 參數

{{需要傳遞給後端的參數，以Json為主}}

#### 回傳

{{期望從後端收到什麼資訊}}
