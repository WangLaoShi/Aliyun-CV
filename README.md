# Aliyun-CV# 第一节课回顾

- 在开始之前有第0步——选择合适的处理环境
- 拿到数据首先要对数据进行基本处理，**观察数据**

  可以直接用EDA工具对数据进行快速处理

```python
import pandas_profiling

pandas_profiling.ProfileReport(df)
```

- 其中有约3W张图片，需要每张去看吗？—— 答案是YES

  根据数据观察可知，每张图基本都有不同，而且每张图片的内容大同小异，涉及的场景也有区别

# 第二节课预习

## 读取图像

```python
cv2.imread(filepath,flags)
```

- filepath

  要读入图片的完整路径

- flags

  - `cv2.IMREAD_COLOR`

    > 默认参数，读入一副彩色图片，忽略alpha通道

  - `cv2.IMREAD_GRAYSCALE`

    > 读入灰度图片

  - `cv2.IMREAD_UNCHANGED`

    > 顾名思义，读入完整图片，包括alpha通道

## 显示图像

```python
cv2.imshow('image',img)
```

- wname：显示图像窗口的名字

- img：要显示的图像（imread读入的图像）


> 窗口大小自动调整为图片大小

```python
cv2.waitKey(0)
```

顾名思义等待键盘输入，单位为毫秒，即等待指定的毫秒数看是否有键盘输入，若在等待时间内按下任意键则返回按键的ASCII码，程序继续运行。若没有按下任何键，超时后返回-1。参数为0表示无限等待。不调用waitKey的话，窗口会一闪而逝，看不到显示的图片。

```python
cv2.destroyAllWindows()
```

销毁所有窗口

```python
cv2.destroyWindow(wname)
```

销毁指定窗口

## 保存图像

```python
cv2.imwrite(file，img，num)
# 例子
cv2.imwrite('1.png',img, [int( cv2.IMWRITE_JPEG_QUALITY), 95])
cv2.imwrite('1.png',img, [int(cv2.IMWRITE_PNG_COMPRESSION), 9])
```

- file：要保存的文件名

- img：要保存的图像

- num

  > 可选参数

  对于**JPEG**，其表示的是图像的质量，用0 - 100的整数表示，默认95

  对于**png** ,第三个参数表示的是压缩级别。默认为3

  - `cv2.IMWRITE_JPEG_QUALITY`

    类型为 long ,必须转换成 int

  - `cv2.IMWRITE_PNG_COMPRESSION`

    从0到9 压缩级别越高图像越小

## 图片操作

```python
cv2.flip(img,flipcode)
# 例子
imgflip = cv2.flip(img,1)
```

翻转图像

- flipcode = 0：沿x轴翻转
- flipcode > 0：沿y轴翻转
- flipcode < 0：x,y轴同时翻转

```python
imgcopy = img.copy()
```

复制图像





*后面有点看不懂= =* 

 
