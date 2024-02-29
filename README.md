#  GitHub加速方法

###  方法一：

首先你需要有一个可以直连的代理，建议用外国服务器安装xui面板自建

直接开启SK5代理：```export all_proxy="socks5://用户名:密码@地址:端口"```

或者开启http代理：```export all_proxy="http://用户名:密码@地址:端口"```

此时输入```curl ip.sb```查看本机IP判断是否配置成功

#### 注意：下载文件或脚本时需要使用`sudo -E`传递环境变量才会生效


###  方法二：

适用于`Ubuntu` `Debian` `Kali Linux`系统

安装`shadowsocks-libev`

```
sudo apt update
```

```
sudo apt install shadowsocks-libev -y
```


创建一个名为`config.json`的文件配置SS节点的相关信息，建议使用`aes-256-gcm`或`aes-128-gcm`等加密算法，将以下配置添加到文件中：

```
touch /root/config.json
```

```
{
  "server": "节点地址",
  "server_port": 端口,
  "local_port": 1080,
  "password": "密码",
  "method": "加密算法"
}
```


使用以下命令启动shadowsocks-libev客户端：

```
ss-local -c /root/config.json > /dev/null 2>&1 &
```

然后就可以开启代理了：

```
export all_proxy="socks5://127.0.0.1:1080"
```



此时输入```curl ip.sb```查看本机IP判断是否配置成功

关闭终端重新连接后会自动关闭代理，重新开启SK5代理即可

#### 注意：下载文件或脚本时需要使用`sudo -E`传递环境变量才会生效

#### 相关命令

查看运行状态

```
systemctl status shadowsocks-libev
```

重启

```
systemctl restart shadowsocks-libev
```


停止

```
systemctl stop shadowsocks-libev
```

卸载

```
apt remove shadowsocks-libev
```

删除相关配置

```
apt purge shadowsocks-libev
```

### 方法三：v2rayA

## [教程地址](https://v2raya.org/docs/prologue/installation/debian/)

#### 通过apt-get安装的话，使用·apt-get remove v2raya·卸载

#### 国内Debian / Ubuntu切换apt源教程

需要root权限

先备份`sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak`

打开文件`/etc/apt/sources.list`

`ucloud`源
```
deb http://mirrors.ucloud.cn/debian/ bullseye main
deb-src http://mirrors.ucloud.cn/debian/ bullseye main
deb http://mirrors.ucloud.cn/debian-security bullseye-security main
deb-src http://mirrors.ucloud.cn/debian-security bullseye-security main
deb http://mirrors.ucloud.cn/debian/ bullseye-updates main
deb-src http://mirrors.ucloud.cn/debian/ bullseye-updates main
```

`阿里云`源

```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

# deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
# deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
# deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
# deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

## Pre-released source, not recommended.
# deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
```

`清华大学`源

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

## Pre-released source, not recommended.
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

更新源
```
sudo apt update
```

切换完成


#  PS

文件格式转换命令```mv config.txt config.json```

你也可以通过编辑```/etc/shadowsocks-libev/config.json```文件来配置SS服务端:

就是把这台服务器当节点用，需要把第一行```server```配置改为```"server":"0.0.0.0",``` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#  允许所有IP连接

配置完成后需重启 

```
sudo systemctl restart shadowsocks-libev
```

为什么使用SS，因为可以使用apt包管理器直接安装。

---
 

###  修改系统hosts文件实现加速(老方法不稳定)：

+ 文件路径：
```
windows: C:\Windows\System32\drivers\etc 
linux: /etc/hosts
```
+ 格式：
```
127.0.0.11 github.com
127.0.0.11 raw.githubusercontent.com
127.0.0.11 assets-cdn.github.com
127.0.0.11 github.global.ssl.fastly.net
```
把```127.0.0.11```替换为查询到的地址

可以从这里获取hosts地址：https://github.com/521xueweihan/GitHub520/blob/main/hosts

该内容会自动定时更新。

#### 修改 hosts 文件

hosts 文件在每个系统的位置不一，详情如下：
- Windows 系统：`C:\Windows\System32\drivers\etc\hosts`
- Linux 系统：`/etc/hosts`
- Mac（苹果电脑）系统：`/etc/hosts`
- Android（安卓）系统：`/system/etc/hosts`
- iPhone（iOS）系统：`/etc/hosts`

修改方法，把上面的内容复制到文本末尾：

1. Windows 使用记事本
2. Linux、Mac 使用 Root 权限：`sudo nano /etc/hosts`
3. iPhone、iPad 须越狱、Android 必须要 root

####  激活生效
大部分情况下是直接生效，如未生效可尝试下面的办法，刷新 DNS：

1. Windows：在CMD窗口输入：`ipconfig /flushdns`

2. Linux命令：`sudo systemctl restart nscd` 如报错则须安装：`sudo apt install nscd` 或 `sudo /etc/init.d/nscd restart`

3. Mac命令：`sudo killall -HUP mDNSResponder`

**PS：** 上述方法无效可以尝试重启机器。

###  GitHub加速网站（不会使用请谷歌） 

https://www.jsdelivr.com/github

https://ghproxy.agrayman.gay/

https://gh.api.99988866.xyz/

https://mirror.ghproxy.com/

https://gitclone.com/

https://hub.nuaa.cf/

https://github.welab.eu.org/

https://ghps.cc/
