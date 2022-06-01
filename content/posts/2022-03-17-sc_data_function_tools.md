---
title: 单细胞数据通用分析
author: Ava zhao
date: '2022-03-17'
categories:
- 单细胞
---

>本篇更新较短，详细内容请参见所介绍工具包的官方地址：
>
>seurat：https://satijalab.org/seurat/index.html
>
>scater：https://bioconductor.org/packages/release/bioc/html/scater.html
>
>scanpy：https://scanpy.readthedocs.io/en/stable/tutorials.html

## 单细胞数据分析常用软件包

- R
  - seurat
  - scater
  - scran
  - scuttle
  - iSEE
- python
  - scanpy

## 单细胞数据分析常见数据类型

- 10X mtx：一个文件夹中包含如下三个文件

  ![image](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image.png)

- 10X h5：10x-Genomics-formatted hdf5 file

- SingleCellExperiment：数据为一个R对象，可保存为rds文件

- loom：一种HDF5文件，一般用来存储很大的单细胞数据集

- h5ad：formatted hdf5 file

- mtx：.mtx file

- h5：hdf5 file

- visum：10x-Genomics-formatted visum dataset 该数据类型包含空间信息

- csv、xlsx、text等等

## 单细胞数据常见分析

- QC质控
- 数据校正
- 数据合并
- 数据降维
- 可视化
- 细胞聚类
- 标识细胞类型
- 差异分析
- marker筛选
- 轨迹推断
- 空间单细胞数据分析
- 细胞周期拟合
- 单细胞多组学数据分析

## seurat功能导图

![img](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220317204251678.png)

https://gitmind.cn/app/doc/8226615223 持续更新中

