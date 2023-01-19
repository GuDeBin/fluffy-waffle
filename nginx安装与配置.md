# nginx 安装与配置

## nginx 简介

Nginx 发音 “engine x” ,是一个开源软件，高性能 HTTP 和反向代理服务器，用来在互联网上处理一些大型网站。它可以被用作独立网站服务器，负载均衡，内容缓存和针对 HTTP 和非 HTTP 的反向代理服务器。

和 Apache 相比，Nginx 可以处理大量的并发连接，并且每个连接占用一个很小的内存。

[Nginx 与前端开发](https://juejin.cn/post/6844903684967825421)

## Ubuntu 下安装

```sh
# 安装命令
sudo apt install nginx

# 验证
nginx -v

# 启动服务
sudo service nginx start
```

## nginx 配置

配置文件目录：/etc/nginx
