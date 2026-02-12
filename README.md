解锁Fastboot——联发科版OPPO通用Bootloader解锁教程
 
#
 
本仓库脚本可基于原厂preloader（预加载器）制作修改版文件，将其中的fastboot锁定标识修改为解锁状态。
 
#
 
## 操作步骤
 
1. 下载并安装Python 3.4及以上版本（下载地址：https://www.python.org/downloads）
 
2. 使用mtkclient（下载地址：https://github.com/bkerler/mtkclient）及其图形界面，从OPPO设备中读取preloader（boot1）镜像文件
 
3. 将备份的preloader文件放入 preloader_path.py 脚本同目录，并重命名为 boot1.bin 
 
4. 双击运行该Python脚本
 
5. 脚本运行完成后，修改后的preloader文件会生成在 preloader_path 文件夹中，文件名为 boot1.bin 
 
6. 继续使用mtkclient及其图形界面，将生成的preloader文件刷入设备
 
7. 务必在手机开发者选项中开启OEM解锁功能
 
8. 打开adb工具，输入命令 adb reboot bootloader ，进入解锁后的fastboot模式
 
9. 进入fastboot模式后，输入命令 fastboot flashing unlock 
 
10. 按下手机音量上键/音量下键确认Bootloader解锁，操作前请仔细查看设备屏幕的解锁提示文字
 
11. 完成以上步骤，即可完成Bootloader解锁操作
 
#
 
## 补丁制作成功的日志示例
 
```
 
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
 
```
 
#
 
## 补充说明
 
俄罗斯4pda论坛用户Max_Goblin发布了超详细操作教程（地址：https://4pda.to/forum/index.php?showtopic=1059838&view=findpost&p=136154776），包含Windows系统下mtkclient完整安装、备份创建与恢复、图形界面详细使用、手动制作preloader补丁的全流程指引。
 
#
 
## 支持设备信息
 
| 机型            | 设备代码 | 处理器      | 处理器ID      | 支持状态                                                   |
 
|-----------------|----------|-------------|---------------|------------------------------------------------------------|
 
| Oppo A17        | CPH2477  | Helio G35   | MT6765        | 完全支持                                                   |
 
| Oppo A17K       | CPH2471  | Helio G35   | MT6765        | 完全支持                                                   |
 
| Oppo A18        | CPH2591  | Helio G85   | MT6768/MT6769 | GUI和命令行存在DAA问题，auth_sv5.auth已测试                |
 
| Oppo A54 4G     | CPH2239  | Helio G35   | MT6765        | GUI和命令行存在DAA问题，auth_sv5.auth未测试                |
 
| Oppo A55 4G     | CPH2325  | Helio G35   | MT6765        | 完全支持                                                   |
 
| Oppo A56 5G     | PFVM110  | 天玑700     | MT6833        | 完全支持                                                   |
 
| Oppo A58 4G     | CPH2577  | Helio G85   | MT6768/MT6769 | GUI和命令行存在DAA问题，auth_sv5.auth未测试                |
 
| Oppo A58x       | PHJ110   | 天玑700     | MT6833        | GUI和命令行存在DAA问题，auth_sv5.auth已测试                |
 
| Oppo A73 5G     | CPH2161  | 天玑720     | MT6853        | 支持图形界面，无图形界面需搭配auth_sv5.auth使用            |
 
| Oppo Reno 10 5G | CPH2531  | 天玑7050    | MT6877V       | GUI和命令行存在DAA问题，auth_sv5.auth未测试                |
 
| Oppo Reno 11F 5G| CPH2603  | 天玑7050    | MT6877V       | GUI和命令行存在DAA问题，auth_sv5.auth未测试                |
 
| Oppo Reno 4 Lite| CPH2125  | Helio P95   | MT6779        | 完全支持                                                   |
 
| Oppo Reno 5 Lite| CPH2205  | Helio P95   | MT6779        | 完全支持                                                   |
 
#
 
## 社区实测成功机型
 
| 机型            | 设备代码 | 处理器      | 处理器ID      | 备注                                                       |
 
|-----------------|----------|-------------|---------------|------------------------------------------------------------|
 
| realme GT Neo   | RMX3031  | 天玑1200    | MT6893        | 已通过测试                                                 |
 
| OPPO Reno6 Pro  | PEPM00   | 天玑1200    | MT6893        | 已通过测试                                                 |
 
| OPPO K10        | PGJM10   | 天玑8000-MAX| MT6895        | 实测通过，封DA后进BROM仍可解锁fastboot                     |
 
| OPPO Find X6    | PGFM10   | 天玑9200    | MT6985        | 已通过测试                                                 |
 
#
 
## 注意事项
 
1. 4pda论坛提供部分机型的预编译preloader文件，可直接下载使用
 
2. 设备存在DAA问题不代表无法解锁，尤其是auth_sv5.auth未测试的机型；OPPO设备通常是难以找到有效DA文件，建议优先尝试
 
3. 可优先尝试刷机匣联机，或使用UN工具、潘多拉、奇美拉等工具辅助操作
 
4. 若使用本方法成功解锁其他OPPO设备，可通过创建issue反馈（建议提供原厂/修改后preloader文件），也可通过Telegram联系作者
 
#
 
## 许可证说明
 
本项目采用AGPL-3.0开源许可证，详细条款见项目内 LICENSE 文件。
