#  国内VPS使用代理的方法，适用于无法拉取github项目

###  方法一：

首先你需要有一个可以直连的代理，建议用外国服务器安装xui面板自建

直接开启SK5代理：```export all_proxy="socks5://用户名:密码@地址:端口"```

或者开启http代理：```export all_proxy="http://用户名:密码@地址:端口"```

此时输入```curl ip.sb```查看本机IP判断是否配置成功


###  方法二：
安装shadowsocks-libev：

```sudo apt install shadowsocks-libev```  &nbsp;&nbsp;&nbsp;&nbsp;  #  Debian/Ubuntu

```sudo yum install shadowsocks-libev```  &nbsp;&nbsp;&nbsp;&nbsp;  #  CentOS


创建一个名为```config.json```的文件配置SS节点的相关信息，建议使用aes-256-gcm或aes-128-gcm等加密算法，将以下配置添加到文件中：
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

```ss-local -c 节点文件路径 > /dev/null 2>&1 &```

然后就可以开启代理了：

```export http_proxy="socks5://127.0.0.1:1080" export https_proxy="socks5://127.0.0.1:1080"```


也可以全局模式：

```export all_proxy="socks5://127.0.0.1:1080"```



此时输入```curl ip.sb```查看本机IP判断是否配置成功

关闭终端重新连接后会自动关闭代理，重新开启SK5代理即可


也可以只用代理下载文件：

```curl --socks5 127.0.0.1:1080 http://www.example.com```


#  PS

文件格式转换命令```mv config.txt config.json```

你也可以通过编辑```/etc/shadowsocks-libev/config.json```文件来配置SS服务端:

就是把这台服务器当节点用，需要把第一行```server```配置改为```"server":"0.0.0.0",``` &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;#  允许所有IP连接

为什么用SS呢？因为apt yum pip包管理器里都内置了这些，直接安装，不用下载。

