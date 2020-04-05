# Lenovo-G400-EFI-For-10.14.6
来自https://github.com/autersu/Lenovo_G400_EFI
在原EFI的基础上删改些内容以适应我的（大多数人）的电脑
下面的内容来自原贴
# Lenovo_G400_EFI
>Lenovo G400 EFI for Mojave10.14.6 它致力于让您直接将EFI替换掉就可以开箱即用。\
>1.Clover登陆主题换成更漂亮的YosemiteLogin \
>2.对基本的补丁做了添加 \
>3.对声卡和显存已经进行了处理。但是像无线网卡还是需要个人去配置的，方法见下文介绍（删除无线网卡驱动，G400自带的网卡不适用）


## 机型以及配置说明
* 电脑型号	联想 Lenovo G400 20235 笔记本电脑    
* 处理器	英特尔 第三代酷睿 i5-3230M @ 2.60GHz 双核 四线程
* 主板	联想 00000000Not Defined ( Intel HM76 Express 芯片组 )
* 内存	8 GB ( 三星 DDR3L 1600MHz / 记忆科技 DDR3L 1600MHz )
* 我的内存 4GB（ 记忆科技 DDR3L 1600MHz ）
* 主硬盘	西数 WDC WDS120G1G0A-00SS50 ( 120 GB / 固态硬盘 )
* 我的主硬盘 海康威视 C160 256G SSD
* 集成显卡	Intel(R) HD Graphics 4000 (2G显存)
* 核心显卡	AMD Radeon HD 8570M  (2G显存) 
* 声卡	Conexant SmartAudio HD @ 英特尔 Panther Point High Definition Audio Controller
* 有线网卡	Qualcomn Atheros AR8172 PCI-E Fast Ethernet) 
* 无线网卡	Qualcomn Atheros AR9485 Wireless Network Adapter
* 本EFI已去除无线网卡的支持
* 蓝牙	Qualcomn Atheros AR3012 Bluetooth 4.0

## 已经实现功能
1. 核心显卡(已经成功驱动，并已经注入缓冲区补丁，使得从默认的1536M正确显示为2048G)
2. 声卡(已经自动注入为3并成功驱动)
3. 有线网卡(成功驱动)
4. 内存(成功驱动)
5. 无线网卡(成功驱动，但是需要一些手段.安装方法见补充知识介绍部分)
6. 亮度调节(已经自动加入补丁，不需要任何配置)
7. ...

## 无法实现
1. 在笔记本上独显无法被驱动(原理性问题,但是好像可以通过屏蔽集显解决，但是g400应该做不到)
2. 蓝牙在10.13之后就无法被成功驱动，即使驱动也无法进行关闭和连接操作，不过由于复杂和对于蓝牙的非必要需求，所以去掉了该模块。当然也可以使之操作，操作方法见链接：[在10.13利用虚拟机软件实现BTFirmwareUploader的工作](https://osxlatitude.com/forums/topic/10127-updated-nov-2017-fix-btfirmwareuploader-in-macos-high-sierra/)
3. 开启HiDPI从而实现画质更清晰加载，这个由于电脑本身属于1366*768的屏幕，所以开启也没有多大意义。所以没有尝试，不过如果外接1080P屏幕或以上，则可以尝试使用。方法见链接[HiDPI的介绍和工具说明](https://www.sqlsec.com/2018/09/hidpi.html)

## 驱动名称介绍
1. FakeSMC.kext(安装hackintosh的核心驱动程序，没有它就没法在电脑上运行MacOS)必备
2. Lilu.kext(内核扩展程序，是其它程序的前置运行程序)必备
3. WhateverGreen.kext(显卡综合修复，整合核显，AMD,NVIDIA的综合修复)必备
4. AppleALC.kext(动态对系统注入必要的文件/打补丁以驱动声卡)
5. IntelGraphicsDVMTFixup.kext(修正 Broadwell/Skylake 平台核显因 DVMT 不足而导致的死机(依赖于Lilu)
6. AirportBrcmFixup(修补Broadcom Wi-Fi综合问题,是博通网上需要的)KILL
7. FakePCIID.kext(仿冒PCI设备核心驱动，部分驱动依赖于它)
8. ACPIBatteryManager.kext(笔记本电池管理驱动)
9. RealtekRTL8xxx.kext(Realtek 8xxx网卡驱动程序)KILL
10. VoodooPS2Controller.kext(Voodoo键盘/鼠标驱动程序)
11. RtWlanU.kext(USB网卡驱动)
12. HoRNDIS.kext(实现Mac通过安卓上网的驱动)KILL(此版本在我电脑上不支持，已更换为安装版，可自行谷歌下载）
13. ...


## 补充知识介绍
0. [国外大神发表的驱动地(国内各种论坛的基本上都是从这个拷贝的)](https://bitbucket.org/RehabMan/)
1. [安装10.14 Mojave所需硬件以及常见的问题](https://www.tonymacx86.com/threads/readme-common-problems-and-workarounds-on-10-14-mojave.255823/)
2. [安装第三方驱动最好应该在/Library/Extensions还是EFI/Clover/Kexts/Other?](https://www.tonymacx86.com/threads/guide-installing-3rd-party-kexts-el-capitan-sierra-high-sierra-mojave-catalina.268964/)
3. [Mojave10.14.16安装镜像以及安装方法(国内版)](https://blog.daliansky.net/macOS-Mojave-10.14.6-18G87-Release-version-with-Clover-5033-original-image.html)
4. [国外版安装教程](https://www.tonymacx86.com/threads/unibeast-install-macos-mojave-on-any-supported-intel-based-pc.259381/)
5. [一个推荐用来下载驱动和优化工具的国内网站](http://www.pc6.com/mac/qdcx_811_1.html)
6. [高通无线网卡驱动安装用法 AR946X AR9485 AR9565 亲测可用](http://bbs.pcbeta.com/viewthread-1806854-1-2.html)
7. [电脑亮度的驱动安装方法(国外大神官方指导)](https://bitbucket.org/RehabMan/applebacklightfixup/src/master/README.md)
8. [声卡id的注入方法](https://www.jianshu.com/p/955ce6706ae2)
9. ...
---
## 操作系统基本知识
1. 目前来说固件大致分两种:*Legacy BIOS*和*BIOS UEFI*,他们统称为BIOS，但是为了区别他们，我们把前者叫做bios,把后者叫做uefi。这个可以开机在BIOS中进行设置。至于选取的原则是：**能用UEFI就用UEFI，除非是像WindowsXP这种不支持MBR的系统。** 同样，分区表也可以分两种：*MBR*和*GPT*，至于选取原则见后续说明。
2. [UEFI的基本介绍](https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface)
3. MBR和GPT分区表的选取原则:[介绍1](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Disks) [介绍2](https://wiki.archlinux.org/index.php/Partitioning#GUID_Partition_Table)
4. 一般来说，我们应该使用**UEFI+GPT**或者**BIOS+MBR**这两个组合，其它的组合如*UEFI+MBR*和*BIOS+GPT*会产生问题(archwiki还是gentoo上曾经看到过一篇文章专门介绍这两种奇怪组合，但是找不到了，见谅)。而对于HACKINTOSH而言，我们应该选择**UEFI+GPT**
5. [bootloader的种类和介绍](https://wiki.archlinux.org/index.php/Arch_boot_process#Boot_loader)
6. [Linux启动过程](https://en.wikipedia.org/wiki/Linux_startup_process)
7. ...




