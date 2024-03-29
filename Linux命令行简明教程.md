# 初学者的 Linux 命令行简易教程

翻译自[Ubuntu 教程](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)

因为反复看这篇教程，其中一些操作和原则非常有用，这也是我坚定使用 Ubuntu 的原因，它对于新手真好。

## 概述

Linux 命令行是计算机的文本界面。通常被称为外壳，终端，控制台，提示符或各种其他名称，它可能看起来很复杂且使用起来令人困惑。然而，从网站复制和粘贴命令的能力，加上命令行提供的强大功能和灵活性，意味着在尝试在线遵循说明时使用它可能是必不可少的，包括这个网站上的许多说明！

本教程将教您一些命令行的历史，然后引导您完成一些实践练习，以熟悉一些基本的命令和概念。我们将假设没有先验知识，但到最后，我们希望您下次面对一些以“打开终端”开头的说明时会感到更舒服一些。

最初由[peppertop](https://github.com/peppertop)撰写。

您将学到什么

- 命令行的小历史
- 如何从您自己的计算机访问命令行
- 如何执行一些基本的文件操作
- 其他一些有用的命令
- 如何将命令链接在一起以制作更强大的工具
- 使用管理员权限的最佳方式

你需要什么

- 运行 Ubuntu 或其他版本 Linux 的计算机

每个 Linux 系统都包含这样或那样的命令行。本教程包括 Ubuntu 18.04 的一些特定步骤，但无论您的 Linux 发行版如何，大多数内容都应该有效。

## 简短的历史课

在计算机工业的形成时期，早期的操作系统之一被称为 Unix。它被设计成在大型计算机上运行的多用户系统，用户可以通过单独的终端远程连接到它。按照现代标准，这些终端是相当基础的:只有键盘和屏幕，没有能力在本地运行程序。相反，他们只需向服务器发送击键，并在屏幕上显示接收到的任何数据。没有鼠标，没有花哨的图形，甚至没有任何颜色的选择。一切都以文本的形式发送，也以文本的形式接收。因此，显然，在大型机上运行的任何程序都必须产生文本作为输出，并接受文本作为输入。

与图形相比，文本占用的资源非常少。即使是在 20 世纪 70 年代的机器上，在极慢的网络连接(以今天的标准)上运行数百个终端，用户仍然能够快速有效地与程序交互。为了减少击键次数，命令也保持得非常简洁，从而进一步加快了人们使用终端的速度。这种速度和效率是这种文本界面至今仍被广泛使用的原因之一。

当用户通过终端登录到 Unix 大型机时，仍然需要管理文件管理任务，而现在您可以通过鼠标和几个窗口来完成这些任务。无论是创建文件、重命名文件、将其放入子目录或在磁盘上移动它们，70 年代的用户都可以通过文本界面完成所有事情。

每个任务都需要自己的程序或命令:一个更改目录(cd)，另一个列出目录的内容(ls)，第三个重命名或移动文件(mv)，等等。为了协调每一个程序的执行，用户将连接到一个主程序，然后可以使用该主程序启动其他任何程序。通过包装用户的命令，这个众所周知的“shell”程序可以为任何命令提供通用功能，例如从一个命令直接传递数据到另一个命令的能力，或者使用特殊的通配符一次性处理大量名称相似的文件的能力。用户甚至可以编写简单的代码(称为“shell 脚本”)，这些代码可用于自动化长序列的 shell 命令，以便使复杂的任务更简单。最初的 Unix shell 程序刚刚被调用，但多年来它已经被扩展和取代，所以在现代 Linux 系统上，您最有可能使用的 shell 是。不要太担心您使用的是哪个 shell，本教程中的所有内容都适用于几乎所有 shell

Linux 可以说是 Unix 的后裔。Linux 的核心部分被设计成与 Unix 系统类似的行为，因此大多数旧 shell 和其他基于文本的程序都能在 Linux 上运行得非常愉快。理论上，你甚至可以将一个上世纪 70 年代的老式终端连接到一个现代 Linux 机顶盒上，并通过它访问外壳。但如今，使用软件终端更为普遍:同样是 unix 风格的文本界面，但在窗口中运行，与图形程序并排运行。让我们看看你自己是如何做到的!

## 开启终端

在 Ubuntu 18.04 系统中，你可以通过点击屏幕左上方的 Activities 项目，然后输入“terminal”、“command”、“prompt”或“shell”的前几个字母来找到终端的启动器。是的，开发人员已经用所有最常见的同义词设置了启动器，所以您找到它应该没有问题。

![ubuntu18.04的终端启动器](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Terminal%20launcher%20in%20Ubuntu%2018.04_2_690x175.png)

其他版本的 Linux，或者其他版本的 Ubuntu，通常会有一个终端启动器，位于与其他应用程序启动器相同的位置。它可能隐藏在子菜单中，或者你可能必须从启动器中搜索它，但它很可能就在那里的某个地方。

如果您找不到启动器，或者您只是想以更快的方式启动终端，大多数 Linux 系统使用相同的默认键盘快捷方式来启动它:Ctrl-Alt-T。

无论如何启动终端，最终都应该看到一个看起来相当沉闷的窗口，顶部有一些“奇怪”的文本，就像下图一样。根据您的 Linux 系统的不同，颜色可能不相同，文本也可能显示不同的内容，但是具有大文本区域(大部分为空)的窗口的总体布局应该是相似的。

![在Ubuntu18.0打开一个新的终端窗口](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/A%20new%20terminal%20window%20in%20Ubuntu%2018.04_2_690x300.png)

让我们运行第一个命令。在窗口中单击鼠标以确保这就是您击键的位置，然后键入以下命令，全部用小写字母，然后按 Enter 或 Return 键运行该命令。

```sh
pwd
```

您应该看到打印出来的目录路径(可能类似于/home/YOUR_USERNAME)，然后是该“奇怪”文本的另一个副本。

![](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Result%20of%20running%20the%20pwd%20command_2_690x300.png)

在深入了解该命令实际做了什么之前，这里需要了解一些基础知识。首先，当您键入一个命令时，它会与“奇怪”文本出现在同一行中。这个文本是告诉你计算机准备好接受命令了，这是计算机提示你的方式。实际上，它通常被称为提示符，您有时可能会看到“弹出提示符”、“打开命令提示符”、“在 bash 提示符”或类似的指示。它们都是要求你打开终端进入外壳的不同方式。

关于同义词的主题，另一种看待提示符的方法是，在终端中有一行用于输入命令。一个命令行，如果你愿意。同样，如果您在本教程的标题中看到“命令行”的提及，那么这只是在另一种方式中谈论在终端中运行的 shell。

第二件要理解的事情是，当您运行一个命令时，它产生的任何输出通常会直接打印在终端上，然后在它完成后会显示另一个提示符。有些命令可以输出大量文本，而其他命令将静默操作，根本不会输出任何内容。如果您运行一个命令，而另一个提示立即出现，请不要惊慌，因为这通常意味着命令成功了。如果你回想一下 20 世纪 70 年代终端缓慢的网络连接，那些早期的程序员认为，如果一切正常，他们还不如什么都不说来节省一些宝贵的数据传输字节。

**案例的重要性**

在命令行中输入时要特别注意大小写。输入 PWD 而不是 pwd 将产生错误，但有时错误的情况会导致命令运行，但没有达到您的预期效果。我们将在下一页中更多地讨论这种情况，但是现在，只要确保在显示的情况下键入所有以下行。

### 路径目录

现在来谈谈命令本身。pwd 是“打印工作目录”的缩写。它所做的只是打印出 shell 的当前工作目录。但是什么是工作目录呢?

需要理解的一个重要概念是，shell 有一个默认位置的概念，任何文件操作都将发生在该位置。这是它的工作目录。如果您试图创建新文件或目录，查看现有文件，甚至删除它们，shell 将假定您正在当前工作目录中查找它们，除非您采取其他步骤进行指定。因此，了解 shell 在任何时候“位于”哪个目录是非常重要的，毕竟，从错误的目录中删除文件可能是灾难性的。如果您有任何疑问，pwd 命令将确切地告诉您当前工作目录是什么。

您可以使用 cd 命令更改工作目录，cd 是“change directory”的缩写。试着输入以下内容:

```sh
cd /
pwd
```

注意，目录分隔符是正斜杠(“/”)，而不是您在 Windows 或 DOS 系统中习惯使用的反斜杠

现在您的工作目录是“/”。如果你有 Windows 背景，你可能习惯了每个硬盘都有自己的字母，你的主硬盘通常是“C:”。类 unix 系统不会这样分割驱动器。相反，它们有一个统一的文件系统，各个驱动器可以附加(“挂载”)到文件系统中最有意义的任何位置。“/”目录通常被称为根目录，它是统一文件系统的基础。从那里，所有其他的分支形成一个目录和子目录的树。

**root 的多种含义**

注意:尽管“/”目录有时被称为根目录，但单词“root”有另一个含义。root 也是自 Unix 早期以来一直用于超级用户的名称。超级用户，顾名思义，拥有比普通用户更多的功能，因此可以很容易地用键入错误的命令造成严重破坏。我们将在第 7 节中更多地讨论超级用户帐户。现在您只需要知道“root”这个词在 Linux 世界中有多种含义，因此上下文非常重要。

从根目录，以下命令将移动到“home”目录(它是“/”的直接子目录):

```sh
cd home
pwd
```

要上移到父目录，在本例中是返回到" / "，在更改目录时使用两个点的特殊语法(注意 cd 和..之间的空格)，不像在 DOS 中，你不能只输入 cd..作为一个命令):

