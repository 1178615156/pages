`kmod-wireguard` 这个是没有arm64版本的,就算`yum`安装成功了也不能正常运行的,`wireguard`需要手动编译才行

### go
```
wget https://dl.google.com/go/go1.17.3.linux-amd64.tar.gz
rm -rf /usr/local/go && tar -C /usr/local -xzf go1.17.3.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```
### 编译和安装wireguard-go
```
git clone https://github.com/WireGuard/wireguard-go
cd  wireguard-go

make && make install
```

### 编译和安装wireguard-tools
```
git clone https://github.com/WireGuard/wireguard-tools
cd wireguard-tools
cd src && make && make install
```
### 设施使用wireguard-go 而非默认的内核模块
```
export WG_QUICK_USERSPACE_IMPLEMENTATION=wireguard-go
export WG_SUDO=1
```

### 测试
```
wg 
wg-quick up wg0
```
