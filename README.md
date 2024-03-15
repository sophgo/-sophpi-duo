

简体中文 | [English](./README-en.md)

<br>

# 目录

- [目录](#目录)
- [项目简介](#项目简介)
  - [硬件资料](#硬件资料)
  - [芯片规格](#芯片规格)
- [SDK目录结构](#sdk目录结构)
- [快速开始](#快速开始)
  - [准备编译环境](#准备编译环境)
  - [获取SDK](#获取sdk)
  - [编译](#编译)
  - [SD卡烧录](#sd卡烧录)
- [关于算能](#关于算能)
- [技术论坛](#技术论坛)

<br>

# 项目简介
- 本仓库提供[算能科技](https://www.sophgo.com/)端侧芯片`CV181x`和`CV180x`两个系列芯片的软件开发包(SDK)。
- 主要适用于官方EVB

<br>

## 硬件资料
- [《CV180xB EVB板硬件指南》](https://sophon-file.sophon.cn/sophon-prod-s3/drive/23/03/14/14/CV180xB_EVB%E6%9D%BF%E7%A1%AC%E4%BB%B6%E6%8C%87%E5%8D%97_V1.0.pdf)
- [《CV180xC EVB板硬件指南》](https://sophon-file.sophon.cn/sophon-prod-s3/drive/23/03/18/18/CV180xC_EVB%E6%9D%BF%E7%A1%AC%E4%BB%B6%E6%8C%87%E5%8D%97_V1.0.pdf)
- [《CV181xC EVB板硬件指南》](https://sophon-file.sophon.cn/sophon-prod-s3/drive/23/03/15/14/CV181xC_QFN_EVB%E6%9D%BF%E7%A1%AC%E4%BB%B6%E6%8C%87%E5%8D%97_V1.0.pdf)
- [《CV181xH EVB板硬件指南》](https://sophon-file.sophon.cn/sophon-prod-s3/drive/23/03/15/15/CV181xH_EVB%E6%9D%BF%E7%A1%AC%E4%BB%B6%E6%8C%87%E5%8D%97_V1.0.pdf)

<br>

## 芯片规格
- [芯片产品简介](https://www.sophgo.com/product/index.html)
<br><br>

# SDK目录结构
```
.
├── build               // 编译目录，存放编译脚本以及各board差异化配置
├── buildroot-2021.05   // buildroot开源工具
├── freertos            // freertos系统
├── fsbl                // fsbl启动固件，prebuilt形式存在
├── install             // 执行一次完整编译后，各image的存放路径
├── isp_tuning          // 图像效果调试参数存放路径
├── linux_5.10          // 开源linux内核
├── middleware          // 自研多媒体框架，包含so与ko
├── opensbi             // 开源opensbi库
├── ramdisk             // 存放最小文件系统的prebuilt目录
└── u-boot-2021.10      // 开源uboot代码
```

<br><br>

# 快速开始

## 准备编译环境
- 在虚拟机上安装一个ubuntu系统，或者使用本地的ubuntu系统，推荐`Ubuntu 20.04 LTS`
- 安装串口工具： `mobarXterm` 或者 `xshell` 或者其他
- 安装编译依赖的工具:
```
sudo apt install pkg-config
sudo apt install build-essential
sudo apt install ninja-build
sudo apt install automake
sudo apt install autoconf
sudo apt install libtool
sudo apt install wget
sudo apt install curl
sudo apt install git
sudo apt install gcc
sudo apt install libssl-dev
sudo apt install bc
sudo apt install slib
sudo apt install squashfs-tools
sudo apt install android-sdk-libsparse-utils
sudo apt install android-sdk-ext4-utils
sudo apt install jq
sudo apt install cmake
sudo apt install python3-distutils
sudo apt install tclsh
sudo apt install scons
sudo apt install parallel
sudo apt install ssh-client
sudo apt install tree
sudo apt install python3-dev
sudo apt install python3-pip
sudo apt install device-tree-compiler
sudo apt install libssl-dev
sudo apt install ssh
sudo apt install cpio
sudo apt install squashfs-tools
sudo apt install fakeroot
sudo apt install libncurses5
sudo apt install flex
sudo apt install bison
```
*注意：cmake版本最低要求3.16.5*

## 获取SDK
```
git clone -b 'BranchName' git@github.com:sophgo/sophpi.git
cd sophpi
./scripts/repo_clone.sh --gitclone scripts/subtree.xml
```

## 编译
- 以 `cv1812h_wevb_0007a_emmc`为例
```
source build/cvisetup.sh
defconfig cv1812h_wevb_0007a_emmc
build_all
```
- 编译成功后可以在`install`目录下看到生成的image

## SD卡烧录
- 接好EVB板的串口线
- 将SD卡格式化成FAT32格式
- 将`install`目录下的image放入SD卡根目录
```
.
├── boot.emmc
├── cfg.emmc
├── fip.bin
├── fw_payload_uboot.bin
├── rootfs.emmc
└── system.emmc
```
- 将SD卡插入的SD卡槽中
- 将平台重新上电，开机自动进入烧录，烧录过程log如下：
```
Hit any key to stop autoboot:  0
## Resetting to default environment
Start SD downloading...
mmc1 : finished tuning, code:60
465408 bytes read in 11 ms (40.3 MiB/s)
mmc0 : finished tuning, code:27
switch to partitions #1, OK
mmc0(part 1) is current device

MMC write: dev # 0, block # 0, count 2048 ... 2048 blocks written: OK in 17 ms (58.8 MiB/s)

MMC write: dev # 0, block # 2048, count 2048 ... 2048 blocks written: OK in 14 ms (71.4 MiB/s)
Program fip.bin done
mmc0 : finished tuning, code:74
switch to partitions #0, OK
mmc0(part 0) is current device
64 bytes read in 3 ms (20.5 KiB/s)
Header Version:1
2755700 bytes read in 40 ms (65.7 MiB/s)

MMC write: dev # 0, block # 0, count 5383 ... 5383 blocks written: OK in 64 ms (41.1 MiB/s)
64 bytes read in 4 ms (15.6 KiB/s)
Header Version:1
13224 bytes read in 4 ms (3.2 MiB/s)

MMC write: dev # 0, block # 5760, count 26 ... 26 blocks written: OK in 2 ms (6.3 MiB/s)
64 bytes read in 4 ms (15.6 KiB/s)
Header Version:1
11059264 bytes read in 137 ms (77 MiB/s)

MMC write: dev # 0, block # 17664, count 21600 ... 21600 blocks written: OK in 253 ms (41.7 MiB/s)
64 bytes read in 3 ms (20.5 KiB/s)
Header Version:1
4919360 bytes read in 65 ms (72.2 MiB/s)

MMC write: dev # 0, block # 158976, count 9608 ... 9608 blocks written: OK in 110 ms (42.6 MiB/s)
64 bytes read in 4 ms (15.6 KiB/s)
Header Version:1
10203200 bytes read in 128 ms (76 MiB/s)

MMC write: dev # 0, block # 240896, count 19928 ... 19928 blocks written: OK in 228 ms (42.7 MiB/s)
Saving Environment to MMC... Writing to MMC(0)... OK
mars_c906#
```
- 烧录成功，拔掉SD卡，重新给板子上电，进入系统

<br><br>

# 关于算能

**算能致力于成为全球领先的通用算力提供商。<br>
算能专注于AI、RISC-V CPU等算力产品的研发和推广应用，以自研产品为核心打造了覆盖“云、边、端”的全场景应用矩阵 ，为城市大脑、智算中心、智慧安防、智慧交通、安全生产、工业质检、智能终端等应用提供算力产品及整体解决方案 。公司在北京、上海、深圳、青岛、厦门等国内 10 多个城市及美国、新加坡等国家设有研发中心。**
- [官方网站](https://www.sophgo.com/)

# 技术论坛
- [技术讨论 - 开源硬件sophpi](https://developer.sophgo.com/forum/index/25/51.html)