```sh
cd ..
pwd
```

输入 cd 是返回你的主目录的快捷方式:

```sh
cd
pwd
```

你也可以用..如果你需要通过多个级别的父目录向上移动不止一次:

```sh
cd ../..
pwd
```

注意，在前面的示例中，我们描述了通过目录的路由。我们使用的路径意味着“从工作目录开始，移动到父目录/从新位置再次移动到父目录”。因此，如果我们想从我们的主目录直接到“etc”目录(直接在文件系统的根目录中)，我们可以使用以下方法:

```sh
cd
pwd

cd ../../etc
pwd
```

相对路径和绝对路径

到目前为止，我们看到的大多数示例都使用相对路径。也就是说，您最终到达的位置取决于您当前的工作目录。考虑尝试 cd 到“etc”文件夹。如果你已经在根目录下，那就没问题:

```sh
cd /
pwd
cd etc
pwd
```

但是如果是在主目录中呢?

```sh
cd
pwd
cd etc
pwd
```

在运行最后一个 pwd 之前，您将看到一个错误提示“没有这样的文件或目录”。通过指定目录名称或使用..会有不同的效果取决于你从哪里开始。该路径只相对于您的工作目录有意义。

但是我们已经看到了两个绝对的命令。无论您当前的工作目录是什么，它们都具有相同的效果。第一个是当你运行 cd 直接到你的主目录时。第二个是当您使用 cd /切换到根目录时。事实上，任何以正斜杠开头的路径都是绝对路径。您可以将其理解为“切换到根目录，然后从那里遵循路由”。这为我们提供了一种切换到 etc 目录的更简单的方法，无论我们当前在文件系统的哪个位置:

```sh
cd
pwd
cd /etc
pwd
```

它还提供了另一种方法来返回您的主目录，甚至返回其中的文件夹。假设您想从磁盘上的任何位置直接进入“Desktop”文件夹(注意大写的“D”)。在下面的命令中，你需要用你自己的用户名替换 USERNAME，如果你不确定，whoami 命令会提醒你你的用户名:

```sh
whoami
cd /home/USERNAME/Desktop
pwd
```

还有一个方便的快捷方式是绝对路径。正如您所看到的，在路径的开头使用“/”意味着“从根目录开始”。在路径的开头使用波浪号(“~”)同样意味着“从我的主目录开始”。

```sh
cd ~
pwd

cd ~ /Desktop
pwd
```

现在，提示符中奇怪的文本可能有点意义了。当您在文件系统中移动时，您是否注意到它的变化?在 Ubuntu 系统中，它会显示你的用户名，你的计算机的网络名称和当前的工作目录。但如果在主目录中的某个位置，它将使用“~”作为缩写。让我们稍微浏览一下文件系统，并在执行过程中注意一下提示:

```sh
cd
cd /
cd ~ /Desktop
cd /etc
cd /var/log
cd . .
cd
```

到现在为止，您一定已经厌倦了在文件系统中来回移动，但是在我们继续创建一些新文件夹和文件时，充分理解绝对路径和相对路径将是非常宝贵的!

