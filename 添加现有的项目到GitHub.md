# 添加现有的项目到 GitHub 库上

1. git remote add origin git@github.com:GuDeBin/glowing-octo-umbrella.git(仓库地址)

2. git branch -M main

3. git push -u origin main

不行啊

一个已经有内容的库无法在添加本地项目，估计存在权限上的事情，还得再摸索

现在先找到一个通用的、可行的操作步骤满足日常使用即可

1. 在 GitHub 上新建一个库，但是不要新增 README

2. 按照添加现有库的方式，增加文章开始的三条命令，记得更换后面的仓库名

3. 完成提交，建立和远程库的链接进行开发

## 2023 年 1 月 19 日

本地强制上传到远程，把远程的覆盖

git push -f origin main

关键在于 -f 参数
