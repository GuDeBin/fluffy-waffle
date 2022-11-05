# npm pnpm 安装缓慢

先描述下问题

这几天不知道怎么回事，启动脚手架后安装依赖过程极其缓慢，之前都是几秒事情，现在往往十几分钟

刚刚开始是使用 UmiJS 的脚手架，在创建时就缓慢异常，我以为是网络问题，结果今天又想尝试 vite，还是如此，我列出几个可能性

1. 我的电脑硬盘，这个固态硬盘的寿命到期了，读取降速吗
2. 频繁使用 rm -rf 删除文件导致系统混乱
3. WSL 的系统问题
4. 网络问题

第一可能性很快排除，如果是硬件问题，那么应该是所有的软件和系统都卡顿

第二个可能性，在我换了个文件夹，在不同的地方测试，皆是如此，排除

第三个，wsl 问题，倒不是找到反证，而是间接解释，如果是 wsl，那么我在这里操作其他的也可能出现同样的症状，不应仅仅是安装脚手架的问题，暂时可以将这个放在第二位

第四个，这次我到越来越能肯定，因为在 npm 和 pnpm 中，卡顿都是在请求 npm 包的过程中

现在在问题未定的情况下先尝试重装重启大法，将 node 重装，npm 升级

使用代理影响这个 npm 和 node 吗

大概率是网络问题

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

## 换源

export NVM_NODEJS_ORG_MIRROR

npm

https://registry.npmjs.org/

npm config set registry

https://registry.npmmirror.com/

新开一篇文章[开发换源](./%E5%BC%80%E5%8F%91%E6%8D%A2%E6%BA%90.md)