## 创建文件夹和文件

在本节中，我们将创建一些实际的文件。为了避免不小心踩到你的任何真实文件，我们将开始创建一个新目录，远离你的主文件夹，这将作为一个更安全的环境，在其中进行实验:

```sh
mkdir /tmp/tutorial
cd /tmp/tutorial
```

注意这里使用了绝对路径，以确保教程目录是在/tmp 中创建的。如果开头没有正斜杠，mkdir 命令将尝试在当前工作目录中查找 tmp 目录，然后尝试在其中创建一个教程目录。如果找不到 tmp 目录，命令就会失败。

如果你没有猜到，mkdir 是“make directory”的缩写。现在我们已经安全地进入了测试区域(如果不确定，请再次使用 pwd 检查)，让我们创建一些子目录:

```sh
mkdir dir1 dir2 dir3
```

这个命令有点不同。到目前为止，我们只看到单独工作的命令(cd、pwd)或后面有一个项的命令(cd /、cd ~/Desktop)。但是这次我们在 mkdir 命令之后添加了三个东西。这些东西称为形参或实参，不同的命令可以接受不同数量的实参。mkdir 命令要求至少有一个参数，而 cd 命令可以使用 0 或 1 个参数，但不能更多。看看当你试图向命令传递错误数量的参数时会发生什么:

```sh
mkdir
cd /etc ~/Desktop
```

回到我们的新目录。上面的命令将在文件夹中创建三个新的子目录。让我们用 ls (list)命令来看看它们:

```sh
ls
```

如果你已经执行了最后几个命令，你的终端应该看起来像这样:

![The terminal, after running mkdir and ls](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/The%20terminal%2C%20after%20running%20mkdir%20and%20ls.png)

注意，mkdir 在一个目录中创建了所有文件夹。它没有在 dir2 和 dir1 中创建 dir3，也没有创建任何其他嵌套结构。但有时能够做到这一点是很方便的，mkdir 确实有一个方法:

```sh
mkdir -p dir4/dir5/dir6
ls
```

这一次，您将看到只有 dir4 被添加到列表中，因为 dir5 在其中，dir6 在其中。稍后我们将安装一个有用的工具来可视化结构，但你已经有足够的知识来确认它:

```sh
cd dir4
ls
cd dir5
ls
cd ../..
```

我们使用的“-p”被称为选项或开关(在本例中它的意思是“也创建父目录”)。选项用于修改命令的操作方式，允许单个命令以各种不同的方式执行。不幸的是，由于历史和人性的特性，选项可以在不同的命令中采用不同的形式。您经常会看到它们是前面加一个连字符的单个字符(如本例)，或者是前面加两个连字符的较长的单词。单字符形式允许组合多个选项，尽管不是所有命令都接受这一点。更让人困惑的是，有些命令根本没有清楚地标识它们的选项，而某些东西是否为选项完全由参数的顺序决定!你不需要担心所有的可能性，只要知道选择的存在，它们可以采取几种不同的形式。例如，以下都是完全相同的意思:

```sh
#不要输入这些，它们只是为了演示的目的
mkdir --parents --verbose dir4/dir5
mkdir -p --verbose dir4/dir5
mkdir -p -v dir4/dir5
mkdir -pv dir4/dir5
```

现在我们知道了如何通过将多个目录作为单独的参数传递给 mkdir 命令来创建多个目录。但是假设我们想要创建一个名称中有空格的目录?让我们试一试:

```sh
mkdir anther folder
ls
```

你可能甚至不需要输入这个就能猜到会发生什么:两个新文件夹，一个叫做 **_anther_**，另一个叫做 **_folder_**。如果希望在目录或文件名中使用空格，则需要对它们进行*转义*。别担心，没人会越狱;*转义*是一个计算术语，指使用特殊代码告诉计算机将特定字符与正常字符区别对待。输入以下命令，尝试用不同的方法创建名称为空格的文件夹:

```sh
mkdir "folder 1"
mkdir 'folder 2'
mkdir folder\ 3
mkdir "folder 4" "folder 5"
mkdir -p "folder 6"/"folder 7"
ls
```

尽管可以使用命令行处理名称中有空格的文件和文件夹，但是需要用引号或反斜杠对它们进行转义，这使事情变得有点困难。您通常可以通过文件名来判断一个人经常使用命令行:他们倾向于坚持使用字母和数字，并使用下划线(“\_”)或连字符(“-”)而不是空格。

### 使用重定向创建文件

我们的演示文件夹开始看起来充满了目录，但是有些缺少文件。让我们通过重定向命令的输出来补救这个问题，这样它就不会被打印到屏幕上，而是以一个新文件的形式结束。首先，提醒自己 ls 命令当前显示的内容:

```sh
ls
```

假设我们希望将该命令的输出捕获为文本文件，以便我们可以进一步查看或操作。我们所需要做的就是在命令行末尾加上大于号字符(" > ")，后面跟着要写入的文件名:

```sh
ls > output.txt
```

这一次没有任何东西打印到屏幕上，因为输出被重定向到我们的文件。如果您只是单独运行 ls，您应该会看到 output.txt 文件已经创建。我们可以使用 cat 命令查看它的内容:

```sh
cat output.txt
```

好了，它和之前显示在屏幕上的不完全一样，但它包含了所有相同的数据，而且它的格式对进一步处理更有用。让我们看看另一个命令 echo:

```sh
echo "this is a test"
```

是的，echo 只是再次打印出它的参数(因此得名)。但是将它与重定向结合起来，你就有了一种轻松创建小测试文件的方法:

```sh
echo "This is a test" > test_1.txt
echo "This is a second test" > test_2.txt
echo "This is a third test" > test_3.txt
ls
```

您应该对每个文件进行 cat 检查，以检查其内容。但是 cat 不仅仅是一个文件查看器——它的名字来自于“concatenate”，意思是“连接在一起”。如果你传递多个文件名给 cat，它会一个接一个地输出每个文件名，作为单个文本块:

```sh
cat test_1.txt test_2.txt test_3.txt
```

如果要将多个文件名传递给单个命令，如果文件名相似，有一些有用的快捷方式可以节省大量输入。可以使用问号(“?”)表示文件名中的“任何单个字符”。星号(“\*”)可以用来表示“零个或多个字符”。这些字符有时称为“通配符”字符。一些例子可能会有所帮助，以下命令都做同样的事情:

