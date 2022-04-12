#图片练习
import numpy as np
import cv2

np.set_printoptions(threshold=5)
## 创建一个宽800高800的白色画布
img = np.ones((800,800,3),np.uint8)
img *= 255

##林
cv2.line(img,(190,300),(280,300),(0,0,0),2)
cv2.line(img,(235,200),(235,500),(0,0,0),2)
cv2.line(img,(235,300),(200,400),(0,0,0),2)
cv2.line(img,(235,300),(280,400),(0,0,0),2)

cv2.line(img,(290,300),(380,300),(0,0,0),2)
cv2.line(img,(335,200),(335,500),(0,0,0),2)
cv2.line(img,(335,300),(300,400),(0,0,0),2)
cv2.line(img,(335,300),(380,400),(0,0,0),2)

##肯
cv2.line(img,(580,200),(580,300),(0,0,0),2)
cv2.line(img,(580,250),(620,250),(0,0,0),2)
cv2.line(img,(540,250),(540,300),(0,0,0),2)
cv2.line(img,(470,300),(660,300),(0,0,0),2)

pts=np.array([[520,500],[520,320],[620,320],[620,500],[590,490]], np.int32)


pts = pts.reshape((-1,1,2,))

cv2.polylines(img,[pts],False,(0,0,0),2)

cv2.line(img,(520,400),(590,400),(0,0,0),2)
cv2.line(img,(520,440),(590,440),(0,0,0),2)

font=cv2.FONT_HERSHEY_SCRIPT_COMPLEX


cv2.putText(img,"Lincoln",(220,700),font,3.5,(112,112,0),2)

a=cv2.imwrite("picture.jpg",img)
from matplotlib import pyplot as plt
%matplotlib inline
plt.imshow(cv2.imread('./picture.jpg',cv2.IMREAD_COLOR))
plt.title('my picture')
plt.show()
##结果
![林肯](https://www.imagebam.com/view/ME99ZMR)
#照片
import cv2 
from matplotlib import pyplot as plt
%matplotlib inline
    
 
path = r'D:\DATA\Aliyun-CV-main\photo\WechatIMG158.png'
    
 
image = cv2.imread(path) 

nose = image[126:156,306:348]


for i in range(6):
    for j in range(6):
        image[30*i:30*(i+1),42*j:42*(j+1)] = nose


cv2.imwrite("huihui-face.jpg",image)
plt.imshow(cv2.imread('./huihui-face.jpg',cv2.IMREAD_UNCHANGED))
plt.title('picture-rgb')
plt.show()
##结果
![照片](https://www.imagebam.com/view/ME99ZMT)
