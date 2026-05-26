# Day 3: 图像处理基础操作

> 📅 2026-05-28 | 🎯 100天计算机视觉学习计划 | Day 3/100

---

## 📚 推荐学习资源

### 🎬 视频课程
- **[OpenCV入门到精通 - B站](https://www.bilibili.com/video/BV1oworBHEsF)** - 完整OpenCV基础教程，含图像基本操作章节
- **[黑马程序员OpenCV入门 - B站 P1-P5](https://www.bilibili.com/video/BV1Fo4y1d7JL)** - 图像读取、显示、保存基础操作
- **[OpenCV Course - YouTube](https://www.youtube.com/watch?v=oXlwWbU8l2o)** - freeCodeCamp完整教程，Section #1-Basics

### 📖 百科与技术文档
- **[OpenCV官方文档: 几何图像变换](https://docs.opencv.ac.cn/4.13.0/da/d54/group__imgproc__transform.html)** - 官方变换函数参考
- **[Wikipedia: Affine Transformation](https://en.wikipedia.org/wiki/Affine_transformation)** - 仿射变换数学原理
- **[OpenCV: Geometric Image Transformations](https://docs.opencv.org/4.x/da/d54/group__imgproc__transform.html)** - 官方英文文档
- **[CSDN: 仿射变换与透视变换实战](https://blog.csdn.net/Sunhen_Qiletian/article/details/158883903)** - 两种变换的区别与代码实现

---

## 📸 配图

![图像处理基础操作](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day003/cv_day003_cover.jpg)

![几何变换示意图](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day003/cv_day003_transform.jpg)

---

## 📜 历史背景

图像处理基础操作是计算机视觉的"基本功"，从20世纪60年代数字图像诞生之初，这些操作就是所有视觉算法的基石。

### 图像处理库的演进
- **1960s-1970s**：NASA使用 Fortran 编写图像处理程序，用于卫星图像校正
- **1980s**：数字图像处理走向商业化，Adobe Photoshop（1990）诞生
- **1999年**：Intel发布OpenCV（Open Source Computer Vision Library），图像处理走向开源
- **2000s**：OpenCV逐步成为计算机视觉领域的"瑞士军刀"
- **2010s-至今**：OpenCV 4.x版本持续更新，支持GPU加速和深度学习集成

### OpenCV的诞生
1999年，Intel在俄罗斯的团队发布了OpenCV，最初目的是促进计算机视觉研究和产品开发。如今OpenCV已成为全球使用最广泛的计算机视觉库，支持C++、Python、Java等多种语言。

---

## 🧠 核心概念

### 1. 图像的读取、显示与保存

#### OpenCV读取图像
```python
import cv2

# 基本读取
img = cv2.imread('image.jpg')  # 读取彩色图像
img = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)  # 读取灰度图
img = cv2.imread('image.jpg', cv2.IMREAD_UNCHANGED)  # 读取含Alpha通道

# 读取失败检测
if img is None:
    print("图像读取失败！")
```

| 读取标志 | 说明 |
|----------|------|
| `cv2.IMREAD_COLOR` (1) | 彩色图像（默认） |
| `cv2.IMREAD_GRAYSCALE` (0) | 灰度图像 |
| `cv2.IMREAD_UNCHANGED` (-1) | 包含Alpha通道 |

#### 显示图像
```python
import cv2

cv2.imshow('Window Title', img)
cv2.waitKey(0)  # 等待按键，0表示无限等待
cv2.waitKey(5000)  # 等待5000毫秒
cv2.destroyAllWindows()  # 关闭所有窗口
```

#### 保存图像
```python
cv2.imwrite('output.jpg', img)  # 保存为JPEG
cv2.imwrite('output.png', img)  # 保存为PNG
cv2.imwrite('output.png', img, [cv2.IMWRITE_PNG_COMPRESSION, 9])
```

### 2. 图像属性获取

```python
import cv2

img = cv2.imread('image.jpg')

# 获取图像形状
print(img.shape)  # (高度, 宽度, 通道数)
# 例如: (1080, 1920, 3)

# 获取图像尺寸
height, width = img.shape[:2]
print(f"宽度: {width}, 高度: {height}")

# 获取图像总像素数
total_pixels = img.size  # = height * width * channels

# 获取图像数据类型
print(img.dtype)  # uint8
```

### 3. 基本几何变换

#### 缩放（Resize）
```python
import cv2

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 方法1：指定具体尺寸
resized = cv2.resize(img, (800, 600))

# 方法2：按比例缩放
scale = 0.5
resized = cv2.resize(img, (int(width*scale), int(height*scale)))

# 方法3：指定缩放因子（OpenCV 4.x）
resized = cv2.resize(img, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)
```

**插值方法对比**：
| 方法 | 适用场景 | 特点 |
|------|----------|------|
| `INTER_LINEAR` | 通用 | 速度与质量平衡（默认） |
| `INTER_AREA` | 缩小图像 | 质量最优 |
| `INTER_CUBIC` | 放大图像 | 质量优，速度较慢 |
| `INTER_LANCZOS4` | 放大图像 | 最高质量，最慢 |

#### 翻转（Flip）
```python
# 翻转图像
# flipCode: 0=垂直翻转, 1=水平翻转, -1=同时水平和垂直

flipped_vertical = cv2.flip(img, 0)   # 上下翻转
flipped_horizontal = cv2.flip(img, 1)  # 左右翻转
flipped_both = cv2.flip(img, -1)        # 同时翻转
```

#### 平移（Translation）
```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 定义平移矩阵：向右平移100像素，向下平移50像素
tx, ty = 100, 50
translation_matrix = np.float32([[1, 0, tx],
                                 [0, 1, ty]])

# 应用平移
translated = cv2.warpAffine(img, translation_matrix, (width, height))
```

#### 旋转（Rotation）
```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]
center = (width // 2, height // 2)

# 获取旋转矩阵（中心旋转）
angle = 45
scale = 1.0
rotation_matrix = cv2.getRotationMatrix2D(center, angle, scale)

# 应用旋转
rotated = cv2.warpAffine(img, rotation_matrix, (width, height))
```

### 4. 仿射变换与透视变换

#### 仿射变换（Affine Transformation）
仿射变换保持"平直性"和"平行性"，包括平移、旋转、缩放、剪切。

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 定义仿射变换：三点确定变换
# 原图中三点
pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
# 变换后三点
pts2 = np.float32([[10, 100], [200, 50], [100, 250]])

# 获取仿射变换矩阵
M = cv2.getAffineTransform(pts1, pts2)

# 应用仿射变换
result = cv2.warpAffine(img, M, (width, height))
```

#### 透视变换（Perspective Transformation）
透视变换保持"直线性"，但平行线可能不再平行。

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 定义透视变换：四点确定变换（原图→目标）
pts1 = np.float32([[56, 65], [368, 52], [28, 387], [389, 390]])
pts2 = np.float32([[0, 0], [300, 0], [0, 300], [300, 300]])

# 获取透视变换矩阵
M = cv2.getPerspectiveTransform(pts1, pts2)

# 应用透视变换
result = cv2.warpPerspective(img, M, (300, 300))
```

**仿射变换 vs 透视变换**：
| 特性 | 仿射变换 | 透视变换 |
|------|----------|----------|
| 变换点 | 3对对应点 | 4对对应点 |
| 矩阵维度 | 2×3 | 3×3 |
| 平行性 | 保持 | 可能改变 |
| 应用场景 | 倾斜矫正、旋转 | 透视矫正、文档扫描 |

### 5. 裁剪（Crop）

```python
import cv2

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 裁剪图像 [y1:y2, x1:x2]
# 例如：裁剪中心区域
cropped = img[height//4:3*height//4, width//4:3*width//4]

# 裁剪ROI（感兴趣区域）
roi = img[100:300, 200:400]
```

---

## 👨‍🔬 科学家故事

### Gary Bradski：OpenCV的创始人

Gary Bradski是OpenCV的开创者之一。1999年，他在Intel工作时发起了OpenCV项目，目标是创建一个开源的计算机视觉库，促进学术研究和商业应用。

Bradski的远见在于认识到计算机视觉领域需要标准化的工具和算法基础。OpenCV的诞生极大地降低了计算机视觉研究的门槛，让更多研究者能够专注于算法创新而非底层实现。

除了OpenCV，Bradski还发明了著名的LBP（Local Binary Patterns）特征，并在机器人视觉、动作识别等领域有重要贡献。他在斯坦福大学担任兼职教授，继续推动计算机视觉教育。

> *"OpenCV的目的是让机器能够看见，而不仅仅是让研究人员能够工作。"*
> — Gary Bradski

---

## 📚 重要文献

1. **Bradski, G. (2000).** *The OpenCV Library*. Dr. Dobb's Journal of Software Tools.
   - OpenCV官方介绍文章

2. **谢尔希·贝尔斯基 (2019).** *Learning OpenCV 4 Computer Vision with Python 3*. Packt Publishing.
   - OpenCV权威教程书籍

3. **Kaehler, A., & Bradski, G. (2016).** *Learning OpenCV 3: Computer Vision in C++ with the OpenCV Library*. O'Reilly Media.
   - C++版OpenCV学习指南

4. **OpenCV Documentation.** *Geometric Image Transformations*. docs.opencv.org.
   - 官方变换函数文档

---

## 🔬 经典实验

### 实验：文档扫描仪的透视矫正

**背景**：用手机拍摄文档时，由于拍摄角度问题，文档往往呈现梯形或任意四边形变形。透视变换可以将不规则的文档矫正为标准的矩形。

**技术流程**：
1. **边缘检测**：使用Canny算子检测文档边缘
2. **轮廓提取**：找到文档的四个角点
3. **角点排序**：按左上、右上、右下、左下排序
4. **目标点定义**：定义标准矩形的四个角点
5. **透视变换**：应用`cv2.getPerspectiveTransform`和`cv2.warpPerspective`

**代码实现**：
```python
import cv2
import numpy as np

# 读取图像并转为灰度
img = cv2.imread('document.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# 边缘检测
edged = cv2.Canny(gray, 75, 200)

# 轮廓检测
contours, _ = cv2.findContours(edged, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)
contours = sorted(contours, key=cv2.contourArea, reverse=True)[:5]

# 近似多边形
for cnt in contours:
    peri = cv2.arcLength(cnt, True)
    approx = cv2.approxPolyDP(cnt, 0.02*peri, True)
    if len(approx) == 4:
        pts = approx.reshape(4, 2)
        break

# 透视变换
def order_points(pts):
    # 排序：左上、右上、右下、左下
    rect = np.zeros((4, 2), dtype=np.float32)
    pts = pts.astype(np.float32)
    rect[0] = pts[np.argmin(pts.sum(axis=1))]
    rect[2] = pts[np.argmax(pts.sum(axis=1))]
    rect[1] = pts[np.argmin(np.diff(pts, axis=1))]
    rect[3] = pts[np.argmax(np.diff(pts, axis=1))]
    return rect

rect = order_points(pts)
(tl, tr, br, bl) = rect

# 计算目标宽度
widthA = np.sqrt(((br[0]-bl[0])**2)+((br[1]-bl[1])**2))
widthB = np.sqrt(((tr[0]-tl[0])**2)+((tr[1]-tl[1])**2))
maxWidth = max(int(widthA), int(widthB))
heightA = np.sqrt(((tr[0]-br[0])**2)+((tr[1]-br[1])**2))
heightB = np.sqrt(((tl[0]-bl[0])**2)+((tl[1]-bl[1])**2))
maxHeight = max(int(heightA), int(heightB))

# 透视变换矩阵
dst = np.array([[0, 0], [maxWidth-1, 0], [maxWidth-1, maxHeight-1], [0, maxHeight-1]], dtype=np.float32)
M = cv2.getPerspectiveTransform(rect, dst)
warped = cv2.warpPerspective(img, M, (maxWidth, maxHeight))
```

**结果**：扭曲的文档被矫正为标准矩形，便于后续OCR识别。

---

## 📖 小故事

### "扫码"背后的秘密

当你用手机扫描二维码或拍下收据时，手机是如何"矫正"这些变形的？

答案就是**透视变换**。即使二维码从斜上方拍摄，手机拍摄的图片中二维码会呈现梯形或任意四边形。通过检测二维码的三个角定位点（QR码的定位图案），计算透视变换矩阵，就能将变形的二维码"展平"为标准正方形，然后进行解码。

这个过程每秒在全球发生数十亿次——快递员扫描包裹、售货员收款、博物馆扫描门票……透视变换技术让这一切成为可能。

### OpenCV：计算机视觉的"Linux"

Gary Bradski曾说，OpenCV之于计算机视觉，就像Linux之于服务器——它提供了一个免费的、公共的、所有人都能使用的平台。

OpenCV的诞生打破了商业软件的垄断，让发展中国家的学生和研究机构也能接触到前沿的计算机视觉技术。如今，全球有数百万开发者在使用OpenCV，它已经成为计算机视觉领域的"基础设施"。

---

## 💡 思考题

1. **基础题**：使用`cv2.warpAffine`和`cv2.warpPerspective`有什么区别？什么时候应该用仿射变换，什么时候应该用透视变换？

2. **进阶题**：在缩放图像时，为什么OpenCV提供了多种插值方法（如INTER_AREA、INTER_CUBIC）？它们各自的优势和劣势是什么？

3. **思考题**：仿射变换和透视变换的数学表示有什么区别？仿射变换矩阵是2×3，透视变换矩阵是3×3，为什么维度不同？

4. **开放题**：设计一个"自动文档扫描仪"程序，需要哪些步骤？考虑边缘检测、角点检测、透视变换等各个环节。

---

## 📖 术语表

| 术语 | 英文 | 简要解释 |
|------|------|----------|
| 图像读取 | Image Reading | 使用imread读取图像文件到内存 |
| 图像显示 | Image Display | 使用imshow在窗口中显示图像 |
| 图像保存 | Image Saving | 使用imwrite将图像写入文件 |
| 缩放 | Resize | 改变图像的像素尺寸 |
| 翻转 | Flip | 沿水平/垂直轴翻转图像 |
| 平移 | Translation | 沿x/y方向移动图像 |
| 旋转 | Rotation | 绕指定中心点旋转图像 |
| 仿射变换 | Affine Transformation | 保持平行性的几何变换 |
| 透视变换 | Perspective Transformation | 可改变平行线的几何变换 |
| 插值 | Interpolation | 计算新像素值的方法 |
| 裁剪 | Crop | 提取图像的矩形子区域 |
| ROI | Region of Interest | 感兴趣区域 |
| 变换矩阵 | Transformation Matrix | 定义几何变换的数学矩阵 |

---

## 🔮 下节预告

**Day 4：灰度变换与直方图**

明天我们将学习图像的灰度变换技术，包括线性变换、对数变换、伽马变换等。同时我们将深入理解直方图的概念，学习直方图均衡化和自适应直方图均衡化（CLAHE）。这些技术是图像增强的核心手段，能够显著改善图像的视觉效果。

> 💡 *图像处理的基本功决定了后续所有复杂算法的起点。万丈高楼平地起，基础操作要扎实。*