```sh
cat test*1.txt test_2.txt test_3.txt
cat test* ? . txt
cat test\_ \*
```

**需要更多转义**

您可能已经猜到了，此功能还意味着您需要使用?或者其中也有\*个字符。如果想从命令行操作文件名，通常最好避免文件名中的任何标点符号。

如果查看 ls 的输出，您会注意到唯一以“t”开头的文件或文件夹是我们刚刚创建的三个测试文件，所以您甚至可以进一步简化最后一个命令为 cat t\*，意思是“连接所有名称以 t 开头、后面有零个或多个其他字符的文件”。让我们使用这个功能将所有的文件连接到一个新文件中，然后查看它:

```sh
cat t* > combined.txt
cat combined.txt
```

如果我们第二次运行这两个命令，您认为会发生什么?因为文件已经存在，计算机会报错吗?它会将文本附加到文件中，从而包含两个副本吗?还是会完全取代它?试着看看会发生什么，但是为了避免再次输入命令，可以使用向上箭头和向下箭头键来来回移动您使用过的命令的历史记录。按几次向上箭头到达第一只 cat，然后按 Enter 运行它，然后重复同样的操作到达第二只 cat。

如您所见，文件看起来是一样的。这并不是因为它保持原样，而是因为 shell 在将 cat 命令的输出写入文件之前清除了文件的所有内容。因此，在使用重定向时应该格外小心，以确保不会意外地覆盖所需的文件。如果你确实想追加而不是替换文件的内容，请使用>>:

```sh
cat t\* >> combined.txt
echo“我追加了一行!”> > combined.txt
cat combined.txt
```

为了方便起见，使用向上箭头再重复第一个 cat 几次，也许还可以添加一些任意的 echo 命令，直到文本文档非常大，以至于在使用 cat 显示时无法一次性放入终端。为了查看整个文件，我们现在需要使用一个不同的程序，称为分页器(因为它每次只显示一个“页”)。以前的标准分页器被称为 more，因为它在每个页面的底部放置一行“- more -”文本，表示您还没有阅读所有内容。如今，有一种更好的寻呼机可以替代它:因为它替代的更多，程序员决定称呼它为 less。

```sh
less combined.txt
```

当通过 less 查看文件时，您可以使用向上箭头，向下箭头，页面向上，页面向下，Home 和结束键来移动您的文件。给他们一个尝试，看看他们之间的区别。查看完文件后，按 q 退出 less 并返回到命令行。

### 关于 case 的注意事项

Unix 系统是区分大小写的，也就是说，它们认为" A.txt "和" A.txt "是两个不同的文件。如果你运行下面的代码行，你会得到三个文件:

```sh
echo “Lower case” > a.t txt
echo “Upper case” > A.TXT
echo “Mixed case” > A.t txt
```

一般情况下，应该尽量避免创建名称仅随大小写而变化的文件和文件夹。它不仅有助于避免混淆，而且还可以防止在使用不同的操作系统时出现问题。例如，Windows 是不区分大小写的，因此它会将上面的三个文件名视为一个文件，这可能会导致数据丢失或其他问题。

您可能会倾向于按“大写锁定”键，并将所有文件名都使用大写。但是绝大多数 shell 命令都是小写的，因此在键入时必须频繁地打开或关闭它。大多数经验丰富的命令行用户倾向于主要坚持用小写字母命名他们的文件和目录，这样他们很少需要担心文件名冲突，或名称中的每个字母使用哪种大小写。

**良好的命名实践**

当您同时考虑大小写和转义时，一个好的经验法则是保持文件名全部小写，只包含字母、数字、下划线和连字符。对于文件，通常在末尾还有一个点和几个字符来表示文件的类型(称为“文件扩展名”)。这条指导原则可能看起来有限制，但是如果您最终以任何频率使用命令行，那么您将很高兴坚持了这个模式。

## 移动和操作文件

现在我们已经有了一些文件，让我们看看您可能需要对它们执行的日常任务的类型。实际上，当你想移动、重命名或删除一两个文件时，你仍然很可能使用图形化程序，但知道如何使用命令行来做这件事对于批量更改或文件分散在不同文件夹中时是有用的。另外，在此过程中您还将了解更多关于命令行的知识。

首先，使用 mv (move)命令将我们的 combine .txt 文件放到 dir1 目录中:

```sh
mv combined.txt dir1
```

您可以通过使用 ls 确认作业已经完成，查看它是否从工作目录中丢失，然后使用 cd dir1 将其更改为 dir1, ls 查看它是否在那里，然后使用 cd ..将工作目录移动回来。或者你可以通过直接向 ls 命令传递一个路径来直接得到你想要的确认，从而节省大量的输入:

```sh
ls dir1
```

现在假设文件最终不应该在 dir1 中。让我们将其移回工作目录。我们可以 cd 到 dir1，然后使用 mv combine .txt ..将 combine .txt 移动到父目录。但是我们可以使用另一种路径快捷方式来避免更改目录。同样地，两个点(..)表示父目录，因此可以使用一个点(.)表示当前工作目录。因为我们知道 dir1 中只有一个文件，所以我们还可以使用“\*”来匹配该目录中的任何文件名，这样可以节省更多的按键操作。我们将文件移动回工作目录的命令因此变成了这样(注意点前的空格，有两个参数被传递给 mv):

```sh
mv dir1/* .
```

mv 命令还允许我们一次移动多个文件。如果传递两个以上的参数，则将最后一个参数作为目标目录，其他参数则被认为是要移动的文件(或目录)。让我们使用一个命令来移动 combine .txt，所有的 test_n.txt 文件和 dir3 到 dir2。这里还有更多，但如果你每次看每个论点，你应该能知道发生了什么:

```sh
mv combined.txt test_* dir3 dir2
ls
ls dir2
```

combine .txt 现在移到了 dir2 中，如果我们认为它又在错误的位置会发生什么?而不是 dir2，它应该放在 dir6，也就是 dir5 里面的那个，dir4 里面的那个。根据我们现在对路径的了解，这也不是问题:

```sh
mv dir2/combined.txt dir4/dir5/dir6
ls dir2
ls dir4 / dir5 / dir6
```

注意我们的 mv 命令如何让我们将文件从一个目录移动到另一个目录，尽管我们的工作目录完全不同。这是命令行的一个强大属性:无论您在文件系统的哪个位置，都可以操作位于完全不同位置的文件和文件夹。

