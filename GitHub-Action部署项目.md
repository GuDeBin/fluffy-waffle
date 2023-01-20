# 使用 Github Action 部署项目到服务器

先说结果，失败

失败的原因也是很简单，阿里云拒绝了 GitHub 的远程、ssh 登录，直接报警，我原本想找到绕开的方法，但是这个服务器毕竟属于我的资产，一旦要是有点困扰，这境外。。。。优点是管不到，缺点也是管不到啊

最后采用了阿里自家的云效，确实不错，但是还是说下这次 GitHub Action 的收获。

## 开始

一开始只是想亲自部署产品，本地代码》GitHub 远程库》触发更改 Action》部署到服务器

路径还是很清晰的，也有相对应的的教程

[使用 Github Action 部署项目到云服务器](https://zhuanlan.zhihu.com/p/107545396)

[GitHub Actions 入门教程](https://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)

[GitHub Actions 部署页面至阿里云 ECS](https://juejin.cn/post/6931318429420879879)

以及花果山

[花果山大圣的 fe-advanced-interview](https://github.com/shengxinjing/fe-advanced-interview)

```yml
# This is a basic workflow to help you get started with Actions

name: deploy

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [main]
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2
      - name: install Node.js
        uses: actions/setup-node@v2.5.0
        with:
          node-version: "16.X"
      - name: install dep
        run: npm install
      - name: build app
        run: npm run build
      - name: copy file via ssh password
        uses: appleboy/scp-action@master
        with:
          host: ${{ secrets.REMOTE_HOST }}
          username: ${{ secrets.REMOTE_USER }}
          password: ${{ secrets.REMOTE_PASS }}
          port: 22
          source: "docs/"
          target: ${{ secrets.REMOTE_TARGET }}
```

可以说，按照教程步骤，和贴出的 yml 代码，修改下就可以做出一个适合自己的 action，基本上都是设置 Ubuntu 环境，签出代码存储库的代码到虚拟机上，安装 node，npm 安装依赖和构建，通过 appleboy/scp-action@master 部署到服务器上

appleboy/scp-action@master

- host：主机 ip 名，也就是服务器的 ip
- username：在服务器上执行的用户名，一般是 root
- password：登录服务器的密码
- port：端口，这里使用的是 ssh，也就是 22 端口
- source：构建项目的目录，也就是需要复制到服务的文件路径
- target：服务器对应的目录

还有一个配置，是 ssh 密钥方式，基本上一致，不过是将密码换成了 key

actions/checkout@v2

这个操作签出$GITHUB_WORKSPACE下的存储库，以便您的工作流可以访问它。默认情况下，对于触发工作流的ref/SHA只获取一个提交。设置fetch-depth: e来获取所有分支和标签的所有历史。参考这里了解$GITHuB_SHA 针对不同事件指向哪个提交。认证令牌在本地 git 配置中持久化。这使您的脚本可以运行经过身份验证的 git 命令。在作业后清理期间删除令牌。设置“persistent -credentials: false”为选择退出。当 Git 2.18 或更高版本不在您的 PATH 中时，返回到 REST API 下载文件。

另一个部署方式-ssh

```yml
name: Continuous Deploy #action名称
on: [push] #在推送的时候运行此action

jobs:
  deploy_job:
    runs-on: ubuntu-latest #运行环境
    name: build
    steps:
      # check out the repository
      - name: Checkout
        uses: actions/checkout@v2 #这里使用了github官方提供的action,checkout项目到虚拟机上

      - name: Install Dependencies
        run: yarn
      - name: Build
        run: yarn build

      # 利用action把build好的文件上传到服务器/var/www/react-app路径下,需要确认此目录已在服务端创建
      - name: Deploy to aliyun server # 为 step 指定一个名称，将会在 github action 的控制台中显示
        uses: easingthemes/ssh-deploy@v2.1.5 #可以访问的仓库，实现的上传服务器步骤被封装在此action
        env:
          SSH_PRIVATE_KEY: ${{ secrets.SERVER_SSH_KEY }} #这个是阿里云的私钥
          ARGS: "-avzr --delete"
          SOURCE: "./build/*"
          REMOTE_HOST: ${{ secrets.REMOTE_HOST }} #阿里云的 ip
          REMOTE_USER: ${{ secrets.REMOTE_USER }} #阿里云用户
          TARGET: "/var/www/html" #被部署的服务器路径
```

前面都是顺利，但是在最后的部署到服务器，错误不断，无法找到服务器，我试了密码、密钥和服务器自己生成 key，但是都是无法成功，网上也没有对应的解决方法，但是两个报警信息告诉我，是阿里云的安全拦截了登录。因为是异常 ip 登录，我看了下，一个是纽约州，一个是爱达荷州，自己的比特穿过太平洋也是别样的浪漫。

最后我放弃在 GitHub 上通过 action 部署，改用了云效，先说下结果，成功了。
