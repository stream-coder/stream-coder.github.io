虚拟机的安装先跳过，本文介绍如何在安装好的虚拟机中如何把默认的基于dhcp分配ip的模式，改成使用静态ip。

#获取需要的信息

配置静态IP之前除了要知道希望配置的静态IP还需要知道另外三个信息：虚拟机中静态IP绑定的网卡、子网掩码、和DNS。下面先介绍如何获取这三个信息。

## 虚拟机中静态IP绑定的网卡

使用ifconfig命令可以查看系统的网络信息，如下图中的ens33和lo就是系统的两个网卡。这里我们把静态ip绑定在ens33上。

![image-20190919150517967](https://tva1.sinaimg.cn/large/006y8mN6ly1g74ualdq2sj30ij0a70v0.jpg)

## 子网掩码



## DNS（重要）

从【系统偏好设置】【网络】，选择上网的网卡，点【高级】，切换到【DNS】页，即可看到本机的DNS

![image-20190922225630513](https://tva1.sinaimg.cn/large/006y8mN6ly1g78orzuwljj30zn0u044o.jpg)

![image-20190922225700812](https://tva1.sinaimg.cn/large/006y8mN6ly1g78osbg23rj31020rwnez.jpg)

# 修改虚拟机配置

编辑配置文件

```shell
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```

添加如下配置

```shell
IPADDR=192.168.235.128
NETMASK=255.255.255.0
GATEWAY=192.168.235.2
DNS1=192.168.1.1
DNS2=192.168.0.1
```



![image-20190922230650344](https://tva1.sinaimg.cn/large/006y8mN6ly1g78p2ion4dj31180muk0l.jpg)

# 重启网络

```shell
service network restart
```

验证

```shell
ping www.baidu.com
```

能ping通就表示已经配置好了







