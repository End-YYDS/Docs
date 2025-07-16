- Config 特化，針對不同Role(Controller, Agent等等)
- RestAPI 接收前端Request，向後端發送gRPC 可以在同一台電腦上，或是不同電腦上

## WorkSpace
- 等mCA開發完之後回Develop 編輯Workspace的Cargo.toml 添加
```toml
[profile.release]
lto = true
strip = "symbols"   # 等价于 strip = true
codegen-units = 1
panic = "abort"
opt-level = 3
```
## mCA
 - 將toml添加進CA中
 - mini-controller 的連線與配置文件設定 (O)
 - 將發布出去的憑證添加到資料庫中 (O)
- 憑證資料庫可以使用(toml、sqlite)來保存(^)
- 將CRL 檢查、生成RSA金鑰對之代碼，抽離成一個新的crate 來提供給其他apps 使用(^)
- Web Init 認證添加 (O)
- 添加clap 以支持終端參數
- 將密碼以argon2 crate hash 之後保存在config 中(X)
- 添加除了sign 之外的gRPC 
### CRL
- grpc 的部分

## Controller
- 與mCA註冊成為第一台controller，並開始gRPC服務(o)

## mDNS
- 將每個dns server ip 寫入每個Service Config
- 重新將DNS 可能需要的欄位重新統整，
## Agent
