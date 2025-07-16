## OpenSSL Commands
### 創建RootCA私鑰及公鑰

```shell
openssl genpkey -algorithm RSA -out rootCA.key -aes256 # 創建私鑰
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 3650 -out rootCA.crt # 創建公鑰
```

### 創建中繼憑證私鑰及公鑰
```shell
openssl genpkey -algorithm RSA -out intermediateCA.key -aes256 # 創建私鑰

openssl req -new -key intermediateCA.key -out intermediateCA.csr # 創建憑證申請請求

openssl x509 -req -in intermediateCA.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out intermediateCA.crt -days 3650 -sha256 -extfile intermediateCA.cnf -extensions v3_intermediate_ca # 使用rootCA簽署.csr 並添加額外config
```

### 創建一般憑證
```shell
openssl genpkey -algorithm RSA -out server.key -aes256 #創建一般憑證的私鑰
openssl req -new -key server.key -out server.csr #憑證申請
openssl x509 -req -in server.csr -CA intermediateCA.crt -CAkey intermediateCA.key -CAcreateserial -out server.crt -days 365 -sha256 -extfile server.cnf -extensions server_cert #使用中繼憑證簽署
openssl verify -CAfile rootCA.crt -untrusted intermediateCA.crt server.crt #檢查憑證
```

### 測試指令
```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh #安裝rust
git clone -b backend/ca --single-branch https://github.com/End-YYDS/CHM.git
sudo apt install protobuf-compiler git build-essential pkg-config libssl-dev
mkdir -p /etc/CHM
cargo run -p ca --release --bin CHM_CA -- --create-ca # 創建初始rootCA
RUST_LOG=ca=trace,tonic::transport=trace cargo run -p ca --bin CHM_CA 
# 將憑證名稱改成rootCA 或是預設，又或是先呼叫--init-config 取得預設設定文件
```

### 安裝openssl
```shell
# macOS (Homebrew)
$ brew install openssl@3

# macOS (MacPorts)
$ sudo port install openssl

# macOS (pkgsrc)
$ sudo pkgin install openssl

# Arch Linux
$ sudo pacman -S pkgconf openssl

# Debian and Ubuntu
$ sudo apt-get install pkg-config libssl-dev

# Fedora
$ sudo dnf install pkgconf perl-FindBin perl-IPC-Cmd openssl-devel

# Alpine Linux
$ apk add pkgconf openssl-dev

# openSUSE
$ sudo zypper in libopenssl-devel
```