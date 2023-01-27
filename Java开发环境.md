# Java 开发环境

我目前开发环境是 window，在微软更换的 CEO 后，越来越拥抱开源，积极放开怀抱，这对我这样的普通开发者实在是方便，有太多软件需要大公司去试错完善。

## window 下的开发环境

我先在[https://dev.java/](https://dev.java/)大致了解下如何进行第一步，也就是安装和 hello world。果然，越是官网越是谨慎，尽量不偏袒，没有态度。

直接上 IDEA，已经和 Java 绑定在一起的集成开发环境，在官网教程 Learn Java 的 Getting Started with Java 章节最后直接放了一个[IDEA Community Edition](https://www.jetbrains.com/idea/)

IDEA 社区版，新建项目，自动下载 jdk。

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

输出 Hello World

简单，直接

就是一点，这个 IDEA 直接要了快两个 G 的内存，让我一愣，虽然没有影响。

## WSL

我一直到都是在 WSL 的 Ubuntu 下开发的，自然也要试试配置 Java 开发环境了

第一时间就是搜索 Java microsoft，果然，[Microsoft Learn](https://learn.microsoft.com/zh-cn/java/)添加了对 Java 的支持，也有环境环境设置，可惜的是在[Getting Started with Java in VS Code](https://code.visualstudio.com/docs/java/java-tutorial)，WSL 下的 Linux 环境需要自己安装 JDK、VSCode 和 Java 拓展包

### JDK

直接下载了[Microsoft Build of OpenJDK](https://learn.microsoft.com/zh-cn/java/openjdk/download)的 OpenJDK 17.0.5 LTS，按照[https://dev.java/](https://dev.java/)的 Linux 教程设置环境变量

首先解压文件

在当前用户目录下新建/home/javauser/jdk 目录

```sh
mkdir /home/javauser/jdk
```

将下载的 JDK 复制到这个目录下解压

```sh
tar xzf *.tar.gz
```

设置环境变量，这里出现一个问题，就是按照[https://dev.java/](https://dev.java/)的方式，每次关闭终端，对应的环境变量就没了等于说每次都要设置一次，在找了几个教程后，选择将环境变量写入当前用户的文件中，也就是~/.bashrc

```sh
sudo vim ~/.bashrc
```

将以下文本写入

```sh
# jdk
# 这里是JDK解压后的文件目录
export JAVA_HOME="/home/javauser/jdk/jdk-19"
export PATH=$JAVA_HOME/bin:$PATH
# jdk end
```

重启终端

验证

```sh
which java
# 如果出现以下信息，说明环境变量设置成功
/home/javauser/jdk/jdk-19/bin/java
```

接下来是安装 Java 拓展包，直接在[Getting Started with Java in VS Code](https://code.visualstudio.com/docs/java/java-tutorial)的 Installing extensions 章节，点击 Install the Extension Pack for Java，现在本地安装对应的拓展插件

打开 WSL 的 vscode，在插件同步本地插件在 wsl 同步安装，也就是 WSL 的小云朵

![WSL下同步安装](./Java%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202023-01-17%20233703.png)

同步完毕后，快捷键(Ctrl+Shift+P)进入命令面板，输入 Java，下列列表中选择 Java:Create Java Project > No build tools，选择工作目录，输入项目名称，code 会自动弹出一个新窗体，在 src 目录下的 App.java 中

```java
public class App {
    public static void main(String[] args) throws Exception {
        System.out.println("Hello, World!");
    }
}
```

点击 main 方法上的 Run

终端输出 Hello World

WSL 环境设置完毕

## 2023 年 1 月 27 日更新

今天再度将 java 环境设置一边，之前只是在 Java 的基础知识上摸爬滚打，没想到的是进入 spring 之后才知道为啥 IDEA 这样的重型编辑器会成为生产开发的首选，真是在生产环境没时间玩玩具，而是产出

说下经过，在 spring initial 网站初始化后在本地根本跑不起来，这让我开始怀疑是 java 环境问题，（其实是我没有装 spring WEB 这个依赖）便开始重新安装 Java 环境，分为 window 环境下和 WSL-Ubuntu 下，最终解决也很简单，直接搜索 Java Microsoft 这两个关键字，直接就指向 Microsoft 的 Java 开发实践，下载安装 jdk 和设置 vscode 环境，简单明了

教训啊，下次直接如此搜索，倒不至于走这么多弯路

还下载了 Eclipse，不过因为不熟悉和中文安装包有点复杂，实在不想在搞了，不过在 wsl 上，同样的开发环境下，并不能类似 window 环境下使用，看样子 Java 开发还得在 window 环境下
