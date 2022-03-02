## 非root用户centos配置jupyter lab、IRkernel及依赖包问题

1. 安装conda
2. 安装jupyter lab
3. 安装R
4. 安装IRkernel
5. 字体不显示，无法找到Cairo依赖

-----------------------------------

### 1. 安装conda

> 没有root权限和sudo权限的普通用户何其痛苦，`yum install`那么丝滑的方式根本用不了，每次都要下tar.gz之类的安装包一步步`make&&make install` ，还是相当难受的，尤其是没有一个完整的教程介绍怎么把整个工作环境配好，只能自己慢慢摸索。

在网页上https://www.anaconda.com/products/individual下载最新版的linux安装脚本（[64-Bit (x86) Installer (529 MB)](https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh)），然后放到服务器（或者直接wget下载 `wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh`，都一样）,然后`bash Anaconda3-2020.11-Linux-x86_64.sh`即可安装成功，如果遇到问题就google，一般这样就安装成功了。

### 2. 安装jupyter lab

jupyter lab是jupyter notebook的升级版，不仅有notebook的功能，还能打开各种文本文件，打开txt，csv，pdf，html，图片等等各种文件（office的不行，如word，ppt，excel），使用起来更加方便。

![image-20210510131628705](C:\Users\admin\Desktop\image-20210510131628705.png)

显示为表格形式的csv

![image-20210422160950388](C:\Users\admin\Desktop\image-20210422160950388.png)

juputer lab可以新建或打开的窗口及文件类型

jupyter lab安装非常简单，一行命令即可`conda install -c conda-forge jupyterlab`。

### 3.安装R

在conda提供的基础环境`base`里直接安装R 4.0.4比较困难，我修改了channel也没能成功，不知道是不是因为本身环境里已经有一个R了。有一个曲线救国的方法可以成功安装最新的R：

①增加镜像

```shell
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
conda config --set show_channel_urls yes
conda config --show  # 查看新增channels
```

②新建一个conda环境安装新版R

```
conda create --name r4-base 
conda activate r4-base 
conda install -c conda-forge r-base 
conda install -c conda-forge/label/gcc7 r-base
```

上面这个代码如果安装不了就指定清华镜像或者其他镜像。

### 4.安装IRkernel

进入R环境

```R
install.packages(c('repr', 'IRdisplay', 'IRkernel'), type = 'source')
IRkernel::installspec()
```

或参考这个网站https://irkernel.github.io/installation/#linux-panel

退出R环境，在bash terminal输入

```shell
jupyter lab
```

等待服务启动完毕后，jupyter lab就可以在浏览器中使用了，如果要放在后台，就用`nohup`挂起。

__________



以上，一个支持 python/R kernel的jupyter lab就搭建好了，在浏览器中输入你内网的服务器地址hostIP:8888，如`10.0.0.1:8888`（jupyter lab默认端口是8888，如果同时开了jupyter notebook，可能变成8889），就会弹出jupyter lab的界面了。

### 5.字体不显示，无法找到Cairo依赖

![image-20210510132601540](C:\Users\admin\Desktop\image-20210510132601540.png)

遇到这个bug我尝试了很久，误入歧途。经人提醒，报错的信息可能和我实际缺少的依赖无关，最后通过以下方法解决：

```shell
conda install -c anaconda fonts-anaconda
conda install -c r r-cairo
```

在R4.0.4环境下重新装了字体依赖，然后安装了R Cairo包（实际上我是报错后先安装好了Cairo但还是没字体，但如果报错信息是没有Cairo依赖，上面的代码应该可以解决全部的问题）。



#### 以上就是本篇全部内容了，如有错误敬请指正。

