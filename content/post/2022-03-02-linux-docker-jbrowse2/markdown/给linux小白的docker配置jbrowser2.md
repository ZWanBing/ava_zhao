### 给linux小白的docker配置jbrowser2

> 前提条件：假设我们只能在一台没有root权限，并且装了docker的linux服务器上配置jbrowse2

##### 1.我比较熟悉centos系统，所以首先拉取一个docker centos镜像下来：

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/clipboard.png)

```shell
docker search centos #搜索镜像 
docker pull docker.io/centos #拉取镜像到本地
```

红框中第一个是官方镜像（不知道为啥拉取的人很少），把官方镜像拉取到本地

##### 2.根据jbrowse2官网的要求（https://jbrowse.org/jb2/docs/quickstart_web），需要先配置好nodejs和web server：

a.我们首先docker run启动一个容器

```shell
docker run -itd --name jbrowse2 -v /data2:/data2 -p 8080:80 docker.io/centos
```

该容器命名为jbrowse2，其他参数如 `-itd`、`-v` 、`-p`可参考Docker run命令详解https://www.runoob.com/docker/docker-run-command.html

然后进入容器内部，准备配置Pre-requisites

```shell
docker exec -it jbrowse2 bash
```

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/20201118133432.png)

b.安装nginx

```shell
yum install nginx 
ps -ef|grep nginx  #没有启动nginx时不会看到nginx的进程
```

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb2.png)

```shell
nginx 
ps -ef|grep nginx  #再次运行该命令看到nginx的进程
```

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb3.png)

> 注1：在docker中进入容器本身就是root用户，单独一个`nginx`命令就可以打开服务，因为可执行文件路径已经加载到环境变量中；但是如果找不到nginx命令，可以`cd /usr/sbin/ && ./nginx`，在centos中nginx可执行文件默认放在这里，cd进入此文件夹然后打开nginx服务
>
> 注2：有一些centos安装nginx的教程给的是`systemctl enable nginx`然后`systemctl start nginx`打开nginx服务，在docker中这是不行的，原因见下图

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb4.png)

在看到ngnix的进程后，可以在浏览器中查看nginx欢迎页面，输入地址：host-IP:port，其中host-IP就是你的服务器的内网或外网IP地址，port是容器映射的端口，本次配置中是将容器的80端口映射到宿主机的8080端口（见前文），例如我的10.0.1.4:8080打开后看到如下界面：

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb5.png)

> 我的是内网的IP，外网的权限（防火墙？）应该是关着的，我没有权限打开。大家根据自己的情况修改就行了，比如云服务器的应该能用外网IP打开这个测试页面
>
> Tips: `ifconfig -a`查看内网IP；`curl cip.cc`查看公网IP

c.安装nodejs

jbrowse2官网上要求安装**Node.js 10+**，第一次安装我装了v10.9.0，后续操作就报错了，所以大家装最新版就好，以免老版本缺胳膊少腿进行不下去

```shell
yum install wget #可能docker里面没有安装wget，需要先安装
wget https://nodejs.org/dist/v14.15.0/node-v14.15.0-linux-x64.tar.xz #这个是最新版 
tar xvf node-v14.15.0-linux-x64.tar.xz cd node-v14.15.0-linux-x64
ln -s /data2/test/wbzhao/software/node-v14.15.0-linux-x64/bin/node /usr/bin/ 
ln -s /data2/test/wbzhao/software/node-v14.15.0-linux-x64/bin/npm /usr/bin/ 
ln -s /data2/test/wbzhao/software/node-v14.15.0-linux-x64/bin/npx /usr/bin/
```

因为下载的是预编译版本，不需要源码编译，但是需要把可执行文件路径加入环境变量中，后面三个ln命令把可执行文件的软连接指向`/usr/bin/`。查看node版本，确认node已经安装好了

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb6.png)

##### 3.前期工作做好以后，就可以配置jbrowse2网页服务了：

按照jbrowse2官网的建议，应该先安装JBrowse CLI

```shell
npm install -g @jbrowse/cli
```

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb7.png)

这时候jbrowse cli工具并没有加到环境变量中，所以要多做一步

```shell
ln -s /data2/test/wbzhao/software/node-v14.15.0-linux-x64/bin/jbrowse /usr/bin/
```

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb8.png)

然后cd到nginx放置web文件的地址，利用jbrowse cli下载jbrowse2到该文件夹

```shell
cd /usr/share/nginx/html/ #进入nginx的资源目录 
rm -f  * #删除该目录内原始的文件，如之前的测试页 
jbrowse create jbrowse2 #下载jbrowse到该目录下 
cp -r jbrowse2/* ./  #将下载的jbrowse2文件夹下的内容拷贝到当前目录 
rm -rf jbrowse2/ #删除jbrowse2文件夹
```

当然我们也可以只在下载好的`jbrowse2`目录中进行后续操作，不去动默认的`html`文件夹下的其他内容，两者的区别是host-IP:port直接打开Jbrowse2网页服务，还是用host-IP:port/jbrowse2打开

> 作为linux小白我理解这个细节理解半天，导致之前配置的时候找不到jbrowse2的网页，这里给不理解的大家提个醒，html文件夹下的index.html以及其次级目录中的index.html都可以在网页中查看，只要给到完整的路径即可

在我当前的情况下，直接刷新之前在浏览器中打开的host-IP:port（10.0.1.4:8080）就能看到jbrowse2了

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb9.png)

由于还没有配置参考基因组和比对文件，所以网页是这样的，点击Volvox sample data会看到如下界面

![img](https://gitee.com/Ava_Zhao/gallery/raw/master/jb10.png)

**目前为止，我们的jbrowse2就可以正常工作了，后续添加配置自己的数据的工作可以参考jbrowse2官网的详细教程**[**https://jbrowse.org/jb2/docs/**](https://jbrowse.org/jb2/docs/)**，祝大家玩的开心~**