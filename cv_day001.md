# Day 1: 计算机视觉概述与OpenCV基础

## 📚 学习目标

1. 理解计算机视觉的基本概念和应用领域
2. 掌握OpenCV的安装方法
3. 学会使用OpenCV进行图像的读取、显示和保存
4. 掌握图像的基本操作方法

---

## 🔰 一、什么是计算机视觉

### 1.1 定义

**计算机视觉（Computer Vision）** 是一门让计算机能够"看懂"图像和视频的科学。它旨在使机器能够自动理解图像和视频中的内容，如同人类视觉系统一样。

### 1.2 计算机视觉 vs 图像处理 vs 机器视觉

| 领域 | 目标 | 输入 | 输出 |
|------|------|------|------|
| 图像处理 | 改善图像质量 | 图像 | 图像 |
| 计算机视觉 | 理解图像内容 | 图像/视频 | 语义信息/知识 |
| 机器视觉 | 工业检测与控制 | 图像 | 控制信号 |

### 1.3 计算机视觉发展历程

```
1960s: 起步阶段 - 边缘检测、图像增强
1980s: 几何视觉 - 相机标定、三维重建
1990s: 特征工程 - SIFT、HOG特征
2010s: 深度学习 - CNN、RCNN、YOLO
2020s: 大模型时代 - Vision Transformer、CLIP
```

### 1.4 主要应用领域

| 应用领域 | 具体应用 | 技术要点 |
|----------|----------|----------|
| 人脸识别 | 刷脸支付、安防监控 | 人脸检测、特征匹配 |
| 自动驾驶 | 车道检测、障碍物识别 | 目标检测、语义分割 |
| 医学影像 | 病灶检测、影像分析 | 图像分类、分割 |
| 工业检测 | 缺陷检测、尺寸测量 | 图像处理、模式识别 |
| 增强现实 | 虚拟物体叠加 | 姿态估计、三维重建 |
| 图像搜索 | 以图搜图 | 特征提取、相似度匹配 |

---

## 🛠️ 二、OpenCV简介与安装

### 2.1 OpenCV概述

**OpenCV（Open Source Computer Vision Library）** 是一个开源的计算机视觉和机器学习软件库，包含2500+优化算法，涵盖从基础图像处理到高级深度学习的各个方面。

### 2.2 OpenCV版本

| 版本 | 发布时间 | 主要特性 |
|------|----------|----------|
| OpenCV 1.0 | 2006 | 基础功能 |
| OpenCV 2.x | 2009-2015 | C++接口、GPU加速 |
| OpenCV 3.x | 2015-2018 | 新API、深度学习模块 |
| OpenCV 4.x | 2018-至今 | DNN优化、C++11支持 |
| OpenCV 5.x | 2024-至今 | 更快的推理速度 |

### 2.3 安装OpenCV

#### Python安装（推荐）

```bash
# 基础版
pip install opencv-python

# 完整版（包含额外模块）
pip install opencv-contrib-python

# 查看版本
python -c "import cv2; print(cv2.__version__)"
```

#### Conda安装

```bash
conda install -c conda-forge opencv
```

#### Docker环境

```bash
docker pull python:3.9
pip install opencv-python
```

### 2.4 OpenCV模块结构

```
opencv
├── cv2.core          # 核心功能
├── cv2.imgproc       # 图像处理
├── cv2.imgcodecs     # 图像读写
├── cv2.videoio       # 视频读写
├── cv2.highgui       # GUI显示
├── cv2.stitching     # 图像拼接
├── cv2.ml            # 机器学习
├── cv2.dnn           # 深度学习
├── cv2.face          # 人脸识别
├── cv2.objdetect     # 目标检测
└── cv2.xfeatures2d   # 高级特征
```

---

## 📖 三、图像的读取、显示和保存

### 3.1 读取图像

