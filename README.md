# 解锁Fastboot——联发科版OPPO通用Bootloader解锁教程

本仓库中的脚本可基于原厂**preloader（预加载器）**制作修改版文件，将其中的fastboot锁定标识修改为解锁状态。

操作步骤
●下载并安装Python 3.4及以上版本
●使用mtkclient及其图形界面，从你的OPPO设备中读取preloader（boot1）镜像文件
●将备份的preloader文件放入preloader_path.py脚本同目录下，确保重命名为boot1.bin
●双击运行该Python脚本
●脚本运行完成后，修改后的preloader文件会生成在preloader_path文件夹中，文件名为boot1.bin
●仍使用mtkclient及其图形界面，将生成的preloader文件刷入设备
●务必在开发者选项中开启OEM解锁功能
●打开adb工具，输入adb reboot bootloader命令进入解锁后的fastboot模式
●进入fastboot模式后，输入fastboot flashing unlock命令
●按下音量上键或音量下键确认Bootloader解锁，建议清晰查看解锁请求后设备屏幕上的提示文字再操作
●完成以上步骤，即可结束Bootloader解锁的操作流程

补丁制作成功的日志示例
Dev. Max_Goblin - 4pda
boot1.bin found state: successfully
Memory type: EMMC_BOOT
Flag block find state: successfully
lock state: 22 (lock)
Write range zeros: 0x800:0x2000
Jump offset code: 0x800 to 0x2000
--------------------
Change BRLYT offset
0x20d: 08 -> 20
0x21d: 08 -> 20
0x211: 08 -> 10
0x212: 08 -> 10
0x221: 08 -> 10
0x222: 08 -> 10
--------------------
Write flag block to: 0x1000
Fastboot lock state: 0x22 -> 00
Create new preloader to: С:\mtkclient\mtkclient_2.0.1\preloader_path\boot1.bin
Press Enter to close

补充说明
俄罗斯4pda论坛的用户Max_Goblin发布了超详细的操作教程，内容包含Windows系统下mtkclient的完整安装步骤、备份的创建与恢复、图形界面的详细使用方法，以及手动制作preloader补丁的操作指引。

支持设备信息
机型	设备代码	处理器	处理器ID	支持状态
Oppo A17	CPH2477	Helio G35	MT6765	完全支持
Oppo A17K	CPH2471	Helio G35	MT6765	完全支持
Oppo A18	CPH2591	Helio G85	MT6768/MT6769	GUI和命令行存在DAA问题，已测试auth_sv5.auth认证文件
Oppo A54 4G	CPH2239	Helio G35	MT6765	GUI和命令行存在DAA问题，auth_sv5.auth未测试
Oppo A55 4G	CPH2325	Helio G35	MT6765	完全支持
Oppo A56 5G	PFVM110	天玑700	MT6833	完全支持
Oppo A58 4G	CPH2577	Helio G85	MT6768/MT6769	GUI和命令行存在DAA问题，auth_sv5.auth未测试
Oppo A58x	PHJ110	天玑700	MT6833	GUI和命令行存在DAA问题，auth_sv5.auth已测试
Oppo A73 5G	CPH2161	天玑720	MT6853	支持图形界面，无图形界面需搭配auth_sv5.auth认证文件
Oppo Reno 10 5g	CPH2531	天玑7050	MT6877V	GUI和命令行存在DAA问题，auth_sv5.auth未测试
Oppo Reno 11F 5g	CPH2603	天玑7050	MT6877V	GUI和命令行存在DAA问题，auth_sv5.auth未测试
Oppo Reno 4 Lite	CPH2125	Helio P95	MT6779	完全支持
Oppo Reno 5 Lite	CPH2205	Helio P95	MT6779	完全支持

社区实测成功机型
机型	设备代码	处理器	处理器ID	备注
realme GT Neo	RMX3031	天玑1200	MT6893	已通过测试
OPPO Reno6 Pro	PEPM00	天玑1200	MT6893	已通过测试
OPPO K10	PGJM10	天玑8000-MAX	MT6895	已通过测试（实测），封DA后进BROM仍可解锁fastboot
OPPO Find X6	PGFM10	天玑9200	MT6985	已通过测试

重要说明
●预编译preloader：4pda论坛上提供了一些机型的预编译preloader文件
●DAA问题说明：存在DAA问题并不一定意味着无法解锁，特别是如果auth_sv5.auth尚未测试。对于OPPO设备，通常只是难以找到有效的DA文件，但仍建议尝试。刷机匣可能有相关的资源包支持，可优先尝试使用刷机匣进行联机，或者使用UN工具、潘多拉、奇美拉等其他工具进行尝试
●设备反馈：如果您使用mtkclient和此补丁成功解锁了任何OPPO设备的bootloader，请创建issue告知我们该方法适用于哪些新OPPO设备，最好能提供原厂preloader和修改后的preloader。您也可以通过Telegram联系我
●系统更新警告：OPPO在2025年8月更新后加入新一轮DA补丁，之前的授权将失效，建议不要更新系统，如已更新请尝试降级
许可证
本项目采用AGPL-3.0许可证。详见LICENSE文件。

（注：文档部分内容可能由 AI 生成）


