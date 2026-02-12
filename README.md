
# 联发科平台OPPO/Realme设备Fastboot解锁指南

> **重要提示**：解锁Bootloader会导致手机数据完全丢失，请务必提前备份重要资料。此操作存在风险，可能导致设备失去保修或变砖，请谨慎操作。

## 方案概述

本方案基于俄罗斯4pda论坛用户Max_Goblin的研究，通过修改设备预加载器（preloader）中的fastboot锁定标识实现Bootloader解锁。该方法适用于多种联发科平台的OPPO和Realme机型[1](@ref)。

**核心原理**：提取原厂preloader镜像，修改其中的锁定标志位，然后重新刷入修改后的镜像，使设备进入解锁状态的fastboot模式。

## 准备工作

### 软硬件要求
- **电脑**：Windows 10或更高版本系统
- **手机**：已开启开发者选项和USB调试模式[3,4](@ref)
- **数据线**：质量可靠的USB数据线，建议使用电脑机箱后置USB接口
- **软件依赖**：
  - [Python 3.4+](https://www.python.org/downloads)
  - [刷机匣](https://gitee.com/geekflashtool)（原mtkclient）
  - ADB和Fastboot工具

### 关键设置
在开发者选项中启用以下设置[3,4](@ref)：
- **USB调试**
- **OEM解锁**（如存在）
- **仅充电模式下允许USB调试**（如存在）

## 详细操作步骤

### 第一步：提取原厂preloader
1. 使用**刷机匣**连接设备，确保驱动正常安装
2. 通过工具读取preloader（boot1）分区镜像
3. 将备份的镜像文件保存为`boot1.bin`，置于脚本同目录下

### 第二步：修改preloader镜像
1. 运行提供的Python脚本（`preloader_path.py`）
2. 脚本会自动识别并修改锁定标志位
3. 成功后会生成修改后的preloader文件，保存在`preloader_path`文件夹中

### 第三步：刷入修改后的preloader
1. 使用**刷机匣**将新生成的`boot1.bin`刷入设备
2. 确保刷写过程完整无误

### 第四步：执行解锁命令
1. 通过ADB重启到fastboot模式：

bash

adb reboot bootloader

2. 在fastboot模式下执行解锁命令：

bash

fastboot flashing unlock

3. 根据设备屏幕提示，使用音量键选择确认解锁，电源键确认

### 第五步：验证解锁状态
部分机型可查询解锁状态[1](@ref)：

bash

fastboot getvar unlocked

如显示`unlocked: yes`则表示解锁成功。

## 补丁制作日志示例

成功运行脚本后，将看到类似输出：

Dev. Max_Goblin - 4pda

boot1.bin found state: successfully

Memory type: UFS_BOOT

Flag block find state: successfully

lock state: 22 (lock)

Write range zeros: 0x1000:0x2000

Jupm offset code: 0x1000 to 0x2000

0x20d: 10 -> 20

0x21d: 10 -> 20

0x211: 10 -> 10

0x212: 04 -> 10

0x221: 10 -> 10

0x222: 04 -> 10

Write flag block to: 0x1000

Fastboot lock state: 0x22 -> 00

Create new preloader to: С:\刷机匣\刷机匣_2.0.1\preloader_path\boot1.bin

Press Enter to close


## 支持设备列表

| 机型 | 设备代码 | 处理器 | 处理器ID | 支持状态 |
|------|----------|--------|----------|----------|
| Oppo A17 | CPH2477 | 曦力G35 | MT6765 | 完全支持 |
| Oppo A17K | CPH2471 | 曦力G35 | MT6765 | 完全支持 |
| Oppo A18 | CPH2591 | 曦力G85 | MT6768/MT6769 | 刷机匣资源包支持 |
| Oppo A54 4G | CPH2239 | 曦力G35 | MT6765 | 刷机匣资源包支持 |
| Oppo A55 4G | CPH2325 | 曦力G35 | MT6765 | 完全支持 |
| Oppo A56 5G | PFVM110 | 天玑700 | MT6833 | 完全支持 |
| Oppo A58 4G | CPH2577 | 曦力G85 | MT6768/MT6769 | 刷机匣资源包支持 |
| Oppo A58x/A58 5G | PHJ110 | 天玑700 | MT6833 | 封DA前测试通过 |
| Oppo A73 5G | CPH2161 | 天玑720 | MT6853 | 刷机匣资源包支持 |
| Oppo Reno 10 5g | CPH2531 | 天玑7050 | MT6877V | 刷机匣资源包支持 |
| Oppo Reno 11F 5g | CPH2603 | 天玑7050 | MT6877V | 刷机匣资源包支持 |
| Oppo Reno 4 Lite | CPH2125 | 曦力P95 | MT6779 | 完全支持 |
| Oppo Reno 5 Lite | CPH2205 | 曦力P95 | MT6779 | 完全支持 |

### 社区实测成功机型
以下为社区用户反馈的成功案例[1](@ref)：
- **realme GT Neo** (RMX3031, 天玑1200, MT6893)
- **OPPO Reno6 Pro** (PEPM00, 天玑1200, MT6893) 
- **OPPO K10** (PGJM10, 天玑8000-MAX, MT6895) - 封DA后进BROM仍可解锁
- **OPPO Find X6** (PGFM10, 天玑9200, MT6985)

## 注意事项与故障排除

### 系统版本警告
OPPO在**2025年8月**的系统更新中引入了新的DA（Download Agent）验证机制[1](@ref)，导致旧版解锁方法失效。建议：
- 避免升级到2025年8月后的系统版本
- 如已升级，尝试降级到早期版本
- 关注社区等待新的破解方案

### 常见问题解决
1. **设备无法进入9008模式**：尝试不同的按键组合，或使用9008工程线[1](@ref)
2. **刷写过程中断**：重新进入9008模式再试，避免直接重试[1](@ref)
3. **fastboot模式黑屏/花屏**：通过设备管理器确认连接状态，而非依赖屏幕显示[1](@ref)
4. **解锁命令无效**：确保从正常fastboot模式而非崩溃进入的模式操作[1](@ref)

### 备份重要性
强烈建议在操作前使用**刷机匣**备份全分区[1](@ref)，包括：
- 系统分区镜像
- 基带和IMEI相关分区
- OCDT等设备特定分区

备份文件仅适用于本设备，切勿用于其他设备。

## 补充资源

- **详细图文教程**：[4pda论坛教程](https://4pda.to/forum/index.php?showtopic=1059838&view=findpost&p=136154776)
- **社区支持**：建议加入相关刷机社区获取最新动态和帮助
- **更新追踪**：关注DA验证机制更新情况，及时调整方案

---

*最后更新：2026年2月12日 | 本教程仅供参考，操作风险自负[1,3,4](@ref)*
