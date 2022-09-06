---
title: Anaconda、Pycharm、Python使用方法整理(windows 10)
tags:
  - null
categories:
  - Python
description: Win10下，基于Anaconda、Pycharm的Python环境搭建详细教程
keywords: 'Python, Anaconda安装及使用, Pycharm, 配置python环境'
abbrlink: be8ba79e
date: 2022-09-02 17:17:00
updated:
top_image:
cover:
---

# 前言

本文记录安装Anaconda和Pycharm的全过程，以及遇到的一些问题和解决方法

安装配置顺序为：纯Python/Anaconda-->Pycharm

# Anaconda篇

> Anaconda对于python初学者而言及其友好，相比单独安装python主程序，选择Anaconda可以帮助省去很多麻烦，Anaconda里添加了许多常用的功能包，如果单独安装python，这些功能包则需要一条一条自行安装，在Anaconda中则不需要考虑这些，同时Anaconda还附带捆绑了两个非常好用的交互式代码编辑器（Spyder、Jupyter notebook）。
>
> [Conda](https://so.csdn.net/so/search?q=Conda&spm=1001.2101.3001.7020)是一个开源的包、环境管理器，可以用于在同一个机器上安装不同版本的软件包及其依赖，并能够在不同的环境之间切换。
>
> 
>
> Anaconda安装、配置：
>
> - [Anaconda详细安装及使用教程（带图文）- CSDN](https://blog.csdn.net/ITLearnHall/article/details/81708148)
> - [windows下Anaconda的安装与配置 - 脚本之家](https://www.jb51.net/article/137772.htm)
>
> 配置镜像地址：
>
> - [conda upgrade --all 失败解决方案](https://blog.csdn.net/JohnnyRian/article/details/88213063)
>
> 修改虚拟环境安装地址：
>
> - [Anaconda安装虚拟环境到指定路径 - 博客园](https://www.cnblogs.com/lemonbit/p/7068091.html)
> - [Anaconda下安装虚拟环境到指定路径 - CSDN](https://blog.csdn.net/baigua3362/article/details/101559799)
> - [一文解决安装Anaconda后C盘不断增加的问题、修改默认配置 - CSDN](https://blog.csdn.net/Chenftli/article/details/124901260)
>
> 
>
> **几个重要注意事项（后面都有相关对应案例！！！）**：
>
> - [安装Anaconda时，不要选择“All uers”，而应该选择当前用户](#跳转1)
> - [要习惯用“管理员权限”打开CMD，在输入相关命令，可以避免由于文件夹权限不足等受到限制](#跳转2)

## 1. 安装及初始环境配置

### 1.1 下载地址

可以通过[Anaconda官网](https://www.anaconda.com/products/distribution)下载，不过速度一般；另外可以通过[清华镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)进行下载

### 1.2 配置环境变量

如果是windows的话需要去 控制面板\系统和安全\系统\高级系统设置\环境变量\用户变量\PATH 中添加 anaconda的安装目录的Scripts文件夹，例如默认安装路径C:\ProgramData\Anaconda3\Scripts，看个人安装路径不同需要自己调整。

之后就可以打开命令行(最好用管理员模式打开) 输入 `conda --version`，如果输出conda 4.5.4之类的就说明环境变量设置成功了.

为了避免可能发生的错误，需要在命令行输入`conda upgrade --all` 先把所有工具包进行升级



**注意以下几点**：

除了在“用户变量/PATH”中添加，也可以在“系统变量/PATH”中添加Scripts文件夹，重点在于需要将该路径置于PATH变量下：

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220808102807618.png" alt="image-20220808102807618" style="zoom: 80%;" />



但需要注意的是，**一定不能直接在用户变量/系统变量中新建一个变量**，路径指定为Scripts文件夹：

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220808104319394.png" alt="image-20220808104319394" style="zoom:80%;" />



具体原因参考用户变量和系统变量的区别：

- 环境变量没有区分大小写，例如path跟PATH是一样的 
- 系统变量对所有用户有效
- 用户变量只对当前用户有效
- 用户变量与系统变量，名称是变量，值是里面的内容，也就是通过变量存储了想要存储的内容，方便调用
- 系统变量与用户变量的PATH：告诉系统可执行文件放在什么路径（平常执行程序的路径，***要放在PATH里面，不能新建一个变量，cmd会提示“不是内部或外部命令，或者不是可执行程序”***）
- windows系统在执行用户命令时，若用户未给出文件的绝对路径，则首先在当前目录下寻找相应的可执行文件、批处理文件等
- 如果当前目录找不到对应文件名的程序，在系统变量的PATH的路径中，依次寻找对应的可执行程序文件（查找顺序是按照路径的录入顺序从左往右寻找的，最前面一条的优先级最高，如果找到程序就停止寻找，后面的路径不再执行）
- 如果系统变量的PATH的路径找不到，再到用户变量的PATH路径中寻找（如果系统变量和用户变量的PATH中同时包含了同一个命令，则优先执行系统变量PATH中的命令）
- ***每次新加了命令以后，要确定保存了。再重启CMD***，否则命令不生效的
- 在CMD里要输出环境变量 ECHO %变量名%



### 1.3 同时自动安装的程序

在 Windows 上，会随 Anaconda 一起安装一批应用程序：

- Anaconda Navigator，它是用于管理环境和包的 GUI
- Anaconda Prompt 终端，它可让你使用命令行界面来管理环境和包
- Spyder，它是面向科学开发的 IDE

为了避免报错，推荐在默认环境下更新所有的包。打开 Anaconda Prompt （或者 Mac 下的终端），键入：

```
conda upgrade --all
```

并在提示是否更新的时候输入 y（Yes）以便让更新继续。初次安装下的软件包版本一般都比较老旧，因此提前更新可以避免未来不必要的问题。

> 若不更新，后续使用时可能会出现报错



## 2. 配置镜像地址(更换为清华镜像)

修改配置文件下载地址，**修改为清华镜像**：

```
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --set show_channel_urls yes
```

> 注意以下两点：
>
> - 在CMD中输入以上代码后，无需按照网上某些教程修改本地配置文件`C:\用户\用户名\.condarc`，已经自动修改好
> - 此处清华镜像地址应**以http开头**，而不是原先的https，否则会因为SSL验证无法连接，原因及其它解决方法见[清华源连接失败原因与解决](https://blog.csdn.net/kxqt233/article/details/121167753)



再次在 Anaconda Prompt 中执行`conda upgrade --all`更新即可

查看当前配置命令:

```
conda config --show
```

配置完后重启一下即可成功



## 3. 安装/卸载第三方包

需要安装所需的第三方包时，在CMD中输入以下指令来安装requests包：

```
conda install requests_name
```

或者

```
pip install requests_name
```

> PyPi地址在国外，因为有墙的原因所以有些地区使用pip安装第三方库的时候会出现下载慢甚至严重的无法访问导致安装失败。通过更换pip镜像源为国内地址可以解决上述问题。这里使用**豆瓣的镜像源**为例：
>
> ```
> pip install requests_name -i https://pypi.douban.com/simple
> ```



以安装numpy包为例，安装完成后可验证是否安装成功：

在CMD/Anaconda Powershell Prompt中输入python进入解释器中，输入` import numpy `，若不报错即安装成功。可输入` help(numpy)`查看该包的详细信息。

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220808175316987.png" alt="image-20220808175316987"  />

> 目前存在两种情况***（暂且无法解释）***：
>
> - 若在Anaconda Powershell Prompt中安装第三方包，则只能在Anaconda Powershell Prompt中输入` import numpy `显示安装成功，在CMD中则会显示“未安装numpy”。
>
>   > 有一种解释是：
>   >
>   > CMD基本上都是默认在系统盘上的操作，而对于Anaconda自带的命令窗口，所有可以在CMD中运行的都可以在这里运行，只不过文件的路径改变了（改变为Anaconda的安装目录下）。例如在这两个命令窗口中分别输入ipython.exe notebook，默认的文件.ipynb存储在不同的位置。
>   >
>   > ![示例](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/201801041523279.png)
>
>   
>
> - 通过`conda install numpy`无法安装numpy包，而通过`pip install numpy`可以成功安装
>
>   > 可能是conda中不包含numpy包？



### **附：pip和conda的区别**

> 来自Anaconda[官方文章](https://www.anaconda.com/blog/understanding-conda-and-pip)

​		Conda和pip通常被认为是几乎相同的。尽管这两个工具的某些功能重叠，但它们是经过设计的，并用于不同的目的。[Pip](https://pip.pypa.io/en/stable/)是 Python Packaging Authority 推荐的源自[Python 包索引](https://pypi.org/)的用于安装包的工具。Pip 用于安装Python软件包，例如wheel或源代码。后者可能要求系统在调用pip成功之前安装兼容的编译器和可能的库。

​		[Conda](https://conda.io/docs/)是一个跨平台的包和环境管理器，从[Anaconda 存储库](https://repo.anaconda.com/)从[Anaconda Cloud](https://anaconda.org/)安装和管理Conda包。Conda 包是二进制文件，永远不需要使用编译器来安装它们。此外，**conda包不限于 Python 软件，它们还可能包含 C 或 C++ 库、R 包或任何其他软件**。这突出了 conda 和 pip 之间的关键区别：Pip 安装 Python 包，而 conda 安装可能包含以任何语言编写的软件包。例如，**在使用 pip 之前，必须通过系统包管理器或下载exe程序文件来安装 Python 解释器。另一方面，Conda 可以直接安装 Python 包和 Python 解释器**。

​		这两个工具之间的另一个关键区别是**conda能够创建可以包含不同版本 Python 和/或 安装在其中的包的隔离环境**。这在使用数据科学工具时非常有用，因为不同的工具可能包含相互冲突的要求，因此不可以全部安装到单个环境中。相反的，**Pip 没有对环境的内置支持，而是依赖于其他工具，例如[虚拟环境(virtualenv)](https://virtualenv.pypa.io/en/latest/)或者[venv](https://docs.python.org/3/library/venv.html)创建孤立的环境**。工具例如[pipenv](https://pipenv.readthedocs.io/en/latest/)，[poetry](https://poetry.eustace.io/)， 和[hatch](https://github.com/ofek/hatch)用于包装 pip 和 virtualenv，以提供一个统一的方法来处理这些环境。

​		Pip 和 conda 在实现环境中的依赖关系方面也有所不同。安装包时，pip 在递归的串行循环中安装依赖项。没有努力确保同时满足所有包的依赖关系。如果较早按顺序安装的软件包相对于较晚安装的软件包具有不兼容的依赖版本，这可能会导致环境以某种方式被破坏。相比之下，conda 使用可满足性 (SAT) 求解器来验证是否满足环境中安装的所有软件包的所有要求。此检查可能需要额外的时间，但有助于防止创建损坏的环境。只要有关依赖项的包元数据是正确的，conda 就可以预见地产生工作环境。

​		鉴于 conda 和 pip 之间的相似性，一些人尝试结合这些工具来创建数据科学环境也就不足为奇了。**将 pip 与 conda 结合的一个主要原因是可能存在一个或多个包只能通过 pip 安装**。Anaconda 存储库中提供了 1,500 多个软件包，包括最流行的数据科学、机器学习和 AI 框架。这些，以及 Anaconda 云上提供的数千个额外的包，包括[conda-forge](https://conda-forge.org/)和[bioconda](https://bioconda.github.io/), 可以使用 conda 安装。**尽管有这么多的包集合，但Anaconda 存储库与 PyPI 上超过 150,000 个包相比，它仍然可能是不足的**。可能存在没有被 conda package提供的软件包，但它可以在 PyPI 上使用，并且可以使用 pip 安装。***在这些情况下，应该尝试同时使用 conda 和 pip***。

|                        |     Conda     |               Pip               |
| :--------------------: | :-----------: | :-----------------------------: |
|        manages         |   binaries    |         wheel or source         |
| can require compilers? |      no       |               yes               |
|     package types      |      any      |           Python only           |
|   create environment   | yes, built-in | no, requires virtualenv or venv |
|   dependency checks    |      yes      |               no                |

> 注：在安装Anaconda后，会自行安装对应版本的python（Anaconda的安装目录下），无需重新单独安装python



## 4. 管理虚拟环境（基于命令行窗口）

用anaconda来创建我们一个个独立的python环境。接下来的例子都是在命令行操作的：

> 可以在CMD或Anaconda Powershell Prompt直接输入python试试, 这样会进入base环境的python解释器, 如果你把原来环境中的python环境去除掉会更能体会到, 这个时候在命令行中使用的已经不是你原来的python而是base环境下的python.而命令行前面也会多一个(base) 说明当前我们处于的是base环境下。

**（1）创建虚拟环境：**

当不满足一个base环境时，可以为自己的程序安装单独的虚拟环境。创建一个**名称为python34**的虚拟环境并指定python版本为3.4（这里conda会自动找3.4中最新的版本下载）：

```
conda create -n python34 python=3.4
```

或者

```
conda create --name python34 python=3.4
```



**（2）切换环境：**

```
activate environment_name
```

如果忘记了名称我们可以先用`conda env list`去查看所有的环境。



**（3）为创建的环境安装/卸载包：**

新创建的环境除了python自带的一些官方包之外是没有其他包的, 一个比较干净的环境。我们可以试试在虚拟环境下，先输入python打开python解释器，然后输入`import requests`，会报错找不到requests包，这是很正常的。按照需求，对新建的环境安装所需包即可。

*安装包*：（安装完成之后我们再输入python进入解释器并`import requests`, 这次一定就是成功的了）

```
conda install requests_name
```

或者

```
pip install requests_name
```



*卸载包*：

```
conda remove requests_name
```

或者

```
pip uninstall requests_name
```



**（4）卸载环境：**

```
conda remove --name environment_name --all
```



**（5）环境相关指令总结：**

```
# 创建一个名为faultcode的环境，指定Python版本是3.9（不用管是3.9.x，conda会为我们自动寻找3.9.x中的最新版本）
# 创建好的环境可以在Anaconda Navigator--environment中查看
conda create --name faultcode python=3.9
# 或者
conda create -n faultcode python=3.9
 
 
# 安装好后，使用activate切换到该环境
activate faultcode                 # for Windows
source activate faultcode          # for Linux & Mac

 
# 激活后，会发现terminal输入的地方多了faultcode的字样，实际上，此时系统做的事情就是把默认2.7环境从PATH中去除，再把3.9对应的命令加入PATH
# 此时，再次输入
python --version
# 可以得到`Python 3.9.5 :: Anaconda 4.1.1 (64-bit)`，即系统已经切换到了3.9的环境
# 在该虚拟环境下便可以像base环境中一样进行设置、安装所需的包等操作
 
 
# 如果想离开这个环境，返回默认的环境，运行
deactivate                         # for Windows
source deactivate                  # for Linux & Mac


# 删除一个已有的环境
conda remove --name faultcode --all
# 或者
conda remove -n faultcode --all


# 列出conda管理的所有环境
# 如果忘记了环境的名称，可以列出你创建的所有环境。你会看到环境的列表，而当前所在环境的旁边会有一个星号。
# 默认的环境（即当你不在选定环境中时使用的环境）名为 root。
conda env list
# 或者
conda info -e
```

> anaconda所谓的创建虚拟环境其实就是安装了一个真实的python环境, 只不过我们可以通过activate，conda等命令去随意的切换我们当前的python环境, 用不同版本的解释器和不同的包环境去运行python脚本。



**（6）其它的常用命令：**

```
conda info                   # 列出Anaconda的所有信息，包括conda version、python version、package cache、envs 								directories等

conda config --show          # 查看Anaconda的详细配置信息

conda create --help          # 查看与create相关的help文档信息

activate                     # 切换到base环境

conda list                   # 列出当前环境的所有包

conda install requests_name  # 安装requests_name包

conda remove requests_name   # 卸载requets_name包

conda update requests_name   # 更新requests包

conda env export > environment.yaml   # 导出当前环境的包信息

conda env create -f environment.yaml  # 用配置文件创建新的虚拟环境
```



## 5. 修改Anaconda虚拟环境的创建路径

首先，明确如何查看Anaconda虚拟环境的创建路径

输入以下命令

```
conda info
```

或者

```
conda config --show 
```

查看虚拟环境创建位置

![image-20220812181036188](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220812181036188.png)

> 可见虚拟环境的默认创建路径为C:\Users\User_name\\.conda\envs*(也有可能直接默认Anaconda安装目录下的envs文件夹)*
>
> 如果按照[第四节](#4. 管理虚拟环境（基于命令行窗口）)方法创建的虚拟环境，由于使用`-n`或者`--name`命令，会将虚拟安装在C盘默认安装路径的envs目录下。
>
> 为避免造成C盘空间被占用，采用以下两种方法修改虚拟环境安装路径到想要的文件夹。

### 5.1 不修改默认创建路径

以在G:\Anaconda\envs中创建名为faultcode的虚拟环境为例，输入相应的命令：

```
conda create --prefix=G:\Anaconda\envs\faultcode python=3.9
```

> 注意：
>
> 路径G:\Anaconda\envs是目标文件夹，faultcode是

在这个命令中，路径G:\Anaconda\envs是目标文件夹(若没有则自动建立)，faultcode是需要创建的虚拟环境名称。创建完成后，虚拟环境的全称应**包含整个路径**，为`G:\Anaconda\envs\faultcode`，后续在调用时需要将它完整输入。激活指定路径下的虚拟环境的命令如下：

```
activate G:\Anaconda\envs\faultcode
```

想要删除指定路径下的虚拟环境，使用如下的命令：

```
conda remove --prefix=G:\Anaconda\envs\faultcode --all
```

此外，在base环境中**直接**为虚拟环境安装软件包的指令为：

```
conda install -prefix=G:\Anaconda\envs\faultcode package_name
```

注意，如果在默认路径下安装的虚拟环境添加包，则命令是

```
conda install -n faultcode package_name
```



### 5.2 修改默认创建路径

方法一比较麻烦，需要随时记住完整路径，可以考虑直接修改默认创建路径。

对应两种解决方式：一种是通过添加dir来替换默认路径，一种是直接配置c盘路径下的.condarc文件

<span id="跳转1">需要注意的是，若按照网上常规的方法，例如[Anaconda更改虚拟环境安装位置 - CSDN](https://blog.csdn.net/weixin_44622686/article/details/125011729)，虽然貌似已经修改了默认创建路径，但实际操作后可能会发现仍然是创建到原先的C盘路径，**出现这种情况的原因是在安装Anaconda时选择的是All User，而不是Just Me**。</span>

上述两种“解决方法”一定是在**安装Anaconda时选择的是Just me**，否则无法生效！！！

> 当然，如果不小心安装时选择了All User，也可以解决：
>
> - <span id="跳转2">以管理员身份运行CMD，再运行命令</span>
>
> （这样也可以解决`conda upgrade all`时由于anaconda文件夹权限不足，部分软件包无法安装的情况）
>
> - 修改anaconda安装文件夹的权限，属性->安全->Users 权限全部允许（有可能无法生效）



#### 5.2.1 通过添加dir来替换默认路径

在CMD中输入`conda config --show`后，会发现虚拟环境目录envs_dirs有多条，其实默认我们会先使用第一个目录，要通过修改配置来重新确定默认环境路径。首先明确修改配置的语法：

```
conda config --add key value       #添加语法
conda config --remove key value    #删除语法
```

其中，key为 envs_dirs、pkgs_dirs等，value为key对应的值。

这里如果只保留想用的G:\Anaconda\envs路径，将其它目录全部删除，例如：

```
conda config --remove envs_dirs dir(虚拟环境路径)
```

则会报下面的错误：

```
CondaKeyError: ‘pkgs_dirs’: key ‘pkgs_dirs’ is not in the config file
```

原因是这个只能删除在我们user路径下的.condarc文件的内容，及我们用户配置的内容。所以我们不能通过删除来解决。只能通过添加路径替换默认路径解决。

```
conda config --add envs_dirs dir（路径）
```

> 若是添加原来已经有的路径，则会发现这个路径变成了环境目录的第一个，可以用来调整envs_dirs安装顺序



#### 5.2.2 直接配置c盘路径下的.condarc文件

在用户路径下修改.condarc，在`C:\Users\User_name\.condarc`下

添加下面配置：

```
channels:
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
  - defaults
show_channel_urls: true
envs_dirs:
  - G:\Anaconda\envs
pkgs_dirs:
  - G:\Anaconda3\pkgs
  - C:\Users\User_name\.conda\envs
  - C:\Users\User_name\AppData\Local\conda\conda\envs
```

添加了清华源、同时改了envs_dirs、pkgs_dirs。


# Pycharm篇

> 注：Anaconda应在Pycharm之前安装，可能会方便后续的设置
>
> 
>
> Pycharm使用教程：
>
> - [Pycharm编辑器教程 - 慕课网](https://www.imooc.com/wiki/pycharmlesson/introduce1.html)
>
>   > 注：文本教程，不是视频
>
> “基于纯python环境”方法：
>
> - [Pycharm配置环境及安装第三方库 - 简书](https://www.jianshu.com/p/bdeb237af302)
>
> pycharm 创建运行、调试配置：
>
> - [在 PyCharm 里创建运行/调试配置 - 慕课网](https://www.imooc.com/wiki/pycharmlesson/runningconfig.html)

## 1. 配置环境及安装第三方库

### 1.1 基于纯python环境

#### ***配置Python环境***

打开软件，通过路径【File】→【Settings】→【Project】→【Project Interpreter】来到我们配置Python环境的界面。一般情况下，这里是一片空白。

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/1.webp" alt="1" style="zoom:90%;" />



点击小齿轮，在弹出的选项中点击【Show All】，然后再弹出的窗口中点击【+】号，进入配置页面。

![2](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/2.webp)



这里可以选择【New Environment】或【Existing Environment】，建议选择【Existing Environment】，然后根据自己安装Python的路径，找到Python.exe，然后勾选【make avaliable to all projects】，将该Python环境应用到所有的项目，最后点击【OK】。

![3](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/3.webp)



这个时候我们会来到这个页面，这里是我们当前配置的Python环境中包含的库信息，点击【OK】，即可完成我们的Python环境配置。

![4](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/4.webp)



#### ***安装第三方库***

安装第三方库，我们有两种方法，第一种方法是使用`pip`命令。比如我们要安装lxml库，打开命令提示符，输入`pip install lxml`，然后回车，等待一会即可完成。

![5](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/5.webp)



这个时候，我们再回到Pycharm的环境配置页面，可以看到lxml库已经成功导入。

![6](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/6.webp)



第二种方法，我们可以直接来到我们的Pycharm的环境配置页面，点击【+】号，然后搜索并选中我们需要的第三方库，点击【Install Package】即可进行安装。

![7](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/7.webp)



#### ***注意事项***

1.我们在配置Python环境的时候，如果选择【New Environment】，需要**将【location】路径设置成一个空白文件夹**，然后找到我们安装的Python，这个时候，Pycharm会将已安装的Python复制到这个空白文件夹中，***构建一个新的Python环境***。

2.使用pip安装第三方库是有默认路径的，所以如果想成功使用pip安装第三方库，需要满足以下两个条件：电脑中只安装了一个Python；在配置Python环境的时候，选择的是【Existing Environment】。

3.如果我们使用pip安装第三方库，但是安装之后，Pycharm中没有成功导入，这个时候建议大家使用**第二种方式**进行安装。



### 1.2 基于Anaconda创建的环境

#### ***配置python环境***

首先要通过Anaconda创建一个虚拟环境，以前面建立的faultcode为例为pycharm创建环境(路径为`Anaconda的安装目录\envs\faultcode`)

同样地，通过路径【File】→【Settings】→【Project】→【Project Interpreter】来到我们配置Python环境的界面。点击小齿轮，在弹出的选项中点击【Show All】，然后再弹出的窗口中点击【+】号，进入配置页面。

![2](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/2.webp)



纯python是进入`Virtualenv Environment`，基于Anaconda则选择`Conda Enveronment`。

这里可以选择【New Environment】或【Existing Environment】，建议选择【Existing Environment】，然后根据前面创建的虚拟环境"faultcode"的路径，找到相应文件夹下的Python.exe，点击【OK】。

> 虚拟环境的好处在于：
>
> 可以对每个项目创建专属的配置环境和软件包，避免冲突，因此此处可以不勾选“make available to all projects”

![image-20220814145400671](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814145400671.png)



来到这个页面，这里是我们当前配置的Python环境中包含的库信息，包含了之前虚拟环境“faultcode”中安装的各个软件包。点击【OK】，即可完成我们的Python环境配置。

![image-20220814145828621](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814145828621.png)



#### ***安装第三方库***

也是同上的两种方法:

- 第一种方法是在CMD使用`pip`命令或者`conda`命令，输入`activate environment_name`转换到。比如我们要安装PyQt5库，打开命令提示符，输入`pip install PyQt5`，然后回车，等待一会即可完成。
- 第二种方法，直接来到我们的Pycharm的环境配置页面，点击【+】号，然后搜索并选中我们需要的第三方库，点击【Install Package】即可进行安装。



### 1.3 Pycharm创建运行、调试配置

> run/debug configuration

参考

- [在 PyCharm 里创建运行/调试配置 - 慕课网](https://www.imooc.com/wiki/pycharmlesson/runningconfig.html)
- [PyCharm 配置 Python 解释器](https://www.imooc.com/wiki/pycharmlesson/interpreter1.html)

自己的配置（目前可正常运行）：

![image-20220814152607159](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814152607159.png)



### 1.4 其它技巧

#### ***界面汉化***

在`Settings-Plugin`下载插件`Chinese(Simplified) Language Pack/中文语言包`即可



#### ***查看当前虚拟环境的软件包***

如图所示：

![image-20220814152847266](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814152847266.png)



#### ***常用快捷键(Windows)***

![keyboard shortcuts](https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/5ee64e0608c4fa0416000953.jpg)

**常用快捷键：**

- **Ctrl + Enter(⌘ ↩)**：在下方新建行但不移动光标；
- **Shift + Enter(⇧ ↩)**：在下方新建行并移到新行行首；
- **Ctrl + /(⌘ /)**：注释(取消注释)选择的行；
- **Ctrl + Alt + L(⌥ ⌘ L)**：格式化代码；
- **Ctrl + Shift + +/-(⇧⌘ + / ⇧⌘ -)**：展开/收缩所有的代码块；
- **Ctrl + Shift + Enter(⇧ ⌘ ↩)**：完成语句；
- **Ctrl + Alt + I(⌃ ⌥ I)**：自动缩进行；
- **Alt + Enter(⌥ ↩)**：优化代码，提示信息实现自动导包；
- **Ctrl + B(⌘ B)**：显示对象声明信息；
- **Double Shift(Double ⇧)**：搜索所有类型对象；
- **Ctrl + E(⌘ E)**：最近打开的文件；
- **Ctrl + Shift + N (⇧⌘ N)**：查找项目中的任何文件。



#### ***查看运行过程中的变量值***

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220816170722042.png" alt="image-20220816170722042" style="zoom:80%;" />

在Pycharm界面的右上方，点击运行栏的这个灰色向下箭头，选择`Edit Configurations`，在接下来出现的窗口中，勾选`run with Python console`

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220816170821626.png" alt="image-20220816170821626" style="zoom: 55%;" />

设置完成后重启Pycharm，运行程序，点击`show variables`就会出现查看变量的窗口

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220816170939520.png" alt="image-20220816170939520" style="zoom: 80%;" />

变量窗口：

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220816171044005.png" alt="image-20220816171044005" style="zoom: 80%;" />





## 2. 安装、使用PyQt5及相关库

安装有两种方法：

- pycharm中(Settings-Project-Project Interpreter)直接搜索并安装
- 在CMD中为Anaconda创建的虚拟环境添加软件包

分别参考：

- [PyCharm安装PyQt5及其工具(Qt Designer、PyUIC、PyRcc)详细教程 - CSDN](https://blog.csdn.net/qq_32892383/article/details/108867482)
- [PyQt5+Pycharm安装和配置 - CSDN](https://blog.csdn.net/zhangziju/article/details/80243858)

> 在找Qt Designer、PyUIC、PyRcc的exe文件时，可能位置有所不同，根据实际情况确定位置.
>
> 由于使用的是anaconda下的虚拟环境，为避免出错，使用的是虚拟环境下的PyQt5及工具的软件包，相关设置如下：
>
> - 环境变量：
>
> <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814161139826.png" alt="image-20220814161139826" style="zoom: 67%;" />
>
> <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814161056277.png" alt="image-20220814161056277" style="zoom:67%;" />
>
> 
>
> - 外部工具：
>   - designer:
>
>     <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814163543991.png" alt="image-20220814163543991" style="zoom: 67%;" />
>     
>   - PyUIC:
>
> <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814163927669.png" alt="image-20220814163927669" style="zoom: 67%;" />
>
> ```
> # 实参：
> $FileName$
> -o
> $FileNameWithoutExtension$.py
> ```
>
>   - PyRcc:
>
> <img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814164305684.png" alt="image-20220814164305684" style="zoom:67%;" />
>
> ```
> #实参：
> $FileName$
> -o
> $FileNameWithoutExtension$_rc.py
> ```
>
> 



## 3. 安装、使用Pyinstaller

安装也是同上，有两种方法。此处参考[pycharm中安装并配置pyinstaller - CSDN](https://blog.csdn.net/qq_43703185/article/details/119342713)

“外部工具”设置：

<img src="https://mikepicture.oss-cn-chengdu.aliyuncs.com/picture/image-20220814164410901.png" alt="image-20220814164410901" style="zoom:67%;" />

```
#实参：
--noconsole
--onefile
$FileName$
```

> 注：运行pyinstaller后，生成的exe文件在**打包程序所在的文件夹的dist文件夹**中


# Python篇

## 1. 纯Python的安装

[廖雪峰的官方网站-安装Python](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014316090478912dab2a3a9e8f4ed49d28854b292f85bb000)

[菜鸟教程-Python3 环境搭建](http://www.runoob.com/python3/python3-install.html)



## 2. 教程推荐

[Python教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/1016959663602400)

[Python3 教程|菜鸟教程](https://www.runoob.com/python3/python3-tutorial.html)



