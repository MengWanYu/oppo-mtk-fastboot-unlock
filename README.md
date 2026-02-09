用户：
需要
豆包：
# 解锁Fastboot——联发科版OPPO通用Bootloader解锁教程
本仓库中的脚本可基于原厂**preloader（预加载器）**制作修改版文件，将其中的fastboot锁定标识修改为解锁状态。
---
## 操作步骤
* 下载并安装[Python](https://www.python.org/downloads) 3.4及以上版本
* 使用[mtkclient](https://github.com/bkerler/mtkclient)及其图形界面，从你的OPPO设备中读取preloader（boot1）镜像文件
* 将备份的preloader文件放入preloader_path.py脚本同目录下，确保重命名为boot1.bin
* 双击运行该Python脚本
* 脚本运行完成后，修改后的preloader文件会生成在preloader_path文件夹中，文件名为boot1.bin
* 仍使用mtkclient及其图形界面，将生成的preloader文件刷入设备
* 务必在开发者选项中开启**OEM解锁**功能
* 打开adb工具，输入`adb reboot bootloader`命令进入解锁后的fastboot模式
* 进入fastboot模式后，输入`fastboot flashing unlock`命令
* 按下音量上键或音量下键确认Bootloader解锁，建议清晰查看解锁请求后设备屏幕上的提示文字再操作
* 完成以上步骤，即可结束Bootloader解锁的操作流程
---
## 补丁制作成功的日志示例
```
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
Create new preloader to: С:\mtkclient\mtkclient_2.0.1\preloader_path\boot1.bin
Press Enter to close
```
## 补充说明
俄罗斯4pda论坛的用户Max_Goblin发布了超详细的[操作教程](https://4pda.to/forum/index.php?showtopic=1059838&view=findpost&p=136154776)，内容包含Windows系统下mtkclient的完整安装步骤、备份的创建与恢复、图形界面的详细使用方法，以及手动制作preloader补丁的操作指引。
---
## 支持设备信息
| 机型               | 设备代码       | 处理器            | 处理器ID          | 支持状态                                                      |
|--------------------|----------------|-------------------|-------------------|---------------------------------------------------------------|
| Oppo A17           | CPH2477        | 曦力G35           | MT6765            | 完全支持                                                      |
| Oppo A17K          | CPH2471        | 曦力G35           | MT6765            | 完全支持                                                      |
| Oppo A18           | CPH2591        | 曦力G85           | MT6768/MT6769     | 图形界面及命令行存在DAA问题，已测试auth_sv5.auth认证文件       |
| Oppo A54 4G        | CPH2239        | 曦力G35           | MT6765            | 图形界面及命令行存在DAA问题，未测试auth_sv5.auth认证文件       |
| Oppo A55 4G        | CPH2325        | 曦力G35           | MT6765            | 完全支持                                                      |
| Oppo A56 5G        | PFVM110        | 天玑700           | MT6833            | 完全支持                                                      |
| Oppo A58 4G        | CPH2577        | 曦力G85           | MT6768/MT6769     | 图形界面及命令行存在DAA问题，未测试auth_sv5.auth认证文件       |
| Oppo A58x          | PHJ110         | 天玑700           | MT6833            | 图形界面及命令行存在DAA问题，已测试auth_sv5.auth认证文件       |
| Oppo A73 5G        | CPH2161        | 天玑720           | MT6853            | 支持图形界面，无图形界面使用需搭配auth_sv5.auth认证文件        |
| Oppo Reno 10 5g    | CPH2531        | 天玑7050          | MT6877V           | 图形界面及命令行存在DAA问题，未测试auth_sv5.auth认证文件       |
| Oppo Reno 11F 5g   | CPH2603        | 天玑7050          | MT6877V           | 图形界面及命令行存在DAA问题，未测试auth_sv5.auth认证文件       |
| Oppo Reno 4 Lite   | CPH2125        | 曦力P95           | MT6779            | 完全支持                                                      |
| Oppo Reno 5 Lite   | CPH2205        | 曦力P95           | MT6779            | 完全支持                                                      |

#### 4pda论坛提供现成的preloader修改文件
#### 存在DAA问题并不代表设备不支持解锁，尤其是未测试auth_sv5.auth认证文件的机型。对于OPPO设备而言，这类问题通常只是因难以找到可用的DA文件导致，建议尝试操作。
#### 若你通过mtkclient工具和本补丁成功解锁了任意OPPO设备的Bootloader，欢迎提交issue反馈，告知该方法支持的新机型，若能提供原厂preloader文件和修改后的文件更佳；若该方法未生效，也可进行反馈。你也可以通过电报与我联系。
---
## 协议说明
本项目基于AGPL-3.0协议授权，详细条款请参阅[LICENSE](LICENSE)文件。

内容由 AI 生成
