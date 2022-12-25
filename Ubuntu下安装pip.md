# ubuntu 下安装 pip

因为需要 jupyter ，在 vscode 运行时需要 pip，记录下安装过程，三步

第一步确认 Ubuntu 中已经安装 python3

```sh
python3 --version
```

确认安装了 python3

第二步，安装 pip

```sh
sudo apt install python3-pip
```

第三步，验证

```sh
pip3 --version
# or
pip --version
```