由于我们似乎经常使用(和移动)该文件，也许我们应该在工作目录中保留它的副本。就像 mv 命令移动文件一样，cp 命令复制它们(再次注意点前的空格):

```sh
cp dir4/dir5/dir6/combined.txt .
ls dir4/dir5/dir6
ls
```

太棒了!现在让我们在工作目录中创建该文件的另一个副本，但使用不同的名称。我们可以再次使用 cp 命令，但不是给它一个目录路径作为最后一个参数，而是给它一个新的文件名:

```sh
cp combined.txt backup_combined.txt
ls
```

这很好，但也许选择一个备用名字会更好。为什么不重命名它，以便它总是在排序列表中出现在原始文件的旁边。传统的 Unix 命令行处理重命名时，就像将文件从一个名称移动到另一个名称一样，因此要使用我们的老朋友 mv 命令。在本例中，您只需指定两个参数:要重命名的文件和要使用的新名称。

```sh
mv backup_combined.txt
ls
```

这也适用于目录，为我们提供了一种方法，可以对前面创建的名称中带有空格的目录进行排序。为了避免在第一个命令之后重新输入每个命令，可以使用向上箭头在历史记录中拉出上一个命令。然后，您可以在运行命令之前编辑它，方法是使用方向键左右移动光标，使用退格键删除左边的字符，或使用 Delete 删除光标所在的字符。最后，在适当的位置输入新字符，完成后按 Enter 或 Return 运行命令。请确保您更改了每一行中数字的两个外观。

```sh
mv "folder 1" folder_1
mv "folder 2" folder_2
mv "folder 3" folder_3
mv "folder 4" folder_4
mv "folder 5" folder_5
mv "folder 6" folder_6
ls
```

### 删除文件和文件夹

---

**警告**

在下一节中，我们将开始删除文件和文件夹。为了绝对确保不会不小心删除主文件夹中的任何内容，在继续之前，使用 pwd 命令再次检查您是否仍然在/tmp/tutorial 目录中。

---

现在我们知道了如何移动、复制和重命名文件和目录。然而，考虑到这些只是测试文件，也许我们实际上并不需要 combine .txt 的三个不同副本。让我们稍微整理一下，使用 rm (remove)命令:

```sh
rm dir4/dir5/dir6/combined.txt combined_backup.txt
```

也许我们也应该删除一些多余的目录:

```sh
rm folder_*
```

![在目录上运行rm时出错](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Error%20when%20running%20rm%20on%20directories.png)

那里发生了什么?事实证明 rm 确实有一个小小的安全网。当然，您可以使用它用一个命令删除目录中的每一个文件，不小心在瞬间删除数千个文件，而且没有任何方法恢复它们。但是它不允许你删除目录。我认为这确实有助于防止您意外地删除数千个文件，但对于这样一个破坏性命令来说，在删除空目录时犹豫不决似乎有点小气。幸运的是，有一个 rmdir(删除目录)命令可以代替我们完成这项工作:

```sh
rmdir folder_*
```

![在非空目录上运行rmdir时出错](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Error%20when%20running%20rmdir%20on%20a%20non-empty%20directory.png)

好了一点，但还是有一个错误。如果运行 ls，您将看到大部分文件夹已经消失，但 folder_6 仍然存在。您可能还记得，folder_6 中仍然有一个文件夹 7，而 rmdir 将只删除空文件夹。再次强调，这是一个小的安全网，可以防止你无意中删除满是文件的文件夹。

然而，在这种情况下，我们确实打算这样做。对我们的 rm 或 rmdir 命令添加选项将让我们在没有安全网的帮助下执行危险的操作!对于 rmdir，我们可以添加一个-p 开关，告诉它也删除父目录。可以把它看作是 mkdir -p 的对应。因此，如果您要运行 rmdir -p dir1/dir2/dir3，它将首先删除 dir3，然后删除 dir2，最后删除 dir1。它仍然遵循正常的 rmdir 规则，只删除空目录，因此，例如，如果 dir1 中也有一个文件，则只删除 dir3 和 dir2。

当您非常非常确定要删除整个目录和其中的任何内容时，一种更常见的方法是通过使用-r 开关让 rm 递归地工作，在这种情况下，它将愉快地删除文件夹和文件。记住这一点，下面的命令可以去掉讨厌的 folder_6 和其中的子目录:

```sh
rm -r folder_6
ls
```

记住:尽管 rm -r 是快速和方便的，它也是危险的。最安全的方法是显式删除文件以清除目录，然后使用 cd ..在使用 rmdir 删除它之前。

**_重要的警告_**

与图形界面不同，rm 不会将文件移动到名为“trash”或类似的文件夹中。相反，它会彻底、彻底、不可挽回地删除它们。您需要非常小心使用 rm 时使用的参数，以确保您只删除您想要删除的文件。在使用通配符时应该特别小心，因为很容易意外地删除比预期更多的文件。命令中一个错误的空格字符可以完全改变它:rm t*表示“删除所有以 t 开头的文件”，而 rm t*表示“删除文件 t 以及名称包含零个或多个字符的任何文件，这将是目录中的所有内容!”如果你完全不确定，使用-i(交互式)选项对 rm，这将提示你确认每个文件的删除;输入 Y 删除它，N 保留它，按 Ctrl-C 完全停止操作。

## 一点管道工程

今天的电脑和手机拥有的图像和音频功能，是我们 70 年代的终端用户甚至无法想象的。然而，文本作为组织和分类文件的一种手段仍然盛行。无论是文件名本身、手机照片中嵌入的 GPS 坐标，还是存储在音频文件中的元数据，文本在计算的各个方面仍然扮演着至关重要的角色。幸运的是，Linux 命令行包含了一些用于操作文本内容的强大工具，以及将这些工具组合在一起以创建功能更强大的东西的方法。

让我们从一个简单的问题开始。txt 文件中有多少行?wc(字数)命令可以告诉我们，使用-l 开关来告诉它我们只需要行数(它也可以进行字符计数，顾名思义，也可以进行字数计数):

```sh
wc -l combined.txt
```

类似地，如果你想知道你的主目录中有多少文件和文件夹，然后自己整理，你可以这样做:

```sh
ls ~ > file_list.txt
wc -l file_list.txt
rm file_list.txt
```

