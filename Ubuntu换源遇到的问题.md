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
sudo vim /etc/apt/sources.list
```

在 vim 编辑器里

直接输入 dG，因为刚进入就是命令模式，dG 命令是将从光标开始到最后一行全部删除

按下 i 键进入输入模式，左下角会出现 Insert 字符

3. 复制源

[阿里源](https://developer.aliyun.com/mirror/ubuntu)

[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

Ctrl+C 和 Ctrl+V

按下:wq 进入底线命令模式，wq 是保存并退出文件

4. 终端执行命令

```shell
sudo apt update && sudo apt upgrade -y
```

## 总结

这次遇到的问题并不是源的问题，而是我删除了一些文件，实在是找不到相对应的解决问题，在 PowerShell 的 issue 中有相应的问题，但是并没有相应的解决，只有一个我已经习惯了的描述

这个真的触发了我固执，我还是想重置电脑，不过当居家办公结束时我就可以使用保留个人文件的方式来重置电脑

## 新增方法

这个是在清华源下看到的，不得不说清华源的教程是最贴心的，给清华源一个赞，感谢

```sh
sudo sed -i "s@http://.*archive.ubuntu.com@https://mirrors.aliyun.com@g" sources.list
sudo sed -i "s@http://.*security.ubuntu.com@https://mirrors.aliyun.com@g" sources.list
```
