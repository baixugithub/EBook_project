# **Ebook说明**： 

##一、项目介绍：		
	系统由S3C2440A处理器和LCD触摸屏机组成。系统主要实现三大功能：
		1.首先用ASCII码、GBK码和freetype矢量字库获取字符点阵，
		2.然后解析不同编码的文件，获得文件里的字，
		3.最后在LCD的显示文档，通过从标准输入获得命令或者通过触摸屏滑动翻页。
##二、职责：
	1.根据系统总体设计的实际要求进行Linux系统裁剪定制；
	2.编写软件开发流程图和系统开发相应的技术文档；
	3.系统程序框架设计及驱动、应用程序的编写调试。
##三、软件环境：Ubuntu9.10、linux-3.4.2内核
四、硬件环境：PC宿主机、S3C2440A处理器、LCD触摸屏
五、开发工具：gcc、gdb调试工具、CuteFTP、SecureCRT、SourceInsight
  六、关键技术：U-Boot移植、Linux内核移植、文件系统移植、多线程操作、文件操作、链表操作、
				字符编码、矢量字体显示、FreeType2字库安装、tslib触摸屏库调用、SVGAlib图像库安装
##七、测试步骤：
```
	1. insmod  s3c_ts.ko
	2.执行ls /dev/event*	/* 确定是哪个设备节点对应触摸屏 */
	3. 配置触摸屏
		export TSLIB_TSDEVICE=/dev/input/event0
		export TSLIB_CALIBFILE=/etc/pointercal
		export TSLIB_CONFFILE=/etc/ts.conf
		export TSLIB_PLUGINDIR=/lib/ts
		export TSLIB_CONSOLEDEVICE=none
		export TSLIB_FBDEVICE=/dev/fb0
	4.校准触摸屏：执行ts_calibrate   
	5.telnetd -l /bin/sh  //启动telnet服务，为了登录进去观察CPU占用率
	  在secureCRT登录登录开发板，不能在后台运行，在后台运行不能从标准输入得到数据
	6.执行：
		./show_file -s 24 -d fb -f ./MSYH.TTF ./speech.txt
	7.ps -T		/* 查看所有线程 */
	8.top 查看CPU占用率
	
```