这种方法是有效的，但是创建一个临时文件来保存 ls 的输出，只在两行之后删除它似乎有点过分。幸运的是，Unix 命令行提供了一个快捷方式，通过从一个命令(称为标准输出或 STDOUT)获取输出，并将其直接作为另一个命令(标准输入或 STDIN)的输入，可以避免创建临时文件。这就好像在一个命令的输出和下一个命令的输入之间连接了一个管道，以至于这个过程实际上被称为从一个命令到另一个命令的数据管道。下面是如何将 ls 命令的输出管道到 wc:

```sh
ls ~ | wc -l
```

注意，这里没有创建临时文件，也不需要文件名。管道完全在内存中运行，如果您不指定要使用的文件，大多数 Unix 命令行工具都希望从管道接收输入。查看上面的行，您可以看到它有两个命令，ls ~(列出主目录的内容)和 wc -l(计算行数)，它们由竖线字符(“|”)分隔。这种将一个命令连接到另一个命令的过程非常常用，以至于字符本身通常被称为管道字符，所以如果您看到这个术语，您现在就知道它只是指竖线。

注意，管道字符周围的空格并不重要，我们使用它们是为了清晰，但下面的命令也同样有效，这次是告诉我们/etc 目录中有多少项:

```sh
ls /etc|wc -l
```

唷!那可是相当多的文件。如果我们想把它们都列出来，它显然会占据不止一个屏幕。正如我们之前所发现的，当一个命令产生大量输出时，最好使用更少的输出来查看它，并且该建议仍然适用于使用管道(记住，按 q 退出):

```sh
ls /etc | less
```

回到我们自己的文件，我们知道如何获得 combine .txt 中的行数，但鉴于它是通过多次连接相同的文件创建的，我想知道有多少行是唯一的? Unix 有一个命令 uniq，它只输出文件中唯一的行。因此，我们需要 cat 文件，并通过 uniq 管道。但是我们想要的只是行数，所以我们还需要使用 wc。幸运的是，命令行不限制你一次只使用一个管道，所以我们可以继续连接我们需要的任意多的命令:

```sh
cat combined.txt | uniq | wc -l
```

这一行可能导致的计数非常接近于文件中的总行数，如果不是完全相同的话。这肯定不对吧?剪掉最后一个管道以查看命令的输出，以便更好地了解发生了什么。如果你的文件很长，你可能想要管道它通过更少，以使它更容易检查:

```sh
cat combined.txt | uniq | less
```

看来我们的重复行被删除的很少，如果有的话。要了解原因，我们需要查看 uniq 命令的文档。大多数命令行工具都附带一个简短(有时不那么简短)的操作手册，可以通过 man (manual)命令访问。输出是自动管道通过你的寻呼机，这通常会更少，所以你可以来回通过输出，然后按 q 当你完成:

```sh
man uniq
```

![uniq的手册页](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/The%20man%20page%20for%20uniq.png)

因为这种类型的文档是通过 man 命令访问的，所以您将听到它被称为“手册页”，就像在“查看手册页以获得更多详细信息”中那样。手册页的格式通常很简洁，可以将其视为命令的快速概述，而不是完整的教程。它们通常是高度技术性的，但你通常可以跳过大部分内容，只寻找你正在使用的选项或参数的细节。

uniq 手册页是一个典型的例子，它以命令的一行简短描述开始，然后是如何使用它的概要，然后是每个选项或参数的详细描述。但是，尽管手册页是无价的，它们也可能是不可逾越的。当您需要一个关于特定开关或参数的提醒时，最好使用它们，而不是作为学习如何使用命令行的一般资源。然而，man uniq 的 DESCRIPTION 部分的第一行确实回答了为什么重复的行没有被删除的问题:它只在相邻的匹配行上工作。

接下来的问题是如何重新排列文件中的行，使重复的条目位于相邻的行上。如果我们按字母顺序对文件的内容进行排序，就可以达到目的。Unix 提供了一个排序命令来做到这一点。对 man sort 的快速检查显示，我们可以直接将文件名传递给命令，所以让我们看看它对我们的文件做了什么:

```sh
sort combined.txt | less
```

你应该可以看到行已经重新排序，现在它适合直接管道到 uniq。我们最终可以完成计算文件中唯一行数的任务:

```sh
sort combined.txt | uniq | wc -l
```

正如您所看到的，将数据从一个命令传输到另一个命令(构建长链来操作数据)的能力是一个强大的工具，它还减少了对临时文件的需求，并为您节省了大量输入。因此，您将在命令行中经常看到它的使用。一开始，长长的命令链可能会让人望而生畏，但请记住，甚至可以将最长的命令链分解为单个命令(并查看它们的手册页)，以更好地理解它在做什么。

**许多手册**
大多数 Linux 命令行工具都包含一个手册页。试着简单看一下您已经遇到的一些命令的页面:man ls、man cp、man rmdir 等等。甚至还有 man 程序本身的 man 页面，当然是使用 man man 访问的。

## 命令行和超级用户

学习一些命令行基础知识的一个很好的理由是，在线指令通常倾向于使用 shell 命令而不是图形界面。如果这些指令要求对计算机进行修改，而不仅仅是修改主目录中的几个文件，那么您将不可避免地面临需要以计算机管理员(或 Unix 术语中的超级用户)身份运行的命令。在开始运行在 internet 某个黑暗角落找到的任意命令之前，有必要了解作为管理员运行的含义，以及如何发现那些需要它的指令，以便更好地判断它们运行起来是否安全。

超级用户，顾名思义，就是拥有超能力的用户。在旧的系统中，它是一个真正的用户，有一个真正的用户名(几乎总是“root”)，你可以登录，就像你有密码一样。至于那些超级功能:根用户可以修改或删除系统中任何目录中的任何文件，而不管这些文件是谁的;Root 用户可以重写防火墙规则或启动网络服务，这些服务可能会使计算机容易受到攻击;Root 可以关闭机器，即使其他人仍在使用它。简而言之，root 几乎可以做任何事情，可以轻松绕过通常为防止用户越界而设置的保护措施。

