---
title: macromolecular docking 简明介绍
author: Ava Zhao
date: '2022-03-02'
categories:
- 科普
---

>背景：现代的药物开发模式为从疾病入手（如新冠特效药），应用疾病模型寻找可能的药物靶点，设计药物。
>
>问题：药物设计前期会产生大量的候选分子，不可能也不应该全部进入生物活性筛选（生命实验）。
>
>方案：对这些候选药物分子做计算虚拟筛选能够极大缩短后续实验时间及研发成本。
>
>结果：分子对接（属于虚拟筛选）在各类创新药百花齐放的当下，成为各大药厂研发大分子、小分子药物的前置必要步骤。

![Snipaste_2022-06-01_15-58-46](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/Snipaste_2022-06-01_15-58-46.jpg)

虚拟筛选


## 概念介绍

![image-20220302173921992](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220302173921992.png)

分子对接：是[分子模拟](https://zh.wikipedia.org/wiki/分子模擬)的重要方法之一，其本质是两个或多个分子之间的[识别](https://zh.wikipedia.org/wiki/分子识别)过程，其过程涉及分子之间的**空间匹配**和**能量匹配**，其目的是找到分子间的**最佳匹配模式及其结合强度**。

![Snipaste_2022-03-02_17-55-20](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/Snipaste_2022-03-02_17-55-20.png)

**注：但是实际上这个理论已经经过了更新，目前较被认可的是在钥匙-锁理论基础上，也存在诱导-契合现象：配体和受体在对接过程中会由于相互适应而产生构象的变化，因为分子是柔性的，其所包含的原子间键长键角可以改变。**

刚性对接：在计算过程中，参与对接的分子构象不发生变化，仅改变分子的空间位置与角度，刚性对接方法的简化程度最高，计算量相对较小，适合于处理大分子之间的对接。

-------------

半柔性对接：允许对接过程中小分子构象发生一定程度的变化，但通常会固定大分子的构象，另外小分子构象的调整也可能受到一定程度的限制，如固定某些非关键部位的键长、键角等，半柔性对接方法兼顾计算量与模型的预测能力，是应用比较广泛的对接方法之一。

------------------------

柔性对接：允许研究体系的构象发生自由变化，由于变量随着体系的原子数呈几何级数增长，因此柔性对接方法的计算量非常大，消耗计算机时很多，适合精确考察分子间识别情况。

----------------------------

除了以上概念外，由于分子对接实际上是**分子间相互作用力**的体现，故而还需要知道一些生物化学、 物理的基础概念。

范德华相互作用：在化学中指分子或原子之间非定向的、无饱和性的、较弱的相互作用力，范德华力是一种电性引力，但它比化学键或共价键弱得多。 范德华力的大小和分子的大小成正比。

静电相互作用：静电作用是化学键--离子键形成的本质，它包括静电引力和静电斥力。 由于静电引力没有方向性，阴阳离子之间的作用可在任何方向上，离子键没有方向性。

自由能：**热力学自由能**是指一个[热力学系统](https://zh.wikipedia.org/wiki/热力学系统)的能量中可以用来对外做[功](https://zh.wikipedia.org/wiki/功)的部分。自由能可以作为一个[热力学过程](https://zh.wikipedia.org/wiki/热力学过程)能否自发进行的判据。自由能的变化决定了两个分子是否能够结合以及结合的强度,一般认为自由能最小的构象存在的概率最高。

## 简明流程

![image-20220302231257807](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220302231257807.png)

通过以上步骤，大部分候选分子就被剔除了，形成一个大小合适进行后续生物活性筛选的分子库，节约大量时间与成本。

## 常用算法

空间匹配是分子间发生相互作用的基础，能量匹配是分子间保持稳定结合的基础。

![image-20220303193931648](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220303193931648.png)

### 空间构象搜索算法

#### 系统搜索算法

通过改变每个扭转角评估所有可能的结合构象，进而选取能量最低的。

#### 非系统搜索算法

- 分子动力学方法
- 随机搜索
  - 完全随机算法
  - 蒙特卡罗模拟
  - 模拟退火法
- 遗传算法
- 距离几何算法
- 片段生长法
- 格点计算

### 能量评估算法

- 经验/半经验自由能
- 分子力场
- 知识统计打分函数

![image-20220302232811279](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220302232811279.png)

目前分子对接领域已出现很多新的算法应用于构象搜索或能量评估，如[人工神经网络](https://zh.wikipedia.org/wiki/人工神经网络)等。构象搜索与能量评估的算法并不是独立于彼此的，可能同时估算并优化了这两方面的因素。

## 常用软件

- AutoDock：

  把拉马克遗传算法和局部搜索结合在一起，遗传算法用于全局搜索，而局部搜索用于能量优化。为了加快计算速度，采用格点计算。首先在受体活性氨基酸附近划定一个长方体区域作为搜索空间，扫描不同类型的原子计算格点能量，在搜索空间内，调整配体的构象、位置和方向，进而评分、排序获得能量最低的构象作为输出结果。

  ![Snipaste_2022-03-03_20-05-26](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/Snipaste_2022-03-03_20-05-26.png)

- Dock

- FlexX

- Rosetta@home：

  是一个基于[伯克利开放式网络计算平台](https://zh.wikipedia.org/wiki/伯克利开放式网络计算平台)（BOINC）的[分布式计算](https://zh.wikipedia.org/wiki/分布式计算)项目，用于[蛋白质结构预测](https://zh.wikipedia.org/wiki/蛋白质结构预测)、[蛋白质-蛋白质对接](https://zh.wikipedia.org/wiki/蛋白质-蛋白质对接)和新的[蛋白质设计](https://zh.wikipedia.org/w/index.php?title=蛋白质设计&action=edit&redlink=1)的研究。是[结构生物信息学](https://zh.wikipedia.org/wiki/生物信息学)中新方法的一个测试框架。如其中两个重要项目——[蛋白质结构预测技术的关键测试](https://zh.wikipedia.org/wiki/蛋白质结构预测技术的关键测试)（CASP）和[交互作用预测的关键测试](https://zh.wikipedia.org/w/index.php?title=交互作用预测的关键测试&action=edit&redlink=1)（CAPRI）。这两项测试实验分别用于评估蛋白质结构预测和蛋白质-蛋白质对接预测的最前沿技术。

- Schrödinger：

  一个集成的分子动力学计算平台，基于物理的计算平台利用对物理、化学和预测建模的深刻理解来加速创新。以更低的成本更快地发现高质量，新颖的分子。

## 应用案例

### 非典（SARS冠状病毒）药物开发

![image-20220302224552906](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220302224552906.png)

![image-20220302224627896](https://cdn.jsdelivr.net/gh/ZWanBing/blogImage@main/img/image-20220302224627896.png)

#### 参考链接

1.[分子对接简明教程 – BioEngX](http://www.bioengx.com/molecular-docking-tutorial/)

2.[Rosetta@home - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/Rosetta@home)

3.[Schrödinger](https://www.schrodinger.com/)

4.[分子对接与虚拟筛选 - 豆丁网 (docin.com)](https://www.docin.com/p-2095138737.html)

5.[分子对接 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/分子对接)
