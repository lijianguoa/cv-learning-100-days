# Day 1: 计算机视觉概述与发展历程

> 📅 2026-05-26 | 🎯 100天计算机视觉学习计划 | Day 1/100

---

## 📸 配图

![计算机视觉发展历程](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day001/cv_day001_cover.jpg)

![CV应用领域全景](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day001/cv_day001_applications.jpg)

---

## 📜 历史背景

计算机视觉（Computer Vision, CV）的历史可以追溯到20世纪60年代，是人类赋予机器"看"的能力的伟大探索。[^1]

[^1]: [Wikipedia: Computer Vision - 计算机视觉的完整历史](https://en.wikipedia.org/wiki/Computer_vision)

### 萌芽期（1960s-1970s）

- **1966年**：MIT的Seymour Papert启动了"Summer Vision Project"[^2]，试图让计算机"看懂"暑假照片，这个雄心勃勃的项目虽然远未完成，却开启了CV研究的序幕。

[^2]: [MIT: The Summer Vision Project 原始提案](http://6.869.csail.mit.edu/sp21/lectures/1_intro.pdf) - 1966年MIT AI Lab的夏季视觉项目

- **1963年**：Larry Roberts的博士论文《Machine Perception of Three-Dimensional Solids》开创了从2D图像恢复3D结构的研究方向。

- **1970s**：David Marr提出了视觉计算理论框架[^3]，将视觉过程分为"草图"、"2.5D图"和"3D模型"三个层次，奠定了计算视觉的理论基础。

[^3]: [Wikipedia: David Marr - 视觉计算理论之父](https://en.wikipedia.org/wiki/David_Marr_(neuroscientist))

> 📎 **Marr的三层理论**：[计算理论、算法、实现三层分析框架](https://m.baike.com/wiki/D.Marr%E8%AE%A1%E7%AE%97%E8%A7%86%E8%A7%89%E7%90%86%E8%AE%BA/19863655)

### 神经科学基础：Hubel & Wiesel的发现

1959年，David Hubel和Torsten Wiesel在研究猫的视觉皮层时发现，某些神经元对特定方向的边缘线条有强烈反应。[^4] 这一发现揭示了视觉信息在神经系统中的分层处理机制，为后来的卷积神经网络提供了生物学灵感。

[^4]: [Nobel Prize: Hubel & Wiesel 1981年诺贝尔奖](https://www.nobelprize.org/prizes/medicine/1981/press-release/) - 视觉系统信息处理的发现

> 📎 **简单细胞与复杂细胞**：[Hubel & Wiesel发现的视觉皮层功能结构](https://www.kepuchina.cn/zmt/mt/sxs/201701/t20170113_62928.shtml)

### 发展期（1980s-1990s）

- **1980s**：几何计算机视觉蓬勃发展，立体视觉、运动恢复结构（SfM）成为研究热点。
- **1989年**：卷积神经网络（LeNet）雏形由Yann LeCun提出，但受限于算力和数据，未引起广泛关注。
- **1990s**：基于特征的方法兴起，SIFT（1999）、HOG等手工特征成为主流。

### 深度学习革命（2012-至今）

- **2012年**：AlexNet在ImageNet竞赛中以巨大优势夺冠[^5]，深度学习时代正式开启。

[^5]: [AlexNet: 2012年深度学习里程碑论文](https://lzwjava.github.io/alexnet-2012-landmark-en) - ImageNet Classification with Deep Convolutional Neural Networks

- **2015年**：ResNet提出残差连接，网络深度突破百层。
- **2020s**：Vision Transformer、扩散模型、多模态大模型等新技术不断涌现，CV进入Foundation Model时代。

> 📎 **计算机视觉六十年**：[从像素到语义的完整发展历程](https://blog.csdn.net/matlab_python22/article/details/153120608)

---

## 🧠 核心概念

### 1. 什么是计算机视觉？

计算机视觉是一门研究如何使机器"看"并"理解"图像和视频的学科。[^6] 它涉及图像获取、处理、分析和理解等多个层面，目标是让计算机能够从数字图像或视频中提取有意义的信息，并据此做出决策。

[^6]: [Wikipedia: Computer Vision - 定义与研究范畴](https://en.wikipedia.org/wiki/Computer_vision)

### 2. CV的研究范畴

| 层次 | 任务 | 描述 |
|------|------|------|
| **低层视觉** | 图像预处理 | 去噪、增强、边缘检测 |
| **中层视觉** | 特征提取 | 特征点检测、描述子生成、图像分割 |
| **高层视觉** | 场景理解 | 目标识别、场景分类、语义理解 |

### 3. 经典CV任务分类

```
计算机视觉任务
├── 图像分类（Image Classification）
│   └── 判断图像中包含什么类别
├── 目标检测（Object Detection）
│   └── 定位并识别图像中的多个目标
├── 图像分割（Image Segmentation）
│   ├── 语义分割（Semantic Segmentation）
│   ├── 实例分割（Instance Segmentation）
│   └── 全景分割（Panoptic Segmentation）
├── 图像生成（Image Generation）
│   ├── 超分辨率（Super Resolution）
│   ├── 风格迁移（Style Transfer）
│   └── 图像修复（Inpainting）
└── 视频理解（Video Understanding）
    ├── 目标跟踪（Object Tracking）
    ├── 动作识别（Action Recognition）
    └── 视频生成（Video Generation）
```

> 📎 **CV任务详解**：[Stanford CS231n: 计算机视觉任务分类](https://cs231n.stanford.edu/)

### 4. 关键术语

- **像素（Pixel）**[^7]：数字图像的最小单位

[^7]: [Wikipedia: Pixel - 像素的定义与历史](https://en.wikipedia.org/wiki/Pixel)

- **分辨率（Resolution）**：图像包含的像素数量
- **特征（Feature）**：图像中具有区分性的信息
- **卷积（Convolution）**[^8]：通过滑动窗口提取局部特征的操作

[^8]: [Wikipedia: Convolution - 卷积的数学定义](https://en.wikipedia.org/wiki/Convolution)

- **感受野（Receptive Field）**[^9]：神经元能"看到"的输入区域大小

[^9]: [Wikipedia: Receptive Field - 感受野的神经科学概念](https://en.wikipedia.org/wiki/Receptive_field)

- **Ground Truth**：人工标注的标准答案，用于评估模型性能

### 5. CV技术栈

```
应用层：自动驾驶 | 医学影像 | 安防监控 | 工业检测 | AR/VR
   ↑
模型层：分类模型 | 检测模型 | 分割模型 | 生成模型
   ↑
框架层：PyTorch | TensorFlow | OpenCV | MMDetection
   ↑
基础层：数学基础 | 机器学习 | 深度学习 | 编程能力
```

> 📎 **OpenCV入门**：[OpenCV官方文档与教程](https://docs.opencv.org/)

---

## 👨‍🔬 科学家故事

### David Marr（1945-1980）：视觉计算理论之父

David Marr是英国神经科学家和心理学家，被誉为"计算视觉之父"。他在MIT工作期间提出了著名的**Marr视觉计算理论**[^10]，将视觉信息处理分为三个层次：

[^10]: [David Marr传记 - 国际社会科学百科全书](https://shimon-edelman.github.io/marr/marr.html)

1. **计算理论层**：视觉系统的目标是什么？
2. **表示与算法层**：如何实现这个目标？
3. **硬件实现层**：在物理上如何构建？

遗憾的是，Marr在35岁时因白血病英年早逝，但他的理论框架至今仍是理解人类视觉和机器视觉的基石。他的经典著作《Vision》在他去世后出版，成为CV领域必读的经典文献。[^11]

[^11]: [Marr的计算理论哲学](https://pmc.ncbi.nlm.nih.gov/articles/PMC3816718/) - Does this computational theory solve the right problem?

> *"Vision is not a passive process of receiving images, but an active process of constructing descriptions."*
> — David Marr

### Yann LeCun：卷积神经网络的坚守者

Yann LeCun在1989年就提出了卷积神经网络的基本架构，并在1998年开发了LeNet-5用于手写数字识别。然而在随后的十多年里，深度学习被学术界冷落，LeCun却始终坚信CNN的力量。2012年AlexNet的成功证明了他的远见。2018年，LeCun与Geoffrey Hinton、Yoshua Bengio共同获得图灵奖，深度学习三巨头实至名归。

---

## 📚 重要文献

1. **Marr, D. (1982).** *Vision: A Computational Investigation*. MIT Press.
   - 视觉计算理论的奠基之作，提出三层分析框架

2. **Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012).** *ImageNet Classification with Deep Convolutional Neural Networks*. NeurIPS.
   - AlexNet论文，深度学习革命的起点[^12]

[^12]: [AlexNet论文深度解析](https://blog.csdn.net/2502_90212264/article/details/154098017) - CNN复兴的里程碑

3. **LeCun, Y., Bottou, L., Bengio, Y., & Haffner, P. (1998).** *Gradient-based learning applied to document recognition*. Proceedings of the IEEE.
   - LeNet-5论文，CNN的经典之作

4. **Dosovitskiy, A., et al. (2021).** *An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale*. ICLR.
   - ViT论文，将Transformer引入视觉领域

5. **Radford, A., et al. (2021).** *Learning Transferable Visual Models From Natural Language Supervision*. ICML.
   - CLIP论文，多模态学习的里程碑

---

## 🔬 经典实验

### ImageNet大规模视觉识别挑战赛（ILSVRC）

**背景**：2010年，斯坦福大学教授李飞飞团队发布了ImageNet数据集[^13]，包含超过1400万张标注图像、2万多个类别。基于此数据集举办的ILSVRC竞赛成为CV领域的"奥运会"。

[^13]: [ImageNet数据集官网](https://www.image-net.org/) - 大规模视觉识别挑战赛

**关键转折——2012年**：
- Alex Krizhevsky设计的AlexNet在ImageNet 2012竞赛中，Top-5错误率从上一年的25.8%骤降至**15.3%**
- 这是深度学习首次在CV大规模竞赛中取得压倒性胜利
- AlexNet使用了ReLU激活函数、Dropout正则化、GPU并行训练等关键技术
- 此后，所有参赛队伍都转向了深度学习方法

**后续发展**：
| 年份 | 获胜模型 | Top-5错误率 | 关键创新 |
|------|----------|-------------|----------|
| 2012 | AlexNet | 15.3% | 深度CNN + GPU训练 |
| 2013 | ZFNet | 11.2% | 可视化CNN特征 |
| 2014 | VGGNet | 7.3% | 小卷积核深层网络 |
| 2014 | GoogLeNet | 6.7% | Inception模块 |
| 2015 | ResNet | 3.6% | 残差连接 |
| 2016 | Inception-v3 | 3.5% | 因子分解卷积 |

到2017年，ResNet的改进版本已经将错误率降至2.3%，**超越了人类的5.1%错误率**。

> 📎 **ImageNet历史**：[从2012到2017的竞赛演进](https://www.turingpost.com/p/cvhistory2) - The Dawn of Computer Vision

---

## 📖 小故事

### "让计算机看懂暑假照片"的伟大失败

1966年夏天，MIT人工智能实验室的Seymour Papert给一群本科生分配了一个暑期项目：连接一台摄像机到计算机，让它"描述"暑假期间拍摄的照片。Papert乐观地认为这只需要一个夏天就能完成。

然而，这个看似简单的任务实际上极其复杂——要让计算机理解一张照片，需要解决光照变化、遮挡、视角变化、物体变形等无数问题。这个"失败"的暑期项目深刻揭示了视觉问题的本质困难，也正式拉开了计算机视觉研究的序幕。

50多年后的今天，借助深度学习，我们确实能让计算机"看懂"照片了——但这条路走了整整半个多世纪。

### ImageNet的诞生：一个博士生的执念

2007年，斯坦福大学博士生李飞飞意识到，CV领域最大的瓶颈不是算法，而是**数据**。当时主流数据集只有几万张图像，她决定构建一个包含千万级图像的数据集。

这个想法在当时被很多人认为不切实际。李飞飞几乎找不到经费支持，甚至被同行嘲笑。但她坚持了下来，通过Amazon Mechanical Turk众包平台，动员了来自167个国家的近5万名标注者，历时两年完成了ImageNet的构建。

事实证明，ImageNet彻底改变了CV的研究范式——没有大数据，就没有深度学习的成功。

---

## 💡 思考题

1. **基础题**：计算机视觉的三大经典任务（分类、检测、分割）之间有什么区别和联系？

2. **进阶题**：为什么2012年AlexNet的成功被认为是深度学习的转折点？除了算法本身，还有哪些因素促成了这次突破？
   > 💡 **提示**：参考[GPU并行计算与大数据的完美结合](https://lzwjava.github.io/alexnet-2012-landmark-en)

3. **思考题**：David Marr的视觉计算三层框架在今天是否仍然适用？深度学习的"端到端"学习范式是否挑战了Marr的理论？
   > 💡 **提示**：阅读[Marr计算理论的现代反思](https://pmc.ncbi.nlm.nih.gov/articles/PMC3816718/)

4. **开放题**：你认为计算机视觉下一个重大突破会是什么方向？为什么？

---

## 📖 术语表

| 术语 | 英文 | 简要解释 |
|------|------|----------|
| 计算机视觉 | Computer Vision (CV) | [让计算机理解和处理视觉信息的学科](https://en.wikipedia.org/wiki/Computer_vision) |
| 图像分类 | Image Classification | 判断图像属于哪个类别 |
| 目标检测 | Object Detection | 定位并识别图像中的目标 |
| 语义分割 | Semantic Segmentation | 对每个像素进行类别标注 |
| 实例分割 | Instance Segmentation | 区分不同实例的像素级分割 |
| 卷积神经网络 | Convolutional Neural Network (CNN) | [利用卷积运算提取空间特征的神经网络](https://en.wikipedia.org/wiki/Convolutional_neural_network) |
| 感受野 | Receptive Field | [神经元对应的输入区域大小](https://en.wikipedia.org/wiki/Receptive_field) |
| 深度学习 | Deep Learning | [基于多层神经网络的机器学习方法](https://en.wikipedia.org/wiki/Deep_learning) |
| 迁移学习 | Transfer Learning | 将一个任务学到的知识迁移到另一个任务 |
| 数据增强 | Data Augmentation | 通过变换扩充训练数据的技术 |
| Ground Truth | Ground Truth | 人工标注的标准答案 |
| mAP | mean Average Precision | 目标检测的平均精度均值 |
| IoU | Intersection over Union | 交并比，衡量预测框与真实框的重合度 |
| 预训练模型 | Pre-trained Model | 在大规模数据集上训练好的模型 |
| 基础模型 | Foundation Model | 在大规模数据上预训练的通用大模型 |
| 视觉计算理论 | Marr's Theory | [David Marr提出的三层视觉分析框架](https://en.wikipedia.org/wiki/David_Marr_(neuroscientist)) |

---

## 🔮 下节预告

**Day 2：数字图像基础**

明天我们将深入数字图像的底层表示，学习像素、分辨率、色彩空间（RGB、HSV、灰度）等基础概念，了解图像的数字化表示与各种存储格式（JPEG、PNG、BMP、TIFF）的特点与适用场景。这些知识是后续所有图像处理操作的基石。

> 💡 *工欲善其事，必先利其器。理解图像的本质，是掌握计算机视觉的第一步。*
