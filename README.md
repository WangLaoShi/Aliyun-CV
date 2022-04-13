# 第二节课作业

## 画名字

**目的：** 将自己的名字画在画布上

### 前期准备

```python
import numpy as np
import cv2

np.set_printoptions(threshold=5)
```

首先创建一个宽512长1024的画布，输出并观察

```python
img2 = 255*np.ones([512,1024,3],np.uint8)  #创建白色画布
a2 = cv2.imwrite('test1.jpg',img2)

from matplotlib import pyplot as plt
%matplotlib inline
plt.imshow(cv2.imread('./test1.jpg',cv2.IMREAD_COLOR))
plt.title('my picture')
plt.show()
```

![](https://s2.loli.net/2022/04/13/d4jv6XRNUJOatr2.png)

将画布输出，能将其作为参照物，对接下来的“画字”有帮助

### 创建画布

```python
# 创建一个宽512长1024的画布
# np.zeros((height,width,channels),dtype='uint8')

img_black = np.zeros([512,1024,3],np.uint8)  #创建纯黑色画布

img = 255*np.ones([512,1024,3],np.uint8)  #创建白色画布
```

### 开始写字

所有写字（代码）顺序都是按照正常笔画顺序进行

```python
# 写“杨”字
# “木”
cv2.line(img,(50,200),(200,200),(0,0,255),10) # 横
cv2.line(img,(125,150),(125,400),(0,0,255),10) # 竖
cv2.line(img,(125,200),(20,350),(0,0,255),10) # 撇
cv2.line(img,(125,200),(175,300),(0,0,255),10) # 捺
# “杨”字右边部分
# 多笔画
pts1 = np.array([[225,175],[325,175],[230,250],[390,250],[370,410],[300,380]],np.int32) 
pst1 = pts1.reshape((-1,1,2,))
cv2.polylines(img,[pts1],False,(0,0,255),10) 
# 两撇
cv2.line(img,(270,270),(200,380),(0,0,255),10)
cv2.line(img,(350,280),(250,395),(0,0,255),10)

# “宇”字
# 宝盖头
cv2.line(img,(490,150),(505,190),(0,0,255),10) # 点
cv2.line(img,(405,160),(405,215),(0,0,255),10) # 竖
cv2.line(img,(405,185),(590,185),(0,0,255),10) # 横
cv2.line(img,(590,185),(560,210),(0,0,255),10) # 勾
# “于”
cv2.line(img,(455,225),(535,225),(0,0,255),10) # 短横
cv2.line(img,(425,280),(570,280),(0,0,255),10) # 长横
cv2.line(img,(495,225),(495,400),(0,0,255),10) # 竖
cv2.line(img,(495,400),(475,380),(0,0,255),10) # 勾

# 写“杰”字
# “木”
cv2.line(img,(620,225),(870,225),(0,0,255),10) # 横
cv2.line(img,(745,175),(745,390),(0,0,255),10) # 竖
cv2.line(img,(745,225),(595,385),(0,0,255),10) # 撇
cv2.line(img,(745,225),(850,350),(0,0,255),10) # 捺
# 四点
cv2.line(img,(615,420),(595,450),(0,0,255),10)
cv2.line(img,(695,420),(720,440),(0,0,255),10)
cv2.line(img,(775,420),(800,440),(0,0,255),10)
cv2.line(img,(845,420),(865,450),(0,0,255),10)

# 保存
a = cv2.imwrite('Name.jpg',img)  
```

### 最终输出

```python
from matplotlib import pyplot as plt
%matplotlib inline
plt.imshow(cv2.imread('./Name.jpg',cv2.IMREAD_COLOR))
plt.title('my picture')
plt.show()
```

![](https://s2.loli.net/2022/04/13/NKO3jCyWgvJ4bHw.png)

## 图片内容替换

**目的：**将图片中的鼻子部分截取，并替换图片左上角

### 读取图片

```python
import cv2

# path 图片路径
path = r'Aliyun-CV-main\ZYT photos\WechatIMG158.png'

# Reading an image in default mode 读取图片
image = cv2.imread(path,cv2.IMREAD_UNCHANGED)

# 将图片中“鼻子”部分取出
nose = image[118:156,313:349] #先y再x

# 将图片左上角部分替换为鼻子
for i in range(3): # [0,2]
    for j in range(5): # [0,4]
        image[38*(i):38*(i+1),36*(j):36*(j+1)] = nose

# 保存
cv2.imwrite('zyt-nose.jpg',image)
```

### 图片标注

中间其实缺少一个关键的隐藏步骤——怎样获取“鼻子”部分的位置信息？

由此，我们需要使用到**图片标注工具**

https://github.com/rachelcao277/LabelImage



通过标注后，得到了四个点的x,y轴的位置信息

```
[
    {
        "content": [
            {
                "x": 313.0514433456963,
                "y": 156.84653504058213
            },
            {
                "x": 349.84742206775434,
                "y": 156.84653504058213
            },
            {
                "x": 349.84742206775434,
                "y": 118.93552666027993
            },
            {
                "x": 313.0514433456963,
                "y": 118.93552666027993
            }
        ],
        "rectMask": {
            "xMin": 313.0514433456963,
            "yMin": 156.84653504058213,
            "width": 36.79597872205802,
            "height": -37.9110083803022
        },
        "labels": {
            "labelName": "未命名",
            "labelColor": "red",
            "labelColorRGB": "255,0,0",
            "visibility": false
        },
        "labelLocation": {
            "x": 331.44943270672536,
            "y": 137.89103085043104
        },
        "contentType": "rect"
    }
]
```

也就能取到图片中“鼻子”这部分了

```python
nose = image[118:156,313:349] #先y再x
```

### 最终输出

```python
from matplotlib import pyplot as plt
%matplotlib inline
plt.imshow(cv2.imread('./zyt-nose.jpg',cv2.IMREAD_UNCHANGED))
plt.title('picture-rgb')
plt.show()
```

![](https://s2.loli.net/2022/04/13/nK6NHofVmwb2DTs.png)

## 有关图床

将图片上传到云图床，方便将图片用markdown形式导出，利于md文件传出

（如果只是单纯的复制粘贴，图片的读取路径是自己电脑的绝对路径，别人拿到的md文件是加载不出图片的）

### 下载PicGo

一个非常好用的集成软件，将多种云图床集合于一体，更加便利

https://github.com/Molunerfinn/PicGo/releases

![](https://s2.loli.net/2022/04/13/1XVmk7MSBCrGeuh.png)

### 选取图床

PicGo自带有七种图床，我选取**SMMS**为主要图床

#### 创建账号

https://sm.ms/

每个账号自带5GB的图床空间，足够使用

#### 获取Token

https://sm.ms/home/apitoken

![](https://s2.loli.net/2022/04/13/uU3XAMY2wZetLJ6.png)

#### 配置图床

![](https://s2.loli.net/2022/04/13/NnpS9VU51IXwlbP.png)

现在就可以方便快捷地使用了！



**参考**

https://zhuanlan.zhihu.com/p/305041593