当然，一个以 root 身份登录的人也会像其他人一样犯错误。计算机历史的编年史中充满了这样的故事:输入错误的命令删除整个文件系统或杀死一个重要的服务器。此外，还存在恶意攻击的可能性:如果用户以根用户身份登录并离开他们的办公桌，那么对心怀不满的同事来说，跳上他们的机器进行破坏就不是太棘手了。尽管如此，由于人的本性，多年来许多管理员都因使用 root 作为主要或唯一的帐户而感到内疚。

**_不要使用 root 帐户_**
如果有人要求您启用 root 帐户，或以 root 身份登录，请非常怀疑他们的意图。

为了减少这些问题，许多 Linux 发行版开始鼓励使用 su 命令。这被描述为“超级用户”或“切换用户”的缩写，允许您在机器上更改为另一个用户，而不必注销和再次登录。当不带参数使用时，它假定您希望更改为根用户(因此是名称的第一个解释)，但您可以将用户名传递给它，以便切换到特定的用户帐户(第二次解释)。通过鼓励使用 su，目的是说服管理员花大部分时间使用普通帐户，只在需要时切换到超级用户帐户，然后使用注销命令(或 Ctrl-D 快捷键)尽快返回到他们的用户级帐户。

通过减少以 root 用户登录的时间，su 的使用减少了犯灾难性错误的机会。尽管如此，由于人的本性，许多管理员都有让长时间运行的终端打开的负罪感，他们在其中使用 su 切换到根帐户。在这方面，su 只是向安全迈出的一小步。

**_不要用 su_**
如果有人要求使用 su，请保持警惕。如果你使用的是 Ubuntu，默认情况下 root 帐户是禁用的，所以不带参数的 su 将不起作用。但还是不值得冒这个险，万一你没有意识到账户已经被启用了。如果您被要求使用带有用户名的 su，那么(如果您有密码)您将有权访问该用户的所有文件，并可能意外地删除或修改它们。

当使用 su 时，你的整个终端会话被切换到另一个用户。不需要 root 访问权限的命令，比如普通的 pwd 或 ls，将在超级用户的支持下运行，这增加了程序中错误导致重大问题的风险。更糟糕的是，如果您丢失了当前操作用户的信息，那么您可能会发出一个命令，该命令在作为用户运行时相当温和，但如果作为根用户运行，则可能会破坏整个系统。

最好是完全禁用根帐户，然后要求用户在每个命令的基础上特别请求超级用户权限，而不是允许具有危险能力的长寿命终端会话。这种方法的关键是一个名为 sudo 的命令(即“切换用户并执行此命令”)。

Sudo 用于给必须以超级用户权限运行的命令加上前缀。配置文件用于定义哪些用户可以使用 sudo，以及他们可以运行哪些命令。当运行这样的命令时，会提示用户输入自己的密码，然后将密码缓存一段时间(默认为 15 分钟)，因此，如果用户需要运行多个超级用户级别的命令，他们不会一直被要求输入密码。

在 Ubuntu 系统中，系统安装时创建的第一个用户被认为是超级用户。当添加一个新用户时，有一个选项可以将其创建为管理员，在这种情况下，他们还可以使用 sudo 运行超级用户命令。在这张 Ubuntu 18.04 的截图中，你可以看到对话框顶部的选项:

![Ubuntu 18.04添加用户对话框](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Ubuntu%2018.04%20add%20user%20dialog.png)

假设您在使用 sudo 的 Linux 系统上，并且您的帐户被配置为管理员，请尝试以下操作，看看当您试图访问一个被认为是敏感的文件(其中包含加密的密码)时发生了什么:

```sh
cat /etc/shadow
sudo cat /etc/shadow
```

![使用sudo](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/Using%20sudo.png)

如果在提示时输入密码，应该会看到/etc/shadow 文件的内容。现在通过执行 reset 命令清除终端，再次执行 sudo cat /etc/shadow 命令。这一次，文件将显示出来，而不会提示您输入密码，因为它仍然在缓存中。

**_小心 sudo_**
如果指示您使用 sudo 运行一个命令，请确保在继续之前理解该命令在做什么。使用 sudo 运行该命令可以获得与超级用户相同的所有功能。例如，软件发布者的站点可能要求您下载一个文件并更改其权限，然后使用 sudo 运行该文件。除非您确切地知道文件在做什么，否则您就打开了一个漏洞，恶意软件可能通过这个漏洞安装到您的系统中。Sudo 可能一次只运行一个命令，但该命令本身可以运行许多其他命令。将 sudo 的任何新用法视为与以 root 身份登录一样危险。

对于针对 Ubuntu 的指令，sudo 的常见外观是使用 apt 或 apt-get 命令将新软件安装到您的系统中。如果使用说明要求您首先使用 apt-add-repository 命令，通过编辑/etc/apt 中的文件，或使用“PPA”(个人包存档)，向您的系统添加一个新的软件存储库，您应该小心，因为这些源不是由 Canonical 管理的。但通常使用说明只要求您从标准存储库安装软件，这应该是安全的。

**安装新软件**
在 Linux 系统上安装软件有许多不同的方法。直接从发行版的官方软件库安装是最安全的选择，但有时你想要的应用程序或版本无法通过这种方式获得。当通过任何其他机制安装时，请确保您从相关项目的官方来源获得文件。

文件来自发行版存储库之外的迹象包括(但不限于)使用以下任何命令:curl、wget、pip、npm、make，或任何告诉您更改文件权限以使其可执行的指令。

Ubuntu 越来越多地使用“snaps”，这是一种新的包格式，通过更严格地限制程序以阻止它们访问系统中不需要的部分，提供了一些安全改进。但是有些选项可能会降低安全级别，因此，如果您被要求运行带有 snap install 的任何参数(而不是 snap 名称)的 snap install，那么有必要检查该命令到底要做什么。

让我们从标准的 Ubuntu 存储库中安装一个新的命令行程序来演示 sudo 的用法:

```sh
sudo apt install tree
```

一旦你提供了密码，apt 程序就会打印出好几行文本来告诉你它在做什么。这个树形程序很小，所以对大多数用户来说，下载和安装它应该不会超过一到两分钟。一旦返回到正常的命令行提示符，程序就安装好了，可以使用了。让我们运行它来更好地了解我们的文件和文件夹集合是什么样子的:

```sh
cd /tmp/tutorial
tree
```

![tree命令输出](./Linux%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%AE%80%E6%98%8E%E6%95%99%E7%A8%8B/The%20output%20of%20the%20tree%20command.png)

