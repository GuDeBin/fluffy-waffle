# github 分支名称更换后的本地操作

目前 GitHub 上主分支默认名称为 main，但是很多的脚手架因为是在更改之前创建的，一直保持了 master 的主分支名称

虽然这是我个人强迫症的表现形式之一，但还是记录下相应的本地操作

首先，目前的情况是本地主分支依旧还是 master，GitHub 上已经修改为 main，接下来在本地终端输入以下命令

```sh
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```
