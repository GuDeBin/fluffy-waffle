# nvm 安装

这个坑来源是因为国内网络原因， 使用 nvm 一键命令

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

总是网络错误，即便用了代理也是如此，很是让沮丧

第一用的方法是手动安装，直接将 install.sh 文件下载下来，之后在运行脚本

但是第二次再次安装我发现了 git install，很可惜，我压根不知道什么叫做 git 激活，也就是

activate nvm by sourcing it from your shell: . ./nvm.sh

这句话的意思，这也是我的一个缺点，过度思考

其实如果我只是想安装，直接复制后面的命令即可。

更根本的是我不知道 bash 命令，他就是一个 · ，也就是 · 脚本文件

哎

其实 git install 也是如此

但是我得知道一个问题，就是我安装 nvm 的步骤

1. 首先是下载 install 脚本文件

2. · install.sh

3. 重启终端

4. 通过 command -v nvm 验证安装是否成功
