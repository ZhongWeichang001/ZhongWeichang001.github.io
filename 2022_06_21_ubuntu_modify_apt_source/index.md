# Ubuntu 20.04 LTS 修改 apt 源


# 概述

由于在 Windows 环境下做开发，在配置环境方面经常会遇到各种问题，因此，选择使用 Ubuntu 来作为开发环境，版本为 Ubuntu 20.04。

Ubuntu 使用 apt 作为软件包管理器，其默认的下载源在国外，为了加快软件下载速度，建议在安装好系统之后就修改为国内的镜像源，常见的国内源包括：阿里源、清华源、中科大源等，完整的官方镜像源列表可以查看 [Mirrors : Ubuntu](https://launchpad.net/ubuntu/+archivemirrors)。

这里使用阿里源为例，展示如何进行修改。

# 备份旧的 apt 配置文件

apt 配置文件位于 `/etc/apt` 目录下，其中 `sources.list` 文件是 apt 用来记录镜像源配置信息的，建议在修改之前对其进行备份：

```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```

# 查看 Ubuntu 版本代号

使用 `lsb_release` 命令来查看 Ubuntu 版本代号：

```cpp
$ lsb_release --codename
Codename:	focal
```

每个版本的代号都是不一样的，例如：

- Ubuntu 22.10：`kinetic`
- Ubuntu 22.04：`jammy`
- Ubuntu 21.10：`impish`
- Ubuntu 20.04：`focal`
- Ubuntu 18.04：`bionic`

{{< admonition type=note open=true >}}
我在这边踩过一次坑，我用的是 20.04 版本，版本代号应该为 `focal`，但是修改源时使用了 18.04 的代号 `bionic`，导致后面在安装软件时遇到各种报错信息，通过排查才知道是自己版本代号配置错了。
{{< /admonition >}}

# 编辑新的 apt 配置文件

```bash
sudo vi /etc/apt/sources.list
```

修改 apt 源为阿里源：

```
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
```

如果需要使用其他的源，只需要修改镜像地址即可，常见的软件源的地址如下：

- 清华源：[https://mirrors.tuna.tsinghua.edu.cn/ubuntu](https://mirrors.tuna.tsinghua.edu.cn/ubuntu)
- 中科大源：[http://mirrors.ustc.edu.cn/ubuntu](http://mirrors.ustc.edu.cn/ubuntu)
- 南大源：[https://mirror.nju.edu.cn/ubuntu](https://mirror.nju.edu.cn/ubuntu/)
- 网易源：[http://mirrors.163.com/ubuntu](http://mirrors.163.com/ubuntu)

# 更新软件列表

执行如下命令更新软件列表索引：

```bash
sudo apt update -y
```

# 更新软件包

执行如下命令升级软件包：

```bash
sudo apt upgrade
```

# 参考资料

- [Ubuntu Manpage: sources.list - List of configured APT data sources](https://manpages.ubuntu.com/manpages/focal/man5/sources.list.5.html)
- [Mirrors : Ubuntu](https://launchpad.net/ubuntu/+archivemirrors)
