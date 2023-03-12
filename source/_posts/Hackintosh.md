---
title: RedmiBook14 黑苹果 EFI 及个人的思路
date: 2023-03-12 19:07:59
tags: [黑苹果，教程，EFI]
cover: https://bing.com/th?id=OHR.SouthDownsSheep_ZH-CN8986424729_1920x1080.jpg&qlt=100
type: post
---
## 前言
本人目前在用的这个笔记本大概是 2019 购入的，反正是疫情之前。 
目前用 Windows 风扇上天。  
突然心血来潮装个黑苹果玩玩，看了看最基础的就开始装了。
> srds 不要像我这样，先了解清楚再搞能少走很多弯路（哭  

然后先找了别人安装成功的 EFI，但是太过远古，然后又修修修  
目前是比较完整的一版，给 RedmiBook14 用的，各位可以看看能否用上  
跟我配置一样的话可以直接抄作业了，不一样的也可以看看后面的思路

## EFI 文件

### 详细配置：

 | 硬件名称 | 型号 |
 | :-----:| :----------------: |
 | CPU | 英特尔 酷睿 I7-8565U（Whiskey Lake 架构） |
 | 主板 | TIMI-1814 |
 | 声卡 | 瑞昱 ALC256 |
 | 网卡 | 英特尔 Wireless  AC-9624 |
 | 独显 | 英伟达 MX250（无解已屏蔽） |
 | 集显 | 英特尔 Graphics UHD620 |
 | 内存 | 三星 8G 2400Mhz |
 | 硬盘 | 三星 PM871B 固态 512G（MZNLN512HAJQ-00000） |

 ### 使用情况

|硬件 | 状态 | 备注|
|:----:|:----:|:----:|
|无线网卡|✅ 支持 | 原生模式驱动，无需 Heliport|
|蓝牙|✅ 支持 |支持蓝牙耳机，AirDrop 未测试|
|合盖睡眠|✅ 支持 | 请谨慎使用 [HiDPi][HiDPi] 可能导致睡眠唤醒缩小、花屏等问题|
|USB|✅ 支持 | 定制 USB，有问题可能需要重新定制|
|电源管理|✅ 支持 | 原生支持|
|声音|✅ 支持 | 本机测试完美，Layout ID 17|
|HDMI 输出|✅ 支持 | 电视输出已测试|
|触摸板|⍻ 不完全支持 | 仅触摸，手势无效|
|独显|❌ 不支持|MX250 无解，屏蔽|
|麦克风|🤷 未测试 | 貌似无效|

### 版本及测试情况

OpenCore 版本 : 0.8.8

macOS 版本 : Ventura 13.2 (22D49)

### 下载地址
[文件下载 >](https://github.com/Zachery-Liu/RedmiBook-8thGen-OpenCore-EFI/releases/tag/stable_v0.8.8-22D49)

## 基本思路

1. 先找别人安装成功过的 EFI，确认是 OpenCore 的，版本无所谓。
2. 在 Windows 下使用 OCAT 升级。
3. 写启动盘。
4. 安装。
> 这里很可能没法进安装界面，想办法修改，包括不限于升级驱动、补新驱动等方法，只要能进去一切都好说。
5. 进系统
6. 补驱动，把所有没驱动起来的东西都驱动起来。