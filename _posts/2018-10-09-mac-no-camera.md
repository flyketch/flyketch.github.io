## MacBook 休眠后，摄像头打不卡

原因：摄像头基本上是在笔记本合上之后，重新打开的情况下不能打开，摄像头被其他程序占用，。

### 解决方法
```
sudo killall VDCAssistant
sudo killall AppleCameraAssistant
```