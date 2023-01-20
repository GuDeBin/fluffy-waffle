# 使用 Github Action 部署项目到服务器

先说结果，失败

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
