# Jbrowse2基因组浏览器使用指南（一）

> 原文地址：https://jbrowse.org/jb2/docs/user_guide

之前已经推送了jbrowse2的安装配置，本文将详细介绍JBrowse2的使用，如果自己的服务器尚未配置安装JBrowse2，可以用JBrowse2官网给的demo。

[TOC]

---

## 用户界面概览

在浏览器中打开自己配置好的jbrowse网页后，会看到下面这样的界面（或者查看官方的demo:https://s3.amazonaws.com/jbrowse.org/code/jb2/master/index.html)，我们常用的就是比对结果的线性视图，所以点击中间的<span style="color:#71BA51;">Linear Genome View</span>打开一个新工作窗口。

![image-20201119113208382](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119113208.png)

### 线性基因组视图

在LGV（Linear Genome View）视图中可以像IGV中一样，在搜索框中输入位置，回车即可定位到想要查看的位置，如：`chr1:1-100 `或 `chr1:1..100`，但是目前还不支持按照基因名称搜索。

1. 左右拖拽

   类似于IGV，在jbrowse中可以鼠标左键按住后拖拽视图，查看周围的序列和reads。

2. 缩放

   如图中红框，在LGV顶部有缩放按钮和滑条：

   ![image-20201119163013784](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119163013.png)

   除此之外，也可以使用`Ctrl`+`鼠标滚轮`的方式放大缩小视图。

3. 窗口重排

   在每一个track窗口的左上角有一个圆角矩形标签：

   ![image-20201119163346247](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119163346.png)

   点击左侧的六个小点既可以拖拽重排track。

## 添加track

jbrowse目前不支持直接在浏览器中打开本地文件，只能通过服务器后台命令行配置、admin server和URL的方式添加新的track，通过URL添加的方式如下：

页面左上角菜单栏中，点击File->Open Track

![image-20201119164348308](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119164348.png)

页面右侧出现添加track表单，另外，通过select tracks按钮也可以打开这个界面，select tracks->+

![image-20201119164656980](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119164716.png)                      ![image-20201119164835841](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119164835.png)

通过添加指向文件的URL，既可以加载到目前的jbrowse窗口中，目前支持的文件类型有：

- Tabixed VCF
- Tabixed BED
- Tabixed GFF
- BAM
- CRAM
- BigWig
- BigBed
- .hic file (Juicebox)

对于tabix文件，允许使用TBI或CSI索引。BAM允许使用CSI或BAI。CRAM仅允许CRAI。对于BAI或TBI索引文件，会推测它的文件名为filename+'.bai'，但是如果与此不同，请确保明确指定索引文件。

### 分享工作窗口

在jbrowse页面顶部中央，可以更改当前工作窗口的名字，也可以生成一个分享链接：

![image-20201119172106579](https://gitee.com/Ava_Zhao/gallery/raw/master/20201119172106.png)

分享该链接可以打开<span style='color:'>完全一样</span>的窗口内容。但最好不要直接从地址栏复制粘贴分享页面，请不要这么做。

### 编辑track配置

太简单了不打算翻译了请查看英文文档！

## 比对track参数设置

### 堆积视图

太简单了不打算翻译了请查看英文文档！

### 覆盖度视图

太简单了不打算翻译了请查看英文文档！

### 显示soft clipping

太简单了不打算翻译了请查看英文文档！

### reads排序

太简单了不打算翻译了请查看英文文档！

### 显示中心线

太简单了不打算翻译了请查看英文文档！













