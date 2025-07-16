#### Sidebar 包含：

[[Apache Webserver]]
[[Nginx]]
[[BIND DNS Server]]
[[DHCP Server]]
[[LDAP Server]]
[[MySQL Database Server]]
[[PostgreSQL Database Server]]
[[ProFTPD Server]]
[[Samba Windows File Sharing]]
[[Squid Proxy Server]]
[[SSH Server]]

## RestfulApi :

點進 Sidebar 中其中一個 server 後

### 取得已安裝某 server 的所有電腦

#### 位置

- Method: ==Get==
- URL: ==/api/servers/installed==

#### 參數

```Json
{
  "Server": String,
}
```

#### 回傳

```Json
{
  "Pcs": {
    "uuid": {
      "Hostname": String,
      "Status": enum (active|stopped),
      "Cpu": float,
      "Memory": float,
    }, …
  },
  "Length": Pcs.len,
}
```

### 取得未安裝某 server 的所有電腦

#### 位置

- Method: ==Get==
- URL: ==/api/servers/noinstall==

#### 參數

```Json
{
  "Server": String,
}
```

#### 回傳

```Json
{
  "Pcs": {
    "uuid": {
      "Hostname": String,
      "Status": enum (active|stopped),
      "Cpu": float,
      "Memory": float,
    }, …
  },
  "Length": Pcs.len,
}
```

### 安裝 server

#### 位置

- Method: ==Post==
- URL: ==/api/servers/install==

#### 參數

```Json
{
  "Server": String,
  "Uuids": [String],
}
```

#### 回傳

```Json
{
  "Type": enum (OK or ERR),
  "Message": String,
},
```

- 檢測所有電腦 有哪些server
  對單一電腦做設定
