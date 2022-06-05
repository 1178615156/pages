#
## 问题排查
在K8S中运行calico-node异常:
```
calico-node pod failing to run: Bad return code from ipset list - Kernel error received: Invalid argument
```
### 可能的原因
#### calico的BUG
可以通过升级版本解决 https://github.com/projectcalico/calico/issues/5011
#### 内核缺少了ipset
在一些ARM机器上会这个问题,例如:
```
  Operating System: Ubuntu 18.04.5 LTS
            Kernel: Linux 4.9.201-tegra
      Architecture: arm64
```
这个安装ipset即可  

安装ipset之前需要安装libmnl
```
git clone git://git.netfilter.org/libmnl.git
cd libmnl && ./autogen.sh && ./configure && make && make install && cd .. 
```
接着安装ipset
```shell
git clone git://git.netfilter.org/ipset.git
cd ipset
./autogen.sh
./configure 
make
make modules 
make install
make modules_install
depmod  -a

```

**检查ipset**正常应该无返回正常
```shell
ipset list 
```
