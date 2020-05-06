
## 简介
该项目可以识别手的轮廓并标记出手指的交点，可判断出手指的数量。<br>
## 运行环境
操作系统:Mac OS <br>
平台:Python3 <br>
库：Opencv <br>
## 使用说明
* 使用Python运行new.py
* 按 b 捕捉背景（此时手不要出现在摄像头中）
* 按 r 重设背景
* 按 ESC 退出
## 过程与原理
### 1.使用opencv自带方法 `BackgroundSubtractorMOG2` 抽离背景；
<br>

```
bgModel = cv2.BackgroundSubtractorMOG2(0, bgSubThreshold)
```

建立抽离的背景的蒙版
```
fgmask = bgModel.apply(frame)
```

将蒙版应用到帧上
```
res = cv2.bitwise_and(frame, frame, mask=fgmask)
```
<br>

### 2.用高斯模糊和阈值来将抽离背景后帧图片转换为二值图; 
<br>

先把图片变为灰度图
```
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

再进行高斯模糊
```
blur = cv2.GaussianBlur(gray, (blurValue, blurValue), 0)
```

设置阈值将其变为二值图
```
ret, thresh = cv2.threshold(blur, threshold, 255, cv2.THRESH_BINARY)
```
<br>

### 3.获取轮廓并找出手指交点
<br>

获取轮廓
```
contours, hierarchy = cv2.findContours(thresh1, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
```

找出轮廓的缺点（手指的交点）
```
hull = cv2.convexHull(res)<br>
defects = cv2.convexityDefects(res, hull)
```
<br>

## 结果演示
![1](https://github.com/ESoapW/Final_Luyouyuanli/blob/master/pics/1.png?raw=true) 
<br>

![2](https://github.com/ESoapW/Final_Luyouyuanli/blob/master/pics/2.png?raw=true) 
<br>

![3](https://github.com/ESoapW/Final_Luyouyuanli/blob/master/pics/3.png?raw=true) 
<br>

## 参考资料
https://github.com/lzane/Fingers-Detection-using-OpenCV-and-Python/blob/master/README.md
by @Izane
