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
- [x] 將toml添加進CA中
- [x] mini-controller 的連線與配置文件設定
- [x] 將發布出去的憑證添加到資料庫中
- [ ] 憑證資料庫可以使用(toml、sqlite)來保存
- [ ] 將CRL 檢查、生成RSA金鑰對之代碼，抽離成一個新的crate 來提供給其他apps 使用
- [x] Web Init 認證添加
- [ ] 添加clap 以支持終端參數
- [ ] 將密碼以argon2 crate hash 之後保存在config 中
- [x] 添加除了sign 之外的gRPC 
- [ ] miniController 先產生UUID之後先創憑證，創好之後，在開啟webServer, 等到controller來連線的時候順便交換UUID
- [ ] 會從config中讀取hostname之後傳給Controller，由Controller 去DNS註冊
- [ ] 與Controller需改用雙向通訊
### CRL
- [x] grpc 的部分

## Controller
- [x] 與mCA註冊成為第一台controller，並開始gRPC服務，在與mCA連線時會交換UUID
- [ ] RestFulApi 設計
- [ ] 將原本從mDNS中產生UUID的拉到Controller來產生，只要後面有添加進叢集的自動分配UUID，Controller也同時會記錄
- [ ] 後面再需要簽發憑證時會一併寫入UUID進SNI,
- [ ] 第一次的時候，會先取得mCA的Hostname去mDNS註冊，第二次之後每次連線就會檢查hostname是否有變更，有變更就去mDNS中變更
- [ ] 與mCA需改用雙向通訊
- [ ] 使用postgesSQL,或是sqlite或記憶體中(podman container)保存添加過叢集裝置

## mDNS
- [ ] 將每個dns server ip 寫入每個Service Config
- [ ] 重新將DNS 可能需要的欄位重新統整，
- [ ] 移除UUID產生，並且多一個UUID欄位來註冊新的主機名。
## Agent
