# shadowsocks-notes

集成记录 shadowsocks 一些相关内容，包括概念、安装、使用等，避免频繁查阅。

## 主要网站

[官网](http://shadowsocks.org/en/index.html)（其实并非由原作者运营）

[GitHub 主页面](https://github.com/shadowsocks)

[一键安装脚本](https://github.com/teddysun/shadowsocks_install)

## 主要分支

- [shadowsocks](https://github.com/ziggear/shadowsocks)（或 shadowsocks-python，其它用户备份）

- [shadowsocks-go](https://github.com/shadowsocks/shadowsocks-go)

- [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)

  等

- [shadowsocksR](https://github.com/shadowsocksr-backup/shadowsocksr)（其它用户备份）

[这里](https://shadowsocks.org/en/download/servers.html)可以查看 shadowsocks 各分支含义的官方简介。

目前最活跃的分支是**shadwsocks-libev**，因此建议使用该分支。

## 一点历史

 shadowsocks 的来源、作者被请喝茶的经历、与 shadowsocksR 的关系等：

- [Shadowsocks 的前世后生](http://www.chinagfw.org/2016/08/shadowsocks_31.html)

- [最近事情有点多，关于SS(R)那点事儿](https://blog.wateroot.com/thinking/2017-07-27-news-about-ssr.html)

## 安装

### 1. 服务器端

​	*环境：Ubuntu + shadowsocks-libev*

​	这里假设已经拥有一台海外线路的服务器，如AWS。

​	在服务器端使用[@teddysun](https://github.com/teddysun)的[一键安装脚本](https://teddysun.com/358.html)（shadowsocks-libev-debian.sh），复制以下命令至命令行：

```bash
wget --no-check-certificate -O shadowsocks-libev-debian.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-libev-debian.sh
chmod +x shadowsocks-libev-debian.sh
./shadowsocks-libev-debian.sh 2>&1 | tee shadowsocks-libev-debian.log
```

​	脚本运行中会提示输入/选择相关配置，其中加密方式选择 **chacha20**。[这里](http://jaminzhang.github.io/network/understanding-ChaCha20/)和[这里](http://www.fanooo.com/archives/262)可以查看 chacha20 与其它主流加密方式的比较。

### 2. 客户端

### 2.1 Windows

​	在[此页面](https://github.com/shadowsocks/shadowsocks-windows/releases)下载最新的 shadowsocks release。Windows 版客户端文档[见此](https://github.com/shadowsocks/shadowsocks-windows)。

### 2.2 Linux

​	在[此页面](https://github.com/shadowsocks/shadowsocks-qt5/releases)下载最新的 shadowsocks release。Linux 版客户端文档[见此](https://github.com/shadowsocks/shadowsocks-qt5)。

​	PAC 文件生成：[GenPAC](https://github.com/JinnLynn/genpac)

```
代理自动配置（英语：Proxy auto-config，简称PAC）是一种网页浏览器技术，用于定义浏览器该如何自动选择适当的代理服务器来访问一个网址
```

​	Ubuntu 系统设置：依次点击 System settings > Network > Network Proxy，选择 Method 为 Automatic，设置 Configuration URL 为 生成的 .pac 文件的路径，点击 Apply System Wide。例如：file:///home/{user}/autoproxy.pac

​	参考：[Ubuntu 16安装shadowsocks-qt5并使用PAC全局代理](https://www.litcc.com/2016/12/29/Ubuntu16-shadowsocks-pac/index.html)

## 使用

- PAC 模式：根据 PAC 规则过滤需要经过 ss 转发的流量

- 全局模式：所有流量均经过 ss 转发

Windows 下有时会遇到 ss 未打开时网页无法连接，这是因为 ss 在上一次关闭的时候没有恢复 Internet 属性中的代理服务器设置，可手动恢复（找到 Internet 属性 > 连接 > 局域网设置 > 代理服务器 > `为 LAN 使用代理服务器`，然后取消勾选），或手动重新打开再关闭一次 ss 客户端来尝试自动恢复。

## 参考

https://github.com/HuMoran/shadowsock-Manual

https://github.com/pkuliubin/aws_shadowsocks

*注意：以上部分链接可能需要翻墙访问*
