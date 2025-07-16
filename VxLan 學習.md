## VxLan創建
```shell
ip link add vxlan10 type vxlan id 10 dev ens3 remote {Remote IP} dstport 4789
```
## VxLan固定配置
```yaml
network:
  version: 2
  ethernets:
    ens3:
      match:
        macaddress: "0c:73:49:0b:00:00" # 根據網卡做變更
      dhcp4: no # 關閉DHCP v4
      dhcp6: no # 關閉DHCP v6
      set-name: "ens3" 設定網卡位置
      addresses:
        - 10.0.0.5/24
      routes:
        - to: default
          via: 10.0.0.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
  vlans: {}
  tunnels:
    vxlan10:
      mode: vxlan
      id: 20
      remote: 10.0.0.10
      port: 4789
      link: ens3
      addresses:
        - 10.10.10.1/24
```

## VxLan 防火牆配置
## 關閉所有介面回應ICMP, 或是Ping
檔案： `/etc/ufw/before.rules`
在ok icmp 下，全部註解
```shell
# ok icmp codes for INPUT**
#-A ufw-before-input -p icmp --icmp-type destination-unreachable -j ACCEPT
#-A ufw-before-input -p icmp --icmp-type time-exceeded -j ACCEPT
#-A ufw-before-input -p icmp --icmp-type parameter-problem -j ACCEPT
#-A ufw-before-input -p icmp --icmp-type echo-request -j ACCEPT
```
添加對於VxLan Ping Request or Reply
```shell
# vxlan10 Ping request
-A ufw-before-input -i {{ vxlan10 }} -p icmp --icmp-type echo-request -j ACCEPT
-A ufw-before-output -o {{ vxlan10 }} -p icmp --icmp-type echo-reply -j ACCEPT
```
### 關閉所有除了VxLan之外的進入
```shell
ufw default deny incoming
ufw default allow outgoing
ufw allow proto udp to any port 4789 comment 'Allow VxLan'
```

## nftables Config
```shell
#!/usr/sbin/nft -f

  

flush ruleset

  

# define ACCEPT_TCP_PORTS = {}

# define ACCEPT_UDP_PORTS = {}

  

table inet filter {

chain input {

type filter hook input priority filter; policy drop;

iif "lo" accept

ct state established,related accept

ct state invalid

# tcp dport $ACCEPT_TCP_PORTS accept

# udp dport $ACCEPT_UDP_PORTS accept

icmp type {

echo-request,

destination-unreachable,

time-exceeded,

parameter-problem

} accept

udp sport 67 udp dport 68 accept

# ip daddr {224.0.0.251,239.255.255.250} udp dport {5353,1900} accept

limit rate 3/minute log prefix "[DROP] " drop

}

chain forward {

type filter hook forward priority filter; policy drop;

}

chain output {

type filter hook output priority filter; policy accept;

# oif "lo" accept

# ct state established,related accept

}

}
```