---
title: 在手机上启用USB调试
author: 神经元
---
如果想要在手机与电脑之间使用adb通信，您还需要在手机上打开USB调试。

首先打开手机的设置，滑动屏幕到最下方，打开关于手机。  
![](~./5.jpg)

连续点击7次版本号，您将会看到“您现在处于开发者模式！”的提示。  
![](~./1.jpg)

之后返回到设备主页，打开系统中的开发者选项  
![](~./6.jpg)  
![](~./2.jpg)

打开USB调试开关  
![](~./3.jpg)

在您使用USB线缆将手机连接至电脑并在电脑上启动adb服务后，您将在手机上看到这样一条提示。 

::: danger
**警告：除非您的手机连接至您的个人计算机上，并且您完全清楚您或者您计算机上的软件正在做什么，请不要点击确定。请勿在任何公共场所或您的手机连接至来历不明的设备（例如：火车站或飞机场的充电桩）时允许USB调试，adb拥有比手机上普通软件高的多的权限，包括任意安装或卸载应用，截取手机屏幕上显示的内容，模拟点击等。**  
:::

![](~./4.png)  

如果您确定要允许连接的计算机调试您的设备，请点击确定。