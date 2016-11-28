
title: 光学脉搏测量 - PulseSensor试用
date: 2016-05-10 12:00:00 +0800
author: me
cover: http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/cover.png
draft: 
config:
    duoshuoKey: a-00009
tags:
    - code
    - arduino
    - love2d
preview: 

---

## demo展示

![](http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/IMG_1_2.jpg-w720p)

## 材料准备

### 硬件

+ windows平台一个(winXP+)
+ arduino开发板一块
	* 至少有一路ADC
	* 至少有一路串口
+ PulseSensor一个
	* 某宝上很多，价格在十几块到二十几块不等
+ 健康人类一只

笔者的演示环境如下：

+ Arduino Leonardo
+ SP4(Windows10 10586.218)

![](http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/IMG_3_2.jpg-h720p)

### 软件

+ [lua环境](http://files.luaforge.net/releases/luaforwindows/luaforwindows)
	* 安装5.1版本
+ [love2d](https://love2d.org/)
	* 请安装32位版本
+ [arduino IDE](https://www.arduino.cc/en/Main/Software)
	* 最新版本即可

## 下位机

### 器件连接

传感器引脚从左往右分别是`GND`,`VCC`和`SIG`，分别连接至`地`，`电源`和`ADC`口即可。传感器兼容3.3v-5v的驱动电压。
![连接图](http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/IMG_4_2.jpg)

### 代码

由于下位机代码太短，我就直接贴在这里了。

	void setup(void)
	{
		Serial.begin(115200);
	}
	void loop(void)
	{
		Serial.print("x:");
		Serial.print(analogRead(A0));
		Serial.print(",\n");
		delay(20);
	}

功能就是按照一定的频率把`A0`口的AD值以`x:{value},\n`的格式通过串口发送至上位机。

## 上位机

上位机上使用了一款小巧的跨平台开源图形引擎`love2d`来绘制界面。
你可以很容易的把在上面开发的程序移植到其他平台。


由于`love2d`引擎使用lua开发，笔者使用了一个[luars232](https://github.com/LuaDist2/luars232/releases)库来完成串口通信。

>> 经过笔者测试，这个luars232库有这样的bug，无法打开大于COM9的串口。所以如果你的设备连接上之后如果串口号超过了COM9，请手动改至COM0-9的范围。

上位机经过如下步骤便可得到题图所示的效果：

1. 下载并安装love2d引擎(32bits)
2. 下载并安装lua for windows环境
3. 使用lua中的`lua51.dll`替换love2d中的dll
4. git clone 我的demo项目
5. 将你的开发板连接至电脑，并调整COM口编号至合适范围
6. 编辑`\gui-love2d\main.lua`文件，将头部`rs232.open()`中的COM口改成你所使用的
7. 将`\gui-love2d\`目录下的文件打包成`zip`(不要打包目录)，并更改后缀为`.love`
8. 双击运行得到的`.love`文件即可

你可以先用arduino IDE自带的串口工具查看一下开发板的串口输出是否正常再进行下一步
![](http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/serial2.png)

最终，应该得到如下图所示的结果。
![](http://7xozbx.com1.z0.glb.clouddn.com/pulsesensor/window2.png)



>> ps. 第7点所述为love2d的打包方法之一，更多运行方法请参见官网  
>> ps.. 第3点是因为love2d使用了luajit，无法正常调用luars232，替换成原生lua即可  





>> 本项目Git:[https://github.com/Nigh/pulsesensor-demo]
