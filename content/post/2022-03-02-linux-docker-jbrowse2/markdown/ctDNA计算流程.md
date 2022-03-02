## ctDNA计算流程

>循环肿瘤DNA（ctDNA）是血液中肿瘤衍生的片段化DNA，是一种具有特征性的肿瘤标志物。通过ctDNA的相关检测，可以检测到肿瘤在患者血液中的踪迹信息，同时可以提供患者体内肿瘤的全景数据。ctDNA作为一项非侵入性的检测方法在肿瘤的筛查、预后、治疗等各个方面都具有重要的意义。

存在一些客户缩小gene list筛选突变的情况，这种情况下需要重新计算ctDNA fraction。

1. 重新注释，通过一个**示例json文件**和一个制作好的**file.list**可以完成自动注释任务投递（作者XCW）

```bash
python /mnt/vol2_ws/test/xcw/scripts/run_json_batch.py /mnt/vol2/rendong/test/xcw_test/results/mutect2_anno/file.list /mnt/vol2/rendong/test/xcw_test/results/mutect2_anno/json/test_anno.json
```

json文件内容如下：

```json
{
    "InputDataSet": {
        "WorkflowInput": {
            "pair_or_single.anno_type": "cf",
            "pair_or_single.outdir": "vol1@xtao:test/wbzhao/test/anno_0528/1926221",
            "pair_or_single.panel":"66",
            "pair_or_single.vcf":"vol1_root@xtao:rendong/project/66gene/1926221/3.somatic_VC/mutect.vcf",
            "pair_or_single.genelist":"vol1@xtao:rendong/project_info/bed_file/50-panel/50gene.list"
        }
    },
    "Name": "MUTECT2_ANNO_test_anno",
    "Pipeline": "MUTECT2_ANNO",
    "Priority": 8
}

```

**cf**指样本类型为**cfDNA**（组织算不了ctDNA fraction），指定**输出路径**、测序以及初次分析**真实的panel**——pair_or_single.panel，样本的**mutect.vcf的路径**，以及客户**指定的gene list**的位置。

file.list应为如下格式：

![image-20210618170659019](C:\Users\admin\Desktop\image-20210618170659019.png)

2. 通过注释流程产生的**ctdna_pre.xls**计算 ctDNA fraction

```bash
python /mnt/vol1/rendong/project_info/pipeLine/scripts/docker_contain/wdl_python/BioBin/ct_dna.py -i /mnt/vol2_ws/test/wbzhao/test/anno_0528/1926221/3.somatic_VC/ctdna_pre.xls -c /mnt/vol1_root/rendong/project/66gene/1926221/5.somatic_CNV/1926221.called.seg -p 50 -st cf -o /mnt/vol2_ws/test/wbzhao/test/anno_0528/1926221/ctdna.xls
```

* -i 输入文件

* -c segment文件

* -p 筛选后的gene list
* -st sample type
* -o 输出文件

