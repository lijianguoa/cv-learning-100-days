# Day 3: 图像绘制与几何变换

> 📅 2026-05-28 | 🎯 100天计算机视觉学习计划 | Day 3/100

---

## 📸 配图

![图像绘制与几何变换](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day003/cv_day003_cover.jpg)

![几何变换应用场景](https://raw.githubusercontent.com/lijianguoa/cv-images/main/day003/cv_day003_applications.jpg)

---

## 📜 历史背景

图像绘制与几何变换是计算机视觉最基础也最实用的技术之一，其历史与计算机图形学和数学有着深厚的渊源。

### 几何变换的数学根源

- **古希腊时期**：欧几里得几何（约公元前300年）奠定了平面几何的基础，平移、旋转、反射等变换概念由此诞生。[^1]

[^1]: [Wikipedia: Euclidean Geometry - 欧几里得几何](https://en.wikipedia.org/wiki/Euclidean_geometry)

- **17世纪**：笛卡尔发明坐标系，将几何问题转化为代数问题，为矩阵表示几何变换提供了数学工具。

- **18-19世纪**：射影几何（Projective Geometry）的发展为透视变换提供了理论框架。[^2]

[^2]: [Wikipedia: Projective Geometry - 射影几何](https://en.wikipedia.org/wiki/Projective_geometry)

### 计算机时代的图像变换

- **1960s**：NASA在阿波罗计划中使用仿射变换校正卫星和航天器拍摄的图像，这是几何变换最早的大规模实际应用之一。

- **1970s-1980s**：医学影像领域开始广泛使用几何变换进行图像配准（Image Registration），将不同时间或不同模态的医学图像对齐。[^3]

[^3]: [NCBI: A Survey of Medical Image Registration](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2396583/) - 医学图像配准综述

- **1990s**：随着数码相机的普及，图像拼接（Image Stitching）技术兴起，几何变换成为全景照片生成的核心技术。

- **2000s-至今**：OpenCV提供了完善的几何变换API，使这些技术变得触手可及。自动驾驶、增强现实（AR）、无人机航拍等领域大量依赖几何变换。

### OpenCV绘图功能的发展

OpenCV的绘图函数（`cv2.line`、`cv2.circle`、`cv2.rectangle`、`cv2.putText`等）是计算机视觉中最常用的可视化工具。从最初的简单标注到如今复杂的调试信息绘制，这些函数始终是CV工程师的"画笔"。[^4]

[^4]: [OpenCV官方文档: Drawing Functions](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html)

---

## 🧠 核心概念

### 1. 图像绘制基础

#### 绘制直线[^5]

[^5]: [OpenCV官方文档: cv2.line](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html#ga7078a9fae8c7e7d559806692f651b588)

```python
import cv2
import numpy as np

# 创建空白画布（黑色背景）
canvas = np.zeros((500, 500, 3), dtype=np.uint8)

# 绘制直线：cv2.line(图像, 起点, 终点, 颜色, 线宽)
cv2.line(canvas, (50, 50), (450, 50), (0, 255, 0), 3)       # 绿色水平线
cv2.line(canvas, (50, 50), (50, 450), (0, 0, 255), 3)       # 红色垂直线
cv2.line(canvas, (50, 50), (450, 450), (255, 0, 0), 3)      # 蓝色对角线

# OpenCV颜色格式：BGR（蓝、绿、红）
# 常用颜色：
# 红色 = (0, 0, 255)
# 绿色 = (0, 255, 0)
# 蓝色 = (255, 0, 0)
# 白色 = (255, 255, 255)
# 黄色 = (0, 255, 255)
```

#### 绘制矩形[^6]

[^6]: [OpenCV官方文档: cv2.rectangle](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html#ga07d2f74cadcf8e305e810ce8eed13bc9)

```python
# 绘制矩形：cv2.rectangle(图像, 左上角, 右下角, 颜色, 线宽)
cv2.rectangle(canvas, (100, 100), (300, 300), (0, 255, 0), 2)  # 绿色空心矩形
cv2.rectangle(canvas, (150, 150), (350, 350), (0, 0, 255), -1)  # 红色实心矩形（-1表示填充）
```

#### 绘制圆形[^7]

[^7]: [OpenCV官方文档: cv2.circle](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html#gaf10604b069374903dbd0f0488cb43670)

```python
# 绘制圆形：cv2.circle(图像, 圆心, 半径, 颜色, 线宽)
cv2.circle(canvas, (250, 250), 80, (255, 0, 0), 2)    # 蓝色空心圆
cv2.circle(canvas, (250, 250), 40, (0, 255, 255), -1)  # 黄色实心圆
```

#### 绘制椭圆[^8]

[^8]: [OpenCV官方文档: cv2.ellipse](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html#ga86dd30d6977f8f2ebd6b15b5b5e1e0f8)

```python
# 绘制椭圆：cv2.ellipse(图像, 中心, (长轴, 短轴), 旋转角度, 起始角, 终止角, 颜色, 线宽)
cv2.ellipse(canvas, (250, 250), (150, 80), 30, 0, 360, (255, 0, 255), 2)  # 紫色椭圆
```

#### 绘制文字[^9]

[^9]: [OpenCV官方文档: cv2.putText](https://docs.opencv.org/4.x/d6/d6e/group__imgproc__draw.html#ga5126f47f883d730f633dca3ec440e4ec)

```python
# 绘制文字：cv2.putText(图像, 文字, 位置, 字体, 字号, 颜色, 线宽)
font = cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(canvas, "OpenCV Drawing", (80, 480), font, 1.2, (255, 255, 255), 2)

# 常用字体：
# FONT_HERSHEY_SIMPLEX    - 正常大小无衬线字体
# FONT_HERSHEY_PLAIN      - 小号无衬线字体
# FONT_HERSHEY_DUPLEX     - 正常大小无衬线字体（更复杂）
# FONT_HERSHEY_COMPLEX    - 正常大小衬线字体
# FONT_HERSHEY_TRIPLEX    - 正常大小衬线字体（更复杂）
# FONT_HERSHEY_COMPLEX_SMALL - 小号衬线字体
# FONT_HERSHEY_SCRIPT_SIMPLEX - 手写风格字体
# FONT_HERSHEY_SCRIPT_COMPLEX - 手写风格字体（更复杂）
```

> 📎 **OpenCV绘图完整教程**：[OpenCV Python Tutorial: Drawing Functions](https://docs.opencv.org/4.x/dc/da5/tutorial_py_drawing_functions.html)

### 2. 图像缩放（Resize）

缩放是最常用的几何变换操作，通过插值算法计算新像素值。[^10]

[^10]: [Wikipedia: Image Scaling - 图像缩放与插值算法](https://en.wikipedia.org/wiki/Image_scaling)

```python
import cv2

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 方法1：指定目标尺寸
resized = cv2.resize(img, (800, 600))

# 方法2：按比例缩放
scale = 0.5
resized = cv2.resize(img, (int(width * scale), int(height * scale)))

# 方法3：使用缩放因子
resized = cv2.resize(img, None, fx=0.5, fy=0.5, interpolation=cv2.INTER_AREA)
```

**插值方法对比**：

| 方法 | 常量 | 适用场景 | 特点 |
|------|------|----------|------|
| 最近邻插值 | `INTER_NEAREST` | 速度优先 | 最快，质量最差 |
| 双线性插值 | `INTER_LINEAR` | 通用（默认） | 速度与质量平衡 |
| 双三次插值 | `INTER_CUBIC` | 放大图像 | 质量好，速度较慢 |
| Lanczos插值 | `INTER_LANCZOS4` | 高质量放大 | 最高质量，最慢 |
| 像素区域关系 | `INTER_AREA` | 缩小图像 | 缩小时抗锯齿效果最好 |

> 📎 **插值算法深入**：[双线性插值与双三次插值的数学原理](https://en.wikipedia.org/wiki/Bilinear_interpolation)

### 3. 图像旋转

旋转是绕某一点（通常是图像中心）按指定角度转动图像。[^11]

[^11]: [Wikipedia: Rotation Matrix - 二维旋转矩阵](https://en.wikipedia.org/wiki/Rotation_matrix)

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]
center = (width // 2, height // 2)

# 获取旋转矩阵
angle = 45  # 旋转角度（正值为逆时针）
scale = 1.0  # 缩放因子
rotation_matrix = cv2.getRotationMatrix2D(center, angle, scale)

# 应用旋转
rotated = cv2.warpAffine(img, rotation_matrix, (width, height))

# 保持完整图像的旋转（不裁剪）
def rotate_bound(image, angle):
    """旋转图像并保持完整内容"""
    h, w = image.shape[:2]
    cx, cy = w // 2, h // 2

    M = cv2.getRotationMatrix2D((cx, cy), angle, 1.0)
    cos_val = np.abs(M[0, 0])
    sin_val = np.abs(M[0, 1])

    # 计算新图像尺寸
    new_w = int((h * sin_val) + (w * cos_val))
    new_h = int((h * cos_val) + (w * sin_val))

    # 调整旋转矩阵的平移部分
    M[0, 2] += (new_w / 2) - cx
    M[1, 2] += (new_h / 2) - cy

    return cv2.warpAffine(image, M, (new_w, new_h))

rotated_full = rotate_bound(img, 30)
```

> 📎 **旋转矩阵推导**：[二维旋转矩阵的数学原理与推导](https://en.wikipedia.org/wiki/Rotation_matrix#In_two_dimensions)

### 4. 图像平移

平移是将图像沿x轴和y方向移动指定距离。[^12]

[^12]: [Wikipedia: Translation (geometry) - 几何平移变换](https://en.wikipedia.org/wiki/Translation_(geometry))

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

**平移矩阵的数学表示**：

$$T = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \end{bmatrix}$$

### 5. 仿射变换（Affine Transformation）

仿射变换是一种二维坐标变换，保持直线的"直线性"和"平行性"。[^13]

[^13]: [Wikipedia: Affine Transformation - 仿射变换详解](https://en.wikipedia.org/wiki/Affine_transformation)

仿射变换包含：**平移、旋转、缩放、剪切**及其任意组合。

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# 三点确定仿射变换
pts1 = np.float32([[50, 50], [200, 50], [50, 200]])
pts2 = np.float32([[10, 100], [200, 50], [100, 250]])

# 获取仿射变换矩阵
M = cv2.getAffineTransform(pts1, pts2)

# 应用仿射变换
result = cv2.warpAffine(img, M, (width, height))
```

> 📎 **OpenCV仿射变换**：[getAffineTransform和warpAffine函数详解](https://docs.opencv.org/4.x/da/d54/group__imgproc__transform.html#gab3e8cc9e4a6a4df3b5c3aa4c9a787f0e)

### 6. 透视变换（Perspective Transformation）

透视变换是一种更一般的变换，可以表示"近大远小"的透视效果。[^14]

[^14]: [Wikipedia: Homography - 单应性矩阵与透视变换](https://en.wikipedia.org/wiki/Homography_(computer_vision))

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')

# 四点确定透视变换
pts1 = np.float32([[56, 65], [368, 52], [28, 387], [389, 390]])
pts2 = np.float32([[0, 0], [300, 0], [0, 300], [300, 300]])

# 获取透视变换矩阵（3×3）
M = cv2.getPerspectiveTransform(pts1, pts2)

# 应用透视变换
result = cv2.warpPerspective(img, M, (300, 300))
```

**仿射变换 vs 透视变换**：

| 特性 | 仿射变换 | 透视变换 |
|------|----------|----------|
| 对应点 | 3对 | 4对 |
| 矩阵维度 | 2×3 | 3×3 |
| 平行性 | 保持 | 可能改变 |
| 直线性 | 保持 | 保持 |
| 自由度 | 6 | 8 |
| 典型应用 | 旋转、缩放、剪切 | 透视矫正、文档扫描 |
| OpenCV函数 | `warpAffine` | `warpPerspective` |

> 📎 **透视变换应用**：[PyImageSearch: 文档扫描仪的透视矫正](https://www.pyimagesearch.com/2014/09/01/complete-guide-building-image-scanners-cameras-opencv/)

### 7. 裁剪与边缘扩展

#### 图像裁剪

```python
import cv2

img = cv2.imread('image.jpg')
height, width = img.shape[:2]

# NumPy数组切片裁剪 [y1:y2, x1:x2]
cropped = img[100:400, 200:500]  # 裁剪ROI区域
```

#### 边缘扩展（Border Padding）[^15]

[^15]: [OpenCV官方文档: cv2.copyMakeBorder](https://docs.opencv.org/4.x/d2/de8/group__core__array.html#ga2ac104f5b0e7aca9b26ae4daf7d8b75c)

```python
import cv2
import numpy as np

img = cv2.imread('image.jpg')

# 边缘扩展：cv2.copyMakeBorder(图像, 上, 下, 左, 右, 边界类型)
BORDER_CONSTANT = cv2.copyMakeBorder(img, 50, 50, 50, 50, cv2.BORDER_CONSTANT, value=(0, 0, 255))
BORDER_REPLICATE = cv2.copyMakeBorder(img, 50, 50, 50, 50, cv2.BORDER_REPLICATE)
BORDER_REFLECT = cv2.copyMakeBorder(img, 50, 50, 50, 50, cv2.BORDER_REFLECT)
BORDER_WRAP = cv2.copyMakeBorder(img, 50, 50, 50, 50, cv2.BORDER_WRAP)
```

| 边界类型 | 说明 | 效果 |
|----------|------|------|
| `BORDER_CONSTANT` | 固定颜色填充 | 用指定颜色填充边缘 |
| `BORDER_REPLICATE` | 复制边缘像素 | 用最近的边缘像素值填充 |
| `BORDER_REFLECT` | 镜像反射 | 如fedcba\|abcdefgh\|gfedcba |
| `BORDER_REFLECT_101` | 不重复边缘的反射 | 如gfedcb\|abcdefgh\|gfedcba |
| `BORDER_WRAP` | 周期性填充 | 如cdefgh\|abcdefgh\|abcdefg |

---

## 👨‍🔬 科学家故事

### Albrecht Dürer（1471-1528）：透视几何的先驱

Albrecht Dürer是德国文艺复兴时期最伟大的艺术家之一，他不仅创作了《忧郁I》《骑士、死亡与恶魔》等传世名作，更在透视几何的理论研究中做出了开创性贡献。

1525年，Dürer出版了《Unterweisung der Messung》（测量指南），系统阐述了透视投影的数学原理。他设计了多种机械装置来辅助艺术家绘制透视效果，包括著名的"透视绘图仪"——通过网格和线绳将三维场景精确投影到二维画布上。[^16]

[^16]: [Wikipedia: Albrecht Dürer - 丢勒的生平与贡献](https://en.wikipedia.org/wiki/Albrecht_D%C3%BCrer)

Dürer的工作本质上就是在解决我们今天用透视变换矩阵解决的问题——将三维世界投影到二维平面。他的研究为后来射影几何和计算机视觉中的透视变换奠定了直观的几何理解。

> *"几何是所有绘画的基础。谁不了解几何，就无法成为真正的艺术家。"*
> — Albrecht Dürer

### Gary Bradski：OpenCV的创始人

Gary Bradski在Intel工作时于1999年发起了OpenCV项目，目标是创建一个开源的计算机视觉库。OpenCV的绘图函数和几何变换API正是Bradski团队精心设计的核心功能之一。[^17]

[^17]: [Wikipedia: Gary Bradski - OpenCV创始人](https://en.wikipedia.org/wiki/Gary_Bradski)

Bradski的远见在于认识到CV领域需要标准化的工具。OpenCV的`warpAffine`和`warpPerspective`函数让复杂的几何变换变得只需几行代码，极大地降低了CV技术的使用门槛。

---

## 📚 重要文献

1. **Hartley, R., & Zisserman, A. (2003).** *Multiple View Geometry in Computer Vision*. Cambridge University Press.
   - 计算机视觉几何的经典教材，深入讲解射影几何、单应性矩阵等[^18]

[^18]: [Multiple View Geometry in Computer Vision - 2nd Edition](https://www.robots.ox.ac.uk/~vgg/hzbook/)

2. **Szeliski, R. (2022).** *Computer Vision: Algorithms and Applications*. 2nd Edition, Springer.
   - CV领域权威教材，涵盖几何变换、图像拼接等[^19]

[^19]: [Computer Vision: Algorithms and Applications - 在线免费版](https://szeliski.org/Book/)

3. **Kaehler, A., & Bradski, G. (2017).** *Learning OpenCV 3 Computer Vision with Python*. O'Reilly Media.
   - OpenCV实战指南，包含丰富的绘图和变换示例

4. **Gonzalez, R. C., & Woods, R. E. (2018).** *Digital Image Processing*. 4th Edition, Pearson.
   - 数字图像处理经典教材，几何变换的理论基础[^20]

[^20]: [Digital Image Processing (Gonzalez & Woods) - 第4版](https://www.imageprocessingplace.com/)

5. **OpenCV Documentation.** *Geometric Image Transformations*. docs.opencv.org.
   - 官方几何变换函数文档[^21]

[^21]: [OpenCV: Geometric Image Transformations](https://docs.opencv.org/4.x/da/d54/group__imgproc__transform.html)

---

## 🔬 经典实验

### 实验：自动文档扫描仪（透视矫正）

**背景**：用手机拍摄文档时，由于拍摄角度问题，文档往往呈现梯形变形。透视变换可以将不规则的文档矫正为标准矩形。这是几何变换最经典的应用之一。

**技术流程**：
1. **灰度转换** → `cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)`
2. **边缘检测** → `cv2.Canny(gray, 75, 200)`
3. **轮廓查找** → `cv2.findContours`
4. **四边形近似** → `cv2.approxPolyDP`
5. **角点排序** → 按左上、右上、右下、左下排列
6. **透视变换** → `cv2.getPerspectiveTransform` + `cv2.warpPerspective`

**完整代码**：
```python
import cv2
import numpy as np

def order_points(pts):
    """将四个点按左上、右上、右下、左下排序"""
    rect = np.zeros((4, 2), dtype=np.float32)
    pts = pts.astype(np.float32)
    s = pts.sum(axis=1)
    rect[0] = pts[np.argmin(s)]  # 左上（x+y最小）
    rect[2] = pts[np.argmax(s)]  # 右下（x+y最大）
    d = np.diff(pts, axis=1)
    rect[1] = pts[np.argmin(d)]  # 右上（x-y最小）
    rect[3] = pts[np.argmax(d)]  # 左下（x-y最大）
    return rect

def four_point_transform(image, pts):
    """执行透视变换"""
    rect = order_points(pts)
    (tl, tr, br, bl) = rect

    # 计算新图像的宽度
    widthA = np.sqrt(((br[0] - bl[0]) ** 2) + ((br[1] - bl[1]) ** 2))
    widthB = np.sqrt(((tr[0] - tl[0]) ** 2) + ((tr[1] - tl[1]) ** 2))
    maxWidth = max(int(widthA), int(widthB))

    # 计算新图像的高度
    heightA = np.sqrt(((tr[0] - br[0]) ** 2) + ((tr[1] - br[1]) ** 2))
    heightB = np.sqrt(((tl[0] - bl[0]) ** 2) + ((tl[1] - bl[1]) ** 2))
    maxHeight = max(int(heightA), int(heightB))

    # 目标点
    dst = np.array([
        [0, 0],
        [maxWidth - 1, 0],
        [maxWidth - 1, maxHeight - 1],
        [0, maxHeight - 1]], dtype=np.float32)

    # 获取透视变换矩阵并应用
    M = cv2.getPerspectiveTransform(rect, dst)
    warped = cv2.warpPerspective(image, M, (maxWidth, maxHeight))
    return warped

# 使用示例
img = cv2.imread('document.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
edged = cv2.Canny(gray, 75, 200)

contours, _ = cv2.findContours(edged, cv2.RETR_LIST, cv2.CHAIN_APPROX_SIMPLE)
contours = sorted(contours, key=cv2.contourArea, reverse=True)[:5]

for c in contours:
    peri = cv2.arcLength(c, True)
    approx = cv2.approxPolyDP(c, 0.02 * peri, True)
    if len(approx) == 4:
        pts = approx.reshape(4, 2)
        break

result = four_point_transform(img, pts)
cv2.imwrite('scanned_document.jpg', result)
```

> 📎 **完整教程**：[PyImageSearch: Building a Document Scanner](https://www.pyimagesearch.com/2014/09/01/complete-guide-building-image-scanners-cameras-opencv/)

---

## 📖 小故事

### "扫码"背后的透视变换

当你用手机扫描二维码时，即使从斜上方拍摄，二维码在图像中会呈现梯形变形。手机系统通过检测QR码的三个定位图案（Position Detection Patterns），计算透视变换矩阵，将变形的二维码"展平"为标准正方形，然后进行解码。

这个过程每秒在全球发生数十亿次——快递员扫描包裹、售货员收款、博物馆扫描门票……透视变换技术让这一切成为可能。

### 从丢勒到OpenCV：500年的透视之旅

1525年，Albrecht Dürer用线绳和木框构建了世界上第一台"透视绘图仪"。500年后，我们用一行代码就能完成同样的变换：

```python
M = cv2.getPerspectiveTransform(src_pts, dst_pts)
result = cv2.warpPerspective(img, M, (width, height))
```

从文艺复兴时期的机械装置到现代的矩阵运算，人类对透视的理解跨越了五个世纪。Dürer如果看到今天的计算机视觉技术，一定会感到惊叹。

---

## 💡 思考题

1. **基础题**：使用`cv2.warpAffine`和`cv2.warpPerspective`有什么区别？什么时候应该用仿射变换，什么时候应该用透视变换？

2. **进阶题**：在缩放图像时，OpenCV提供了多种插值方法（INTER_NEAREST、INTER_LINEAR、INTER_CUBIC等）。请解释双线性插值和双三次插值的原理，并说明为什么缩小图像时推荐使用`INTER_AREA`？
   > 💡 **提示**：参考[双线性插值与双三次插值的数学原理](https://en.wikipedia.org/wiki/Bilinear_interpolation)

3. **思考题**：仿射变换矩阵是2×3，透视变换矩阵是3×3，为什么维度不同？从数学角度解释仿射变换和透视变换的本质区别。
   > 💡 **提示**：阅读[射影几何与单应性变换](https://en.wikipedia.org/wiki/Homography_(computer_vision))

4. **开放题**：设计一个"自动文档扫描仪"程序，需要哪些步骤？考虑光照不均匀、文档边缘模糊、背景复杂等实际挑战。

---

## 📖 术语表

| 术语 | 英文 | 简要解释 |
|------|------|----------|
| 几何变换 | Geometric Transformation | 对图像像素位置进行数学变换的操作 |
| 缩放 | Resize / Scaling | [改变图像的像素尺寸](https://en.wikipedia.org/wiki/Image_scaling) |
| 旋转 | Rotation | [绕指定中心点旋转图像](https://en.wikipedia.org/wiki/Rotation_matrix) |
| 平移 | Translation | [沿x/y方向移动图像](https://en.wikipedia.org/wiki/Translation_(geometry)) |
| 仿射变换 | Affine Transformation | [保持平行性的几何变换（6个自由度）](https://en.wikipedia.org/wiki/Affine_transformation) |
| 透视变换 | Perspective Transform | [可改变平行线的几何变换（8个自由度）](https://en.wikipedia.org/wiki/Homography_(computer_vision)) |
| 单应性矩阵 | Homography Matrix | 透视变换的3×3矩阵表示 |
| 插值 | Interpolation | [计算新像素值的方法](https://en.wikipedia.org/wiki/Bilinear_interpolation) |
| 双线性插值 | Bilinear Interpolation | [基于4个邻近像素的加权平均插值](https://en.wikipedia.org/wiki/Bilinear_interpolation) |
| 双三次插值 | Bicubic Interpolation | 基于16个邻近像素的高阶插值 |
| 裁剪 | Crop | 提取图像的矩形子区域（ROI） |
| 边缘扩展 | Border Padding | 在图像边缘添加像素填充 |
| 变换矩阵 | Transformation Matrix | 定义几何变换的数学矩阵 |
| 射影几何 | Projective Geometry | [研究透视和投影性质的几何学分支](https://en.wikipedia.org/wiki/Projective_geometry) |
| 图像配准 | Image Registration | [将不同图像对齐到同一坐标系的技术](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2396583/) |

---

## 🔮 下节预告

**Day 4：图像滤波与增强**

明天我们将学习图像滤波的核心概念，包括卷积操作的原理、均值滤波、高斯滤波、中值滤波和双边滤波。这些滤波技术是图像去噪和增强的基础，也是后续边缘检测、特征提取等高级操作的前提。我们还将了解图像锐化与边缘增强技术，理解空间域滤波的工作机制。

> 💡 *几何变换让我们能够"操控"图像的形状，而滤波则让我们能够"操控"图像的内容。两者结合，构成了图像处理的两大支柱。*
