# 配置 SSH 密钥

## 前言

SSH 协议可以实现安全的免密认证，且性能比 HTTP(S) 协议更好，因为需要在不同的平台代码推拉，所以尝试生成多个密钥，并配置不同的平台

## 开始

第一步就是便是生成密钥，我是用的是 WSL，Ubuntu22.04 版本，这里默认本地没有生成过密钥，也可以用以下命令检测

### 检查本地密钥

```sh
ls -al ~/.ssh

# 检查目录列表以查看您是否已经拥有公共 SSH 密钥
# id_rsa.pub
# id_ecdsa.pub
# id_ed25519.pub

# 如果您收到 ~/.ssh 不存在的错误，则默认位置中没有现有的 SSH 密钥对。您可以在下一步中创建新的 SSH 密钥对。
```

### 生成密钥

```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
# 将your_email@example.com替换为对应平台的邮箱
> Generating public/private ALGORITHM key pair.
> Enter a file in which to save the key (/home/YOU/.ssh/ALGORITHM):[Press enter]
# 出现这条命令主意，这是设置保存文件的目录
```

这里我遇到一个问题，之前 GitHub 平台的教程，密钥生成使用的是默认路径，也就是~/.ssh/id_ed25519，但是我在输入了~/.ssh/codeup_ed25519 后，报错-No such file or directory，说没有找到文件或者目录，只得输入一个文件名，在执行目录下生成了密钥，也就是说如果想在.ssh 目录下生成，需要先 cd ~/.ssh

### 将 SSH 密钥添加到 ssh 代理

这是 GitHub 上的教程的一步，我在其他的教程上，云效或者 gitee 上并未见到，我猜测应该是在第一次链接后会默认添加到 ssh 代理中。

```sh
eval "$(ssh-agent -s)"
# 这里的id_ed25519换成生成密钥的文件名
ssh-add ~/.ssh/id_ed25519
```

### 定义认证密钥路径规则

目前有两个平台，GitHub 和 CodeUp（云效），所以需要设置认证密钥路径规则

在~/.ssh 目录下新建 config 文件，使用 vim 打开

```sh
cd ~/.ssh
touch config
vim config
```

编辑 config

```vim
# github
Host github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_ed25519

# codeup
Host codeup.aliyun.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/codeup_ed25519
```

这里 Host 就是对应平台的域名，IdentityFile 是对应私钥文件的路径

### 平台添加公钥

这个需要看下各个平台设置里 ssh 公钥选项，将公钥，也就是 pub 尾缀的文件

```sh
# 这里的id_ed25519换成生成密钥的文件名
cat ~/.ssh/id_ed25519.pub
```

### 测试链接

```sh
ssh -T git@gitee.com
ssh -T git@codeup.aliyun.com

# 看到如下信息
# The authenticity of host 'github.com (IP ADDRESS)' can't be established.
# RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
# Are you sure you want to continue connecting (yes/no)?

# 回复yes后
# GitHub平台回复
# Hi USERNAME! You've successfully authenticated, but GitHub does not
# provide shell access.
# 云效平台
# Warning: Permanently added 'codeup.aliyun.com' (RSA) to the list of known hosts.
# Welcome to Codeup, your_email@example.com
```

## 总结

有点烦，我一直以为 ssh 就是钥匙和锁，但是还有主机列表之类，上次因为无法使用 22 端口，害得我急了几天，现在希望别再出问题了