回到实际安装新程序的命令(sudo apt install tree)，它看起来与您到目前为止看到的那些命令略有不同。实际上它是这样工作的:

1. 在不带任何选项的情况下使用 sudo 命令时，将假定第一个参数是用于以超级用户权限运行的命令。任何其他参数都将直接传递给新命令。Sudo 的开关都以一个或两个连字符开始，并且必须紧接在 Sudo 命令之后，因此不会混淆行上的第二个参数是命令还是选项。

2. 这个命令在本例中是恰当的。与我们看到的其他命令不同，这个命令不能直接处理文件。相反，它期望它的第一个参数是要执行(安装)的指令，其余的参数会根据该指令而变化。

3. 在本例中，install 命令告诉 apt 命令行的其余部分将由一个或多个包名组成，要从系统软件库中安装。通常这将向机器中添加新软件，但软件包可能是需要安装到特定位置的任何文件集合，如字体或桌面图像。

您可以将 sudo 放在任何命令前面以超级用户的身份运行它，但很少有必要这样做。甚至系统配置文件通常也可以作为普通用户查看(使用 cat 或 less)，如果需要编辑它们，只需要 root 权限。

**小心 sudo su**
使用 sudo 的一个技巧是使用它来运行 su 命令。这将为您提供一个根 shell，即使根帐户被禁用。当您需要以超级用户的身份运行一系列命令时，它可能很有用，以避免在所有命令前都加上 sudo，但它会使您面临与上面为 su 所描述的完全相同的问题。如果您按照任何指示运行 sudo su，请注意之后的每个命令都将以 root 用户运行。

在本节中，您已经了解了根帐户的危险，以及像 Ubuntu 这样的现代 Linux 系统如何通过使用 sudo 来降低危险的风险。但是，任何使用超级用户能力的行为都应该慎重考虑。当遵循你在网上找到的指令时，你现在应该能够更好地发现那些可能需要更仔细检查的命令。

## 隐藏文件

在结束本教程之前，有必要提一下隐藏文件(和文件夹)。这些文件通常在 Linux 系统上用于存储设置和配置数据，通常是隐藏起来的，这样它们就不会打乱您自己文件的视图。隐藏的文件或文件夹没有什么特别的，除了它的名称:只需在名称的开头用一个点(“。”)就足以使它消失。

```sh
cd /tmp/tutorial
ls
mv combined.txt .combined.txt
ls
```

你仍然可以通过确保在指定文件名时包含圆点来使用隐藏文件:

```sh
cat .combined.txt
mkdir .hidden
mv .combined.txt .hidden
less .hidden/.combined.txt
```

如果运行 ls，您将看到.hidden 目录被隐藏了，正如您所预料的那样。你仍然可以使用 ls .hidden 来列出它的内容，但是因为它只包含一个文件，它本身是隐藏的，你不会得到太多的输出。但是你可以使用-a (show all)切换到 ls，让它显示目录中的所有内容，包括隐藏的文件和文件夹:

```sh
ls
ls -
ls .hidden
ls -a .hidden
```

注意我们之前使用的快捷方式。和. .，它们看起来也像是真正的目录。

至于我们最近安装的 tree 命令，它以类似的方式工作(除了没有通过.和..):

```sh
tree
tree -a
```

切换回您的主目录(cd)并尝试运行 ls，先不带-a 开关，然后再带-a 开关。通过 wc -l 管道输出，可以让您更清楚地了解一直以来有多少隐藏的文件和文件夹就在您的眼皮底下。这些文件通常存储您的个人配置，这也是 Unix 系统一直提供系统级设置(通常在/etc 目录中)的功能的原因，这些设置可以被个人用户覆盖(通过他们的主目录中的隐藏文件)。

您通常不需要处理隐藏文件，但偶尔可能会有指令要求您将 cd 导入.config，或编辑一些名称以点开头的文件。至少现在您可以理解发生了什么，即使您无法在图形化工具中容易地看到该文件。

### 清理

本教程已经结束，现在您应该回到了您的主目录(使用 pwd 检查，如果没有检查则使用 cd 检查)。让你的电脑保持我们发现它时的状态是礼貌的，所以作为最后一步，让我们删除我们之前使用的实验区域，然后再次检查它是否真的消失了:

```sh
rm -r/tmp/tutorial
ls /tmp
```

最后一步，让我们关闭终端机。您可以直接关闭窗口，但是注销 shell 是更好的做法。您可以使用 logout 命令，也可以使用 Ctrl-D 键盘快捷方式。如果你打算经常使用终端，记住 Ctrl-Alt-T 启动终端，Ctrl-D 关闭终端，很快就会让它感觉像一个方便的助手，你可以立即调用，也可以很容易地关闭它。

## 结论

本教程只是简单介绍了 Linux 命令行。我们已经了解了在文件系统中移动和操作文件的一些常用命令，但是没有教程能够提供对所有可用命令的全面指导。更重要的是，您已经了解了使用 shell 的关键方面。您已经了解了在网上可能遇到的一些广泛使用的术语(和同义词)，并深入了解了典型 shell 命令的一些关键部分。您已经学习了绝对路径和相对路径、参数、选项、手册页、sudo 和根、隐藏文件等。

有了这些关键概念，您应该能够更好地理解遇到的任何命令行指令。即使您不能理解每一个命令，您至少应该知道一个命令在哪里停止，下一个命令在哪里开始。您应该能够更容易地知道他们正在操作哪些文件，或者正在使用哪些其他开关和参数。通过参考手册页，您甚至可以确切地收集到命令在做什么，或者至少获得一个大致的概念。

我们在这里所介绍的内容很少可能使您放弃图形化文件管理器，转而使用提示符，但是文件操作并不是真正的主要目标。然而，如果您对通过几次按键就能影响硬盘驱动器不同部分的文件的能力感兴趣，那么还有很多东西需要您学习。

### 进一步的阅读

关于命令行有许多在线教程和商业出版的书籍，但是如果你想更深入地了解这个主题，下面的书可能是一个很好的起点:

- William Shotts 的[Linux 命令行](http://linuxcommand.org/tlcl.php)

特别推荐这本书的原因是，它是在知识共享许可下发布的，并且可以作为 PDF 文件免费下载，这对于不确定自己有多想使用命令行的初学者来说是理想的。如果您发现自己被命令行错误捕获并需要纸质参考，它也可以作为打印卷提供。
