### 1.数据集介绍

​	在火星探测任务中，需要构建火星场景下的系列数据集用于相关感知算法的训练以及验证。2021年，围绕语义分割任务中，美国宇航局火星科学实验室发布了第一个名为AI4Mars的大规模火星地形数据集，其中包含四种类型的地形。但由于其中的地形类别定义匮乏，标注精度过低，使得数据集不具有实际的应用价值。为此，本团队针对语义分割任务，发布了一组命名为Mars_seg的系列数据集。

​	Mars- seg数据集包含丰富的火星场景的高分辨率图像，这有助于研究人员了解真正的火星景观。该数据集的所有单通道灰度图像均来自行星数据系统(PDS)，覆盖了机遇号和勇气号火星漫游者(MER)的导航摄像机(NAVCAM)和全景摄像机(PANCAM)拍摄的1064张高清图像；所有的RGB图像是由火星32k收集的，全部来自好奇号漫游者(MSL)的桅杆照相机(MastCam)，总共4148幅图像。其中，MER-Seg中的灰度图像的空间分辨率是1024 × 1024，而MSL-Seg中的彩色图像通过双线性插值被降采样到560 × 500。

​	在本数据集中，通过分析探测车在探测过程中遇到的困难和执行任务过程中可能遇到的高风险问题，我们将数据集中的地形划分为以下9个类别：

| 类别名称                 | 类别定义                                                     | 图例                                                         |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 火星土壤（Martian Soil） | 未固结或固结较差的风化物质;粒度更小，1mm以下，流动性相对较小;受地形的影响不会形成脊，颜色偏红; | <img src=".\pic\exm1.png" alt="image-20220507173101076" style="zoom:50%;" /> |
| 沙地<br />（Sands）      | 颗粒物质,很细小的岩石,直径1至2毫米;岩石经风化、剥蚀而形成;有迎风坡、背风坡,中间有一个脊,流动性相对较强，暗色为主; | <img src=".\pic\image-20220507173119751.png" alt="image-20220507173119751" style="zoom:50%;" /> |
| 沙砾<br />（Gravel）     | 比岩石颗粒要小，但比沙地颗粒粗糙，岩石经风化、剥蚀而形成，颜色偏灰色。 | <img src=".\pic\image-20220507173131095.png" alt="image-20220507173131095" style="zoom:50%;" /> |
| 基岩<br />（Bedrock）    | 陆壳表层风化层下面完整的新矿物岩石。比石头平整,颜色偏灰白色。多被土层覆盖，埋藏深度个一o | <img src=".\pic\image-20220507173200263.png" alt="image-20220507173200263" style="zoom:50%;" /> |
| 岩石<br />（Rocks）      | 由大岩体遇外力脱落下来的小型岩体，外表较为粗糙,质地坚硬，形状不规则，较为突兀，颜色偏青色。 | <img src=".\pic\image-20220507173213432.png" alt="image-20220507173213432" style="zoom:50%;" /> |
| 行车轨迹（Tracks）       | 探测车行进后留下的轨迹                                       | <img src=".\pic\image-20220507173226008.png" alt="image-20220507173226008" style="zoom:50%;" /> |
| 阴影（Shadows）          | 探测车、岩石等在光照下投射的影子                             | <img src=".\pic\image-20220507173246046.png" alt="image-20220507173246046" style="zoom:50%;" /> |
| 背景（Background）       | 远处的山和天空等类别                                         | <img src=".\pic\image-20220507173257502.png" alt="image-20220507173257502" style="zoom:50%;" /> |
| 未知（Unknown）          | 除以上类别的未知区域，例如火星车自身的影像                   | <img src=".\pic\image-20220507173311377.png" alt="image-20220507173311377" style="zoom:50%;" /> |



### **2.文件组成**及使用方法

#### 2.1文件组成

Mars_Seg

├─MER
│  ├─JPEGImages	原始图像（.jpg）
│  └─SegmentationClassPNG	语义分割标签（.png）
└─MSL
    ├─JPEGImages	原始图像（.jpg）
    └─SegmentationClassPNG	语义分割标签（.png）

​	本数据集按照图像格式以及数据来源划分为了两组，其中MER数据集中均为1024 ×1024的灰度图像，MSL数据集中均为560×500的RGB图像。

#### 2.2使用方法

在有监督方法中，可以使用单独的MER或者MSL数据集完成训练、验证和测试；在无监督方法中，可以使用其中的任意一组作为源域数据集，另一组作为目标域数据集进行域适应训练。

#### 3.2数据类别统计

<img src=".\pic\counter.png" alt="image-20220507173246046" style="zoom:50%;" />

我们统计了数据集中包含各个类别的图像数量。



### 论文引用

如果您在您的研究中用到了我们的数据集，请记得引用我们的论文。

[A Stepwise Domain Adaptive Segmentation Network With Covariate Shift Alleviation for Remote Sensing Imagery](https://ieeexplore.ieee.org/document/9716091 ) ( Volume: 60)

J. Li, S. Zi, R. Song, Y. Li, Y. Hu and Q. Du

Published in [IEEE Transactions on Geoscience and Remote Sensing](https://ieeexplore.ieee.org/xpl/RecentIssue.jsp?punumber=36) ( Volume: 60)

#### 论文亮点

​	我们提出了一种基于协变量域偏移的逐步域自适应分割网络。具体来说，为了缓解不同传感器采集数据时产生的协变量域偏移，我们设计了一个色彩空间映射统一模块。另外，使用了一个多统计量联合评估模块来捕捉子场景的不同统计特征，用于筛选目标域中高置信度的数据，并通过二次域适应进一步提高分割性能。

```
@ARTICLE{9716091,
  author={Li, Jiaojiao and Zi, Shunyao and Song, Rui and Li, Yunsong and Hu, Yinlin and Du, Qian},
  journal={IEEE Transactions on Geoscience and Remote Sensing}, 
  title={A Stepwise Domain Adaptive Segmentation Network With Covariate Shift Alleviation for Remote Sensing Imagery}, 
  year={2022},
  volume={60},
  number={},
  pages={1-15},
  doi={10.1109/TGRS.2022.3152587}}
```

#### 数据集链接 https://drive.google.com/drive/folders/1nOe2kNdI11MCohKwVuNoMcl8T7xoPAsS?usp=sharing

#### 构建数据集成员

博士生：席博博、武超雄

硕士生：刘佳超、张欢庆、訾顺遥、马寅乐、杜松乘、田鹏昊、刁妍、刘玉哲、陈轩

本科生：张致源、冷奕泓
