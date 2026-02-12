解锁Fastboot——联发科版OPPO通用Bootloader解锁教程
 
#
 
本仓库脚本可基于原厂预加载器制作修改版文件，将其中的fastboot锁定标识修改为解锁状态。
 
#
 
## 操作步骤
 
1. 下载并安装Python 3.4及以上版本（下载地址：https://www.python.org/downloads）
 
2. 使用刷机匣（官网地址：https://gitee.com/geekflashtool）及其图形界面，从OPPO设备中读取预加载器（boot1）镜像文件
 
3. 将备份的预加载器文件放入 preloader_path.py 脚本同目录，并重命名为 boot1.bin 
 
4. 双击运行该Python脚本
 
5. 脚本运行完成后，修改后的预加载器文件会生成在 preloader_path 文件夹中，文件名为 boot1.bin 
 
6. 继续使用刷机匣及其图形界面，将生成的预加载器文件刷入设备
 
7. 务必在手机开发者选项中开启OEM解锁功能
 
8. 打开adb工具，输入命令 adb reboot bootloader ，进入解锁后的fastboot模式
 
9. 进入fastboot模式后，输入命令 fastboot flashing unlock 
 
10. 按下手机音量上键/音量下键确认Bootloader解锁，操作前请仔细查看设备屏幕的解锁提示文字
 
11. 完成以上步骤，即可完成Bootloader解锁操作
 
#
 
## 相关示例
 
### 补丁制作成功的日志示例
 
```
 
Dev. Max_Goblin - 4pda
 
boot1.bin found state: successfully
 
Memory type: EMMC_BOOT
 
Flag block find state: successfully
 
lock state: 22 (lock)
 
Write range zeros: 0x800:0x2000
 
Jump offset code: 0x800 to 0x2000
 
Change BRLYT offset
 
0x20d: 08 -> 20
 
0x21d: 08 -> 20
 
0x211: 08 -> 10
 
0x212: 08 -> 10
 
0x221: 08 -> 10
 
0x222: 08 -> 10
 
Write flag block to: 0x1000
 
Fastboot lock state: 0x22 -> 00
 
Create new preloader to: С:\mtkclient\mtkclient_2.0.1\preloader_path\boot1.bin
 
Press Enter to close
 
```
 
#
 
## 补充说明
 
俄罗斯4pda论坛用户Max_Goblin发布了超详细操作教程（地址：https://4pda.to/forum/index.php?showtopic=1059838&view=findpost&p=136154776），包含Windows系统下刷机匣完整安装、备份创建与恢复、图形界面详细使用、手动制作预加载器补丁的全流程指引。
 
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
 
| 机型            | 设备代码 | 处理器        | 处理器ID  | 备注       |
 
|-----------------|----------|---------------|-----------|------------|
 
| realme GT Neo   | RMX3031  | 天玑1200      | MT6893    | 已通过测试 |
 
| OPPO Reno6 Pro  | PEPM00   | 天玑1200      | MT6893    | 已通过测试 |
 
| OPPO K10        | PGJM10   | 天玑8000-MAX  | MT6895    | 已通过测试 |
 
| OPPO Find X6    | PGFM10   | 天玑9200      | MT6985    | 已通过测试 |
 
#
 
## 注意事项
 
1. 预编译预加载器：4pda论坛上提供了一些机型的预编译预加载器文件，可直接下载使用
 
2. DAA问题说明：存在DAA问题并不一定意味着无法解锁，特别是如果auth_sv5.auth尚未测试；对于OPPO设备，通常只是难以找到有效的DA文件，但仍建议尝试
 
3. 设备反馈：如果您使用刷机匣和此补丁成功解锁了任何OPPO设备的bootloader，请创建issue告知适用机型，最好提供原厂预加载器和修改后的预加载器文件
 
4. 系统更新警告：OPPO在2025年8月更新后加入新一轮DA补丁，之前的授权将失效，建议不要更新系统，如已更新请尝试降级
 
#
 
## 许可证说明
 
本项目采用AGPL-3.0许可证，详细条款见项目内 LICENSE 文件。
 
以上内容可直接复制保存为  OPPO_MTK_Bootloader_Unlock.md  文件，所有格式符合Markdown规范，支持直接在markdown阅读器中打开查看，表格、代码块均可正常显示。
