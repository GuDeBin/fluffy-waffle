# Ubuntu 换源遇到的坑

首先因为网络墙的问题，我在使用 WSL 的 Linux，也就是 Ubuntu 时需要将自己的软件更新源换成国内相关的源

之前用的是清华源，确实没有什么坑，但是也有一个自己感觉上的不舒服，大概是自己反感精英的思想作祟

所以后面换成了阿里源，也就有了今天的坑，它不管用

## 步骤

1. 首先是定位到软件源的目录并备份原先的软件源，以防失败

```shell
# 终端输入以下命令
cd /etc/apt

sudo cp sources.list sources.list.bak
```

2. 删除原先的源文件内容

```shell
sudo vi /etc/apt/sources.list
```

在 vi 编辑器里，按下 i 键进入输入模式，左下角会出现 Insert 字符，直接使用退格键删除原先的内容

3. 复制源

[阿里源](https://developer.aliyun.com/mirror/ubuntu?spm=a2c6h.13651102.0.0.77561b11tcYvqo)

[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

Ctrl+C 和 Ctrl+V

4. 终端执行命令

```shell
sudo apt update
```

## 总结

这次遇到的问题并不是源的问题，而是我删除了一些文件，实在是找不到相对应的解决问题，在 PowerShell 的 issue 中有相应的问题，但是并没有相应的解决，只有一个我已经习惯了的描述

这个真的触发了我固执，我还是想重置电脑，不过当居家办公结束时我就可以使用保留个人文件的方式来重置电脑
