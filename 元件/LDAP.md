## 安裝LDAP
```shell
sudo apt update && sudo apt upgrade -y
sudo apt install slapd ldap-utils -y
```
### 配置slapd
```shell
sudo dpkg-reconfigure slapd
```
- **Omit OpenLDAP server configuration?** → No
- **DNS domain name:** `example.com` → `dc=example,dc=com`
- **Organization name:** `Example Inc`
- **Administrator password:** 自訂強密碼
- **Database backend:** MDB
- **Remove database when purged?** → No
- **Move old database?** → Yes
### 驗證 slapd 執行狀態 & 基本查詢
```shell
sudo systemctl status slapd
ldapsearch -x -LLL -H ldap://localhost -b dc=example,dc=com
```
確認服務為 `active (running)`，並能成功回傳 Base DN 條目。
## 檢查是否支持Argon2
```shell
ls /usr/lib/ldap | grep -E 'argon2|pw-argon2'
```

## 開啟Argon2加密hash
setting.ldif
```ldif
dn: cn=module{0},cn=config
changetype: modify
add: olcModuleLoad
olcModuleLoad: argon2

dn: olcDatabase={-1}frontend,cn=config
changetype: modify
add: olcPasswordHash
olcPasswordHash: {ARGON2}
```
### 應用setting.ldif
```shell
ldapmodify -Y EXTERNAL -H ldapi:/// -f setting.ldif
```

### 檢查是否啟用成功

```shell
ldapsearch -Y EXTERNAL -H ldapi:/// -b cn=module{0},cn=config  -LLL  olcModuleLoad
ldapsearch -Y EXTERNAL -H ldapi:/// -b olcDatabase={-1}frontend,cn=config -LLL olcPasswordHash
```

### 系統中的Argon2測試
```shell
slappasswd -o module-load=argon2 -h '{ARGON2}' -s MySecretPassword
```
如果看到開頭=={ARGON2}==及成功

## 帳號
### 創建OU
add_ou1.ldif
```ldif
dn: ou=People,dc=example,dc=com
objectClass: organizationalUnit
ou: People
```
```shell
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f add_ou1.ldif
```
### 創建帳號
add_user1.ldif
```ldif
dn: uid=user1,ou=People,dc=example,dc=com
objectClass: inetOrgPerson
cn: User One
sn: One
uid: user1
userPassword: password123
```
```shell
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f add_user1.ldif
```

### 刪除帳號
```shell
ldapdelete -x -D "cn=admin,dc=example,dc=com" -W "uid=user1,ou=People,dc=example,dc=com"
```

### 查詢帳號
```shell
ldapsearch -x -LLL \
  -D "cn=admin,dc=example,dc=com" -W \
  -b "ou=People,dc=example,dc=com" \
  "(uid=user1)" userPassword
```

### 重新使用Argon2 hash 
```shell
ldappasswd -x -D "cn=admin,dc=example,dc=com"  -W  -S "uid=user1,ou=People,dc=example,dc=com"
```