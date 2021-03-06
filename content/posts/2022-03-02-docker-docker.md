---
title: docker=游戏存档？关于docker的一个日常化类比
author: Ava Zhao
date: '2022-03-02'
categories:
- 胡言乱语
---
![img](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20210709150747197.png)



> 首先要听说过docker的一些基本概念：
>
> 1. 镜像 docker image
>
> 2. 容器 docker container
>
> 3. 镜像文件 dockerfile
>
> 4. 仓库 Docker Hub
>
>    

**docker**应该是一个IT或者IT相关行业从业者不太陌生的名词，网络教程里大多把docker比喻成**集装箱与运输工具**，但在跟同事讨论问题的过程中，我们发现对于从小接触游戏的我们90后🐶来说，有一个更（不）好（妥）的类比——**游戏存档**。（如有雷同，纯属巧合）

![img](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20210709151609262.png)



小时候玩主机游戏，有的关卡很难，或者自己只打通一种结局而没有发现其他结局的时候，大家可能会在网上找其他玩家上传的存档文件，下载到自己电脑上，然后放到存档文件夹中，这样再打开游戏，就会发现多了一个存档可以读入。继而读取这个存档就拥有了大神玩家的进度、属性及装备等等。而且一个游戏可以同时有很多存档，每个存档侧重点可能不一样。当然，如果自己的存档很有意思，也可以把自己的存档放在论坛中供人下载。

![img](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20210709171039244.png)

在这里，本地的一个**镜像 ** **=** 一个游戏里的一个**存档**，游戏 **=** 主机/服务器环境，一个个存档 **=** 一个个隔离开的镜像。当存档在存档栏里时 **=** 一个镜像文件image，当存档被读入时就产生了一个容器，但是读档产生的进度 = 容器内的更改并不是发生在存档 **=** 镜像文件上的，**除非**我们覆盖了当时读入的那个存档 **=** commit修改镜像，例如上图中我们读入了潇隐村，然后做了一个任务，拿到了一把武器，但是存档时没有存在第一栏，则第一个存档仍然保留，如果覆盖了第一个存档，则第一个存档就再也无法读入了=镜像已经被修改。

当我们退出游戏但是没有保存进度到某个存档时 = 没有commit镜像，这个游戏进度=容器内产生的相对于镜像文件的更改就会灭失，除非我们只是暂停游戏/挂起游戏/放置后台 **=** 暂停容器/挂起容器/后台运行，当我们取消暂停进入游戏，就可以继续在当前进度玩 **=** restart容器/继续在容器内操作。

不同存档/游戏进度 = 镜像/容器，是相互独立的。假设我们在两个不同档开始的时候就选择了两个不同的角色，拥有不同的性别、门派，这就像镜像中配置的软件或者环境，都可以是不同的，根据玩家 = 制作者的制作过程及需求而变。玩家想要玩什么角色，可以自己一点点塑造 **=** 制作dockerfile/在最基础镜像读出的容器中安装配置，也可以在网上下载存档 **=** docker hub仓库下载镜像。docker仓库是专门用来存放docker镜像的地方，可以把它想象成大家把自己的游戏进度的存档po到这个地址供大家下载体验。而dockerfile相比于镜像文件更加特殊一些，它更像一个可以设置**自动游戏的托管机器人**，具体细节在这里不做更多描述，有兴趣的读者可以自己去搜索了解。

游戏存档与docker有许多相似之处，但也有很多各自的特点，例如容器的**文件挂载**（假设一个进度得到的武器可以保存在计算机中某个文件，另一个游戏进度也可以读文件使用武器），**端口映射**及**资源分配**（限制每个游戏存档读入后消耗的计算机资源）等，也不是完全可以类比的。如果大家有什么可以很好类比的例子，欢迎自己琢磨或者在后台留言。本篇到此结束，如有纰漏，欢迎指出~

