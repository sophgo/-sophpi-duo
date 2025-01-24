# 快速入门指南

## V410 SDK 编译步骤

### 获取源码

步骤一:

``` bash
mkdir -p <WORKSPACE>
cd <WORKSPACE>
git clone -b sg200x-evb git@github.com:sophgo/sophpi.git
cd sophpi
./scripts/repo_clone.sh --gitclone scripts/subtree.xml
```

步骤二:

``` bash
source build/envsetup_soc.sh
defconfig sg2002_wevb_riscv64_sd
clean_all
build_all
```

## V420 SDK 编译步骤

### 获取源码

步骤一:

``` bash
mkdir -p <WORKSPACE>
cd <WORKSPACE>
git clone -b sg200x-evb git@github.com:sophgo/sophpi.git
cd sophpi
./scripts/repo_clone.sh --gitclone scripts/subtree_cv18xx-v4.2.x.xml
```

步骤二:

``` bash
source build/envsetup_soc.sh
defconfig cv180zb_wevb_0008a_spinor
clean_all
build_all
```

# NOTE.

TODO

# 修订记录

## V410 SDK 修订记录

| 版本号  | 版本日期  | 版本更新内容                                      |
| ------ | --------- | ------------------------------------------------ |
| v4.1.6 | 2024.04.19 | TODO                                             |
| v4.1.6.1 | 2025.01.24 | tdl_sdk: 新增CVI_TDL_Set_ROI接口及yolov8模型<br>SensorSupportList: 修改gc2053_1l & gc2053_slave 的时钟模式|

## V420 SDK 修订记录

| 版本号  | 版本日期  | 版本更新内容                                      |
| ------ | --------- | ------------------------------------------------ |
| v4.2.6 | 2024.04.19 | TODO                                             |