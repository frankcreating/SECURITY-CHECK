# windows系统下，基于python的各类安全检测脚本
#### 更新说明
1. 日期:2024年3月11日
2. 更新内容:
#### 介绍
windows系统下，基于python的各类安全检测脚本
主要场景：
1.  办公室里检测是否有非法插入的u盘，可移动设备接入
2.  内网电脑是否非法联网
3.  定时屏幕截图
4.  计算机信息
5. 
## 用法环境配置
1. 封装成exe文件后执行
2. pip包: pillow,pywin32
3. 最低支持python3.4
4. 仅截图功能暂时不支持xp系统
5. 如无需xp系统支持，可直接使用其他系统打包即可
6. 
## 软件启动后

1. 定时屏幕截图:<br>
   (1). 发现联网或usb接入→<br>
        截图保存→<br>
        计数次数达到标准→<br>
        强制关机指令<br>
   (2). 没发现联网或usb→<br>
        计数器时间延长，减少硬盘压力，上限1200秒→<br>
        继续检查直到发现为止<br>
2. usb可写报警:<br>
检测到可写入硬盘→<br>
记录硬盘数据→<br>
计数器→<br>
通知用户拔出→<br>
截图→<br>
强制关机阻止用户行为<br>
3. 计算机信息:计算机名，ip地址
4. windows下设置自启动:检查指定目录下是否有软件，不管有没有尝试复制一份过去→注册自启动
5. 托盘:透明,常规信息提醒使用winOperator.myOperator.warm()函数
6. 日志记录:常规记录→检查日志大小→确认是否重置日志→写入
7. 指定软件后台检测到强制关闭,增加管理员密码，可开启或关闭这个功能


### 运维端口
1. 监控指定端口（8000），检查illegal文件夹是否有文件，有的话邮件报警并去现场检查
2. 日常巡查屏幕截图
3. 检查常规日志是否有异常
4. 使用网页浏览器8000端口访问目标ip，可查看计算机指定目录下的屏幕截图和相关信息
5. 客户端查看,自动化运维
6. 


### security_main.py:
```
#需要自己将这段代码保存到security_main.py里作为主程序
import os
import sys
from common import S_setting
from security_window import S_MainWindowWithRemove, S_window
from PyQt5.QtWidgets import QApplication
if __name__ == "__main__":
    app = QApplication(sys.argv)
    MyWindow=S_MainWindowWithRemove('S')
    a=S_window(MyWindow)
    MyWindow.showMinimized()
    a.thread_start(a)
    a.setDeamonStartUp()
    sys.exit(app.exec_())


```
### 打包
```
pyinstaller -F -w 
-i C:\icon\file_error.ico 
-n deamon security_main.py
```

### 特别鸣谢
1. 百度:文心一言
2. 作者:phoney