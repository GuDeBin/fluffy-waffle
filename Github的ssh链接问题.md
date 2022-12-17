# GitHub 的 ssh 连接问题

昨天突然出现，不知道是什么原因，无法克隆，也无法提交更改，我顿时慌了

## 原因分析

1. 代理问题
2. git 问题
3. wsl 问题
4. GitHub 问题

## 逐一排查

首先排除的就是 GitHub 问题，因为概率极低，服务器炸了，这个在网络上第一时间就是最大的热门头条，可我并未搜到相关的报告和 GitHub 通告

wsl 问题，难道是 Ubuntu22.04 出现的新 BUG，联系思考下，这个问题和 git 问题是一致的，都是系统软件问题，立刻结合测试下，gitee 没有问题。

那就只剩下代理，按照 GitHub 的 ssh 排查

## 检查是否连接到正确的服务器

```sh
$ ssh -vT git@github.com
> OpenSSH_8.1p1, LibreSSL 2.7.3
> debug1: Reading configuration data /Users/YOU/.ssh/config
> debug1: Reading configuration data /etc/ssh/ssh_config
> debug1: /etc/ssh/ssh_config line 47: Applying options for *
> debug1: Connecting to github.com port 22.
```

是在端口 22 上建立了链接

## Always use the "git" user：总是使用 git 用户

说实话这个我没看懂，在尝试两个命令都没有效果后

```sh
$ ssh -T GITHUB-USERNAME@github.com
$ ssh -T GuDeBin@github.com
```

都是没有反应，应该是被拒绝了

之后尝试测试链接的命令也是失败的

```sh
ssh -T git@github.com
```

## 确保您有正在使用的密钥

这个也是丈二和尚摸不着头脑，按照命令

```sh
$ ssh-add -l -E sha256
```

没有打印出任何字符，显示没有找到之类的

但是我看 sha256，这个应该不是我生产 ssh 公钥的算法吧

## 解决

问题还没排查完，我就觉的没戏，大概率还是重装大法，我已经适应，但是我看到在第一问题后有一个通过 https 使用 ssh，我点开，第一句便是

> 有时，防火墙拒绝完全允许 SSH 连接。如果无法将 HTTPS 克隆与凭据缓存结合使用，则可以尝试使用通过 HTTPS 端口建立的 SSH 连接进行克隆。大多数防火墙规则应允许这样做，但代理服务器可能会干扰。

代理服务器，防火墙，联想到之前将 ssh 公钥加入到 gitee 中，一套 ssh 公钥两边用，是不是让 ssh 出现识别问题，也就是说 ssh 认为这把锁应该是用于 gitee 上，而不是 GitHub 上，这个是不是导致出现问题的原因，而且我的代理呢

直接尝试下

在~/.ssh 下新建一个 config 文件，添加以下内容

```sh
Host github.com
Hostname ssh.github.com
Port 443
User git
```

测试连接

```sh
ssh -T git@github.com
```

OK 了

赶紧 clone 一个仓库，没有问题了，vscode 上也显示 git 更改和修改了

## 疑问

到底是代理干扰了之前使用的 22 端口还是因为使用 gitee 后导致的

其实现在就可以再次测试一次

gitee 仍可以使用，通过 22 端口，但是当我删除了 https 的配置文件后，github 无法连接，这个就让我怀疑，并不是代理的问题，还可能是 ssh 默认将 git 用户，也就是 git 软件连接 gitee，而不是 GitHub，这个问题还真的是，要不重新生成显得密钥，再次连接到 GitHub 中，要不就按照现在的模式使用，因为问题已经解决了。

思考以后

gitee 注定失败，心疼它的尝试，政治至上的原则扼杀太多的想象。

删除现有的 ssh 和新增的配置文件 config

按照 GitHub 的新增 ssh 方式进行

## 最新

重新生成 ssh 密钥无效，依旧无法连接到 GitHub 上，只有在 config 中配置通过 https 端口建立 ssh 连接才可以连接，但是 Gitee 却没有问题
