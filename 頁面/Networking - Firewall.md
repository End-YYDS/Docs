## RestfulApi :

### 取得所有主機

#### 位置

- Method: ==Get==
- URL: ==/api/firewall/pcs==

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

### 取得單一防火牆狀態

#### 位置

- Method: ==Get==
- URL: ==/api/firewall==

#### 參數

```Json
{
  "Uuid": String
}
```

#### 回傳

```Json
{
  "Status": enum(active|inactive),
    "Chains": [
      {
        "Name": "INPUT",
        "Policy": enum(ACCEPT|DROP|REJECT), // 預設策略
        "Rules": [
          {
              "Target": enum(ACCEPT|DROP|REJECT),
              "Protocol": String,
              "In": String, // 進入的網路介面（例如 eth0 代表外部網卡）
              "Out": String, // 送出的網路介面（* 代表不限）
              "Source": String, // 封包的來源 IP
              "Destination": String, // 目標IP
              "Options": String // 其他選項
            },
            { // example: 拒絕 192.168.1.100 試圖透過 `eth0` 連接到 SSH
              "Target": "DROP",
              "Protocol": "tcp",
              "In": "eth0",
              "Out": "*",
              "Source": "192.168.1.100",
              "Destination": "0.0.0.0/0",
              "Options": "tcp dpt:22" //`tcp dpt:22` 代表 TCP port 22，即SSH服務
            }, //...
        ],
        "Rules_Length": Rules.len
      },
      {
        "Name": "FORWARD",
        "Policy": enum(ACCEPT|DROP|REJECT), // 預設策略
        "Rules": {
          "id01": {
              "Target": enum(ACCEPT|DROP|REJECT),
              "Protocol": String,
              "In": String, // 進入的網路介面（例如 eth0 代表外部網卡）
              "Out": String, // 送出的網路介面（* 代表不限）
              "Source": String, // 封包的來源 IP
              "Destination": String, // 目標IP
              "Options": String // 其他選項
            }, //...
          },
          "Rules_Length": Rules.len
      },
      {
        "Name": "OUTPUT",
        "Policy": enum(ACCEPT|DROP|REJECT), // 預設策略
        "Rules": {
          "id01": {
              "Target": enum(ACCEPT|DROP|REJECT),
              "Protocol": String,
              "In": String, // 進入的網路介面（例如 eth0 代表外部網卡）
              "Out": String, // 送出的網路介面（* 代表不限）
              "Source": String, // 封包的來源 IP
              "Destination": String, // 目標IP
              "Options": String // 其他選項
            }, //...
          },
          "Rules_Length": Rules.len
      }
  ]
}
```

### 新增防火牆規則

#### 位置

- Method: ==Post==
- URL: ==/api/firewall/rule==

#### 參數

```Json
{
  "Uuid": String, // 主機 ID
  "Chain": enum(INPUT|FORWARD|OUTPUT),
  "Target": enum(ACCEPT|DROP|REJECT),
  "Protocol": String,
  "In": String,
  "Out": String,
  "Source": String,
  "Destination": String,
  "Options": String
}
```

#### 回傳

規則是否新增成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 刪除防火牆規則

#### 位置

- Method: ==Delete==
- URL: ==/api/firewall/rule==

#### 參數

```Json
{
  "Uuid": String, // 主機 ID
  "Chain": enum(INPUT|FORWARD|OUTPUT),
  "RuleId": Int // 要刪除的規則索引
}
```

#### 回傳

規則是否刪除成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 修改防火牆狀態（啟用/停用）

#### 位置

- Method: ==Put==
- URL: ==/api/firewall/status==

#### 參數

```Json
{
  "Uuid": String,
  "Status": enum(active|inactive)
}
```

#### 回傳

規則是否修改成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

### 修改預設策略（Policy）

#### 位置

- Method: ==Put==
- URL: ==/api/firewall/policy==

#### 參數

```Json
{
  "Uuid": String,
  "Chain": enum(INPUT|FORWARD|OUTPUT),
  "Policy": enum(ACCEPT|DROP|REJECT)
}
```

#### 回傳

policy是否修改成功

```json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```
