# Oppo MediaTek（通用）Fastboot解锁——解锁引导加载程序
## 概述
本仓库中的脚本可基于原厂preloader进行修补，将其中的fastboot锁定标识修改为解锁状态。

##⚠️您必须确保您拥有救砖的能力，否则不建议您使用此方案操作，修改preloader是非常危险的行为！
##🚫修改preloader后禁止*ota更新*
##更新系统会替换掉原来的preloader，你的设备很可能将崩溃至preloader vcom端口，甚至更糟：没有任何端口和反应！
##💬有关于preloader刷写的讨论在[酷安帖子](https://www.coolapk.com/feed/69780533?s=YTAyMmFhNzcxMGFhOGJlZzY5OGQzNzQwega1602)中，##刷写preloader应避免刷写*preloader_raw*分区，否则会导致设备*无法启动*

## 操作步骤
1. 下载并安装[Python](https://www.python.org/downloads) **3.4+** 版本
2. 使用
[刷机匣](https://gitee.com/geekflashtool)
或者
[mtkclient](https://github.com/bkerler/mtkclient)
读取你的Oppo设备的预加载器（boot1）镜像文件
3. 将preloader备份文件放到`preloader_path.py`同一文件夹中，且必须命名为`boot1.bin`
4. 双击运行该Python脚本
5. 脚本运行完成后，生成的预加载器文件会存放在preloader_path文件夹中，文件名为`boot1.bin`
6. 使用**mtkclient**或刷机匣将修补好的preloader写入设备
7. 务必在开发者选项中开启**OEM解锁**功能
8. 使用**adb**工具执行命令`adb reboot bootloader`，进入解锁后的fastboot模式
9. 进入fastboot模式后，执行命令`fastboot flashing unlock`
10. 按下音量上键或音量下键确认引导加载程序解锁操作，操作前可查看设备屏幕的解锁提示文字确认操作方式
11. 完成引导加载程序的解锁操作

## 相关示例
以下为补丁制作成功的日志示例：
```
Dev. Max_Goblin - 4pda
boot1.bin 检测状态：成功
Memory type: EMMC_BOOT
标识块检测状态：成功
锁定状态：22（已锁定）
写入零值范围：0x800:0x2000
代码跳转偏移量：0x800 至 0x2000
--------------------
修改BRLYT偏移量
0x20d: 08 -> 20
0x21d: 08 -> 20
0x211: 08 -> 10
0x212: 08 -> 10
0x221: 08 -> 10
0x222: 08 -> 10
--------------------
将标识块写入至：0x1000
Fastboot锁定状态：0x22 -> 00
在路径С:\mtkclient\mtkclient_2.0.1\preloader_path\boot1.bin生成新预加载器
按回车键关闭
```

## 补充说明
俄罗斯4pda论坛的用户Max_Goblin提供了极为详细的[操作教程](https://4pda.to/forum/index.php?showtopic=1059838&view=findpost&p=136154776)，内容包含Windows系统下**mtkclient**的详细安装步骤、设备备份的创建与恢复方法、图形界面的完整使用说明，以及手动制作预加载器补丁的操作指南。
对于中文用户，可以查看此[酷安教程](https://www.coolapk.com/feed/70198121?s=MDM3MGIyOGIxMGFhOGJlZzY5OGQzNGJhega1602)

## 支持设备
| 型号            | 设备代码 | 处理器        | 处理器ID    | 备注                                                         |
|-----------------|----------|---------------|-------------|--------------------------------------------------------------|
| Oppo A17        | CPH2477  | 联发科 Helio G35     | MT6765      | 完全支持                                                      |
| Oppo A17K       | CPH2471  | 联发科 Helio G35     | MT6765      | 完全支持                                                      |
| Oppo A18        | CPH2591  | 联发科 Helio G85     | MT6768/MT6769 | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo A54 4G     | CPH2239  | 联发科 Helio G35     | MT6765      | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo A55 4G     | CPH2325  | 联发科 Helio G35     | MT6765      | 完全支持                                                      |
| Oppo A56 5G     | PFVM110  | 联发科 天玑700 | MT6833      | 完全支持                                                      |
| Oppo A58 4G     | CPH2577  | 联发科 Helio G85     | MT6768/MT6769 | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo A58x       | PHJ110   | 联发科 天玑700 | MT6833      | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo A73 5G     | CPH2161  | 联发科 天玑720 | MT6853      | 支持图形界面，刷机匣资源包已支持             |
| Oppo Reno 10 5g | CPH2531  | 联发科 天玑7050| MT6877V     | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo Reno 11F 5g| CPH2603  | 联发科 天玑7050| MT6877V     | DAA图形界面及命令行存在问题，刷机匣资源包已支持              |
| Oppo Reno 4 Lite| CPH2125  | 联发科 Helio P95     | MT6779      | 完全支持                                                      |
| Oppo Reno 5 Lite| CPH2205  | 联发科 Helio P95     | MT6779      | 完全支持                                                      |
| realme GT Neo   | RMX3031  | 联发科 天玑1200      | MT6893      | 已通过测试                                                    |
| OPPO Reno6 Pro  | PEPM00   | 联发科 天玑1200      | MT6893      | 已通过测试                                                    |
| OPPO K10        | PGJM10   | 联发科 天玑8000-MAX  | MT6895      | 已通过测试              |
| OPPO Find X6    | PGFM10   | 联发科 天玑9200      | MT6985      | 已通过测试                                                    |

4pda论坛提供现成的预加载器文件；DAA相关问题并不代表设备不支持解锁，尤其是在刷机匣资源包已支持的情况下。
*刷机匣中oppo的mtk授权资源包，目前已经支持从天玑700到天玑1300等芯片授权，可以通过资源包尝试进行授权
但是，如果你已经升级了2025年8月安全补丁，那么基本上是无法进行解锁的，da被拉进黑名单了。

## 社区实测
若你通过**mtkclient**和本补丁成功解锁了任意Oppo设备的引导加载程序，可提交issue告知该方法适配的新Oppo设备，建议同时提供原厂preloader和修改后的preloader文件；若该方法未成功，也可进行相关反馈。你也可以通过Telegram与项目作者取得联系。

## 注意事项
1. 解锁操作前，必须在设备开发者选项中开启**OEM解锁**功能，否则无法完成后续fastboot解锁
2. 预加载器的读取和写入操作，均需通过**mtkclient**的图形界面完成
3. 原厂预加载器备份文件需严格命名为`boot1.bin`，并与`preloader_path.py`放置在同一目录，否则脚本无法识别
4. 执行`fastboot flashing unlock`后，需根据设备屏幕的文字提示，按下音量上键或音量下键完成解锁确认
5. DAA相关问题并非Oppo设备解锁的绝对阻碍，多数情况为难以找到有效DA文件，建议尝试各类可用的DA文件和刷机匣授权资源包
6. 写入修改后的预加载器是解锁核心步骤，需确保文件写入过程无中断，避免设备故障

## 许可证说明
本项目采用AGPL-3.0许可证进行授权，详细的授权条款可查阅[LICENSE](LICENSE)文件。

