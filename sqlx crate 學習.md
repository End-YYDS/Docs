## 使用終端建立預設的DataBase
### 安裝sqlx-cli
```shell
cargo install sqlx-cli
```

### 創建資料庫檔案
```shell
export DATABASE_URL="sqlite:<test.db>" # 名字隨便取
sqlx db create
```

### 創建遷移資料
```shell
sqlx migrate add -r <anyname>
```

### 編寫up.sql & down.sql

### 執行遷移
```shell
sqlx migrate run
```

### 查看遷移詳細
```shell
sqlx migrate info
```

### Prepare 
```
cargo sqlx prepare
```