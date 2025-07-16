身份認證（Basic Authentication)

Dashboard 介面修改：![[X CPU.jpeg]]

若訊號不佳 數值傳送中時 以容器為單位顯示 loading： ![[X CPU 2.jpeg]]

info區：三格（safe綠、warn黃、dang紅） 點擊格子任意位置進入 List頁面
cluster區（叢集，所有主機取平均）：包含CPU折線圖、Memory折線圖、Disk長條圖

剛載入時 折線圖只有一點 隨時間增加並繪製成折線圖

因為需要連線的主機可能達上百台，所以將使用 ajax 定時更新頁面
頁面載入時 Get 取得以上 6 個數值，回傳格式如下（以下所有 send, return 均為 Json 檔）：

## Restful api :

### 取得所有資訊

#### 位置

- Method: ==Get==
- URL: ==/api/info/getAll==

#### 參數

無參數

#### 回傳

```json
{
  "Info": {
    "Safe": Int, // 幾台電腦
    "Warn": Int, // 幾台電腦
    "Dang": Int, // 幾台電腦
  },
  "Cluster": {
    "Cpu": float,
    "Memory": float,
    "Disk": float,
  },
},
```

### 取得資訊

若需向後端索取特定數值，使用 Post 方法，格式如下
zone 包含 info/ cluster
target 包含 safe/ warn/ dang/ Cpu/ Memory/ Disk
id 傳 -1 表索取全部數據 正整數表第幾台主機
回傳包含 所有主機的 id, CPU, Memory, Disk ，以及主機總數

#### 位置

- Method: ==Post==
- URL: ==/api/info/get==

#### 參數

```json
{
  //target = "info.safe, info.warn, info.dang, cluster.Cpu, cluster.Memory, cluster.Disk"
  "Zone": "info",
  "Target": "safe",
  "Uuid": (-1) if all data
},
```

#### 回傳

```Json
{
  "Pcs": {
    "uuid": {
      "Cpu": float,
      "Memory": float,
      "Disk": float,
    }, …
  },
  "Length": Pcs.len,
}
//Pcs.id.Cpu
```

### 全域設定

使用者可在全域設定調整向後端請求數據的頻率，也是頁面更新頻率。

#### 位置

- Method: ==Get==
- URL: ==/api/config/==

#### 參數

```json
{
  "Name": "ReloadRate",
},
```

#### 回傳

```json
{
  "ReloadRate": Int,
},

Config {
  "ReloadRate",
  … // 待增加
},
```

### List頁面

主機名稱若過長會省略
超過螢幕長度以卷軸表示

![[X CPU 3.jpeg]]
