# IDEA-Debug调试

## Debug的设置

设置 Debug 连接方式：进入File-Settings-Dubgger：

![image-20221023203547863](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232105981.png)

默认是 Socket。Shared memory 是 Windows 特有的一 个属性，一般在 Windows 系统下建议使用此设置，内存占用相对较少。(一般无需改动，保持默认即可)

## 设置断点

在代码左侧空白区域，点击鼠标左键出现红色圆点，当设置一个断点则将右侧代码为debug调试起始位置。当设置多个断点时可进行断点之间的切换。

![image-20221023203946871](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232105586.png)

## 设置条件断点

调试的时候，在循环里增加条件判断，可以极大的提高效率。

鼠标移动到断点区域，鼠标右键即可添加条件，点击Done完成。可以在满足某个条件下，实施断点。

![image-20221023204813995](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232105146.png)

## 启动调试

点击右上角绿色小虫子即可，或在代码区域右键点击Debug'Xxx.mian'(快捷键为Shift+F9)：

![image-20221023205706239](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232106319.png)

![image-20221023205739929](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232105916.png)

## debug功能面板

![image-20221023210532902](https://cdn.jsdelivr.net/gh/letengzz/Two-C@main/img/Java/202210232106669.png)