```python
import cv2
import numpy as np

# 基本读取
img = cv2.imread('image.jpg')

# 读取并指定颜色模式
# -1: 保持原格式 (IMREAD_UNCHANGED)
# 0: 灰度图 (IMREAD_GRAYSCALE)
# 1: 彩色图 (IMREAD_COLOR)
img_gray = cv2.imread('image.jpg', 0)  # 灰度模式
img_color = cv2.imread('image.jpg', 1)  # 彩色模式

# 检查是否读取成功
if img is None:
    print("无法读取图像，请检查路径是否正确")
else:
    print(f"图像形状: {img.shape}")  # (高度, 宽度, 通道数)
```

### 3.2 显示图像

```python
import cv2

# 读取图像
img = cv2.imread('image.jpg')

# 创建窗口并显示
cv2.imshow('Display Window', img)

# 等待按键
cv2.waitKey(0)

# 关闭窗口
cv2.destroyAllWindows()
```

### 3.3 保存图像

```python
import cv2

# 读取图像
img = cv2.imread('image.jpg')

# 保存图像
success = cv2.imwrite('output.jpg', img)

# 保存为不同格式
cv2.imwrite('output.png', img)
cv2.imwrite('output.bmp', img)

# 带质量参数的保存(JPEG)
params = [cv2.IMWRITE_JPEG_QUALITY, 95]
cv2.imwrite('output_compressed.jpg', img, params)
```

---

## 🎯 四、图像基本操作

### 4.1 图像属性

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')

# 基本属性
print(f"形状: {img.shape}")        # (H, W, C)
print(f"尺寸: {img.size}")         # 总像素数
print(f"数据类型: {img.dtype}")    # uint8
```

### 4.2 像素访问与修改

```python
# 访问单个像素 (BGR格式)
pixel = img[100, 100]  # 第100行第100列

# 修改像素值
img[100, 100] = [255, 255, 255]  # 设为白色

# 区域访问
region = img[50:100, 50:100]  # ROI区域
```

### 4.3 图像通道操作

```python
# 分离通道
b, g, r = cv2.split(img)

# 合并通道
img_merged = cv2.merge([b, g, r])

# HSV颜色空间转换
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```

### 4.4 图像缩放

```python
# 按比例缩放
resized = cv2.resize(img, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)

# 按指定尺寸缩放
resized = cv2.resize(img, (800, 600))
```

### 4.5 ROI操作

```python
# 定义ROI
x, y, w, h = 100, 100, 200, 200
roi = img[y:y+h, x:x+w]

# 对ROI进行操作后放回
roi_blurred = cv2.GaussianBlur(roi, (21, 21), 0)
img[y:y+h, x:x+w] = roi_blurred
```

---

## 📝 五、练习题

### 基础练习

1. **图像读取与显示** - 读取图像并显示基本信息
2. **图像基本操作** - 对ROI进行模糊处理
3. **图像通道操作** - 分离并显示各通道

### 进阶练习

4. **图像批处理** - 批量处理文件夹中的图像
5. **图像处理工具** - 实现亮度、对比度调整
6. **综合应用** - 实现完整的图像处理流程

---

## 📚 扩展阅读

- 官方文档: https://docs.opencv.org/
- OpenCV Python教程: https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html
- Learn OpenCV: https://learnopencv.com/

---

## ✅ 今日总结

| 知识点 | 内容 | 掌握程度 |
|--------|------|----------|
| 计算机视觉定义 | 让机器理解图像内容的科学 | ⭐⭐⭐⭐⭐ |
| OpenCV安装 | pip install opencv-python | ⭐⭐⭐⭐⭐ |
| 图像读取 | cv2.imread() | ⭐⭐⭐⭐⭐ |
| 图像显示 | cv2.imshow() + waitKey() | ⭐⭐⭐⭐⭐ |
| 图像保存 | cv2.imwrite() | ⭐⭐⭐⭐⭐ |
| 像素操作 | 访问和修改像素值 | ⭐⭐⭐⭐ |
| 通道操作 | split()和merge() | ⭐⭐⭐⭐ |
| ROI操作 | 感兴趣区域处理 | ⭐⭐⭐⭐ |

### 下节预告

**Day 2: 图像基础与色彩空间** - 像素操作详解、RGB/HSV/灰度色彩空间、色彩空间转换

---

*本课程由计算机视觉100天学习计划提供*
