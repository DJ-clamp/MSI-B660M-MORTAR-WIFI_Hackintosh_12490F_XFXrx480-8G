# [👀️] 安装引导前的注意事项

我当前的BIOS版本是```7D43v17``` (PS.更新过了最新的BIOS `7D43v1D`后依然可用 )在经历了卡在```EB|LOG:EXITBS:START```的无数次试验后发现只有当把 Booter -> Quirks -> SetupVirtualMap 设置为 true 时启动通过
更多信息请查阅这篇[`issue贴文`](https://github.com/laggykiller/Hackintosh_MSI_B660M-A_WIFI_DDR4/issues/1#issuecomment-1251633487)

Notice：

2023-08-15 目前可以启动MacOS 13 暂时未验证是否能直接引导Windows和Linux 

CPU 12490F在使用了[`CPUFriend`](https://github.com/acidanthera/CPUFriend) kext插件在macOS下生成`CPUFriendDataProvider` 后睿频正常，暂时不清楚如果这个插件是否可以直接给别人的电脑来用。

我把`SecureBootModel`选项设置为`Disabled`,暂时不清楚如果设置Auto之后是否能够引导安装，按照一篇在Github大师的[`readme文件`](https://github.com/laggykiller/Hackintosh_MSI_B660M-A_WIFI_DDR4#5-post-install)的理解,以及OpenCore中Post-install对于[Apple secureboot model](https://dortania.github.io/OpenCore-Post-Install/universal/security/applesecureboot.html)的文档说明。
我所选择的MacPro7,1 (December 2019) 可以设置为 `j160` 启动，待验证。

# [🚀️] 配置

| 配置 | 型号 |
| --- | --- |
| CPU | [Intel i5 12490F](https://ark.intel.com/content/www/cn/zh/ark/products/134588/intel-core-i512490f-processor-20m-cache-up-to-4-60-ghz.html) |
| 主板 | [微星MAG B660M MORTAR DDR4](https://cn.msi.com/Motherboard/MAG-B660M-MORTAR-DDR4) |
| 显卡 | XFX RX480 8G 黑狼进化版 -> 刷 华硕 ASUS RX480 8G BIOS |
| 内存 | ADATA 威刚 XPG D35G 灯条 DDR4 3200 16Gx2 |
| 网卡 | Realtek® 8125BG 2.5G LAN + Intel® Wi-Fi 6E AX211 |
| 硬盘 | 长江储存芯片方案的 2T M.2 PCIE4.0 |
| OC版本 | 0.9.3 |
| macOS | macOS Ventura 13.2.1 (22D68) |
| 机型 | MacPro7,1 |
| BIOS | 7D43v17 |

# [💻] 设置
| 选项 | 状态 |
| --- | --- |
| D.T.M | enable |
| Secure Boot | disable |
| *SR-IOV (但是建议试下开启后的是否有bug，个人认为这个还是很有用的) | disable |
| Erp Ready | disable |

说明: 如果你已经把主板BIOS升级到了`7D43v17`或者更高的版本，
现在只需要设置两项参数即可实现黑苹果启动：设置`D.T.M ->Enable`和 `Secure Boot -> Disabled` 非常简单。
ref. MSI website. D.T.M 是叫做 disable title message 的东西 开启这项会自动把所有要屏蔽的信息显示出来，包括了fast boot disable，cfg-lock disable etc., 在开启保存时候会提示出来哪些发生了变更，哪里有具体的设置信息.

# [📕] 更新记录

2023-08-14

目前所有的核心和插件都是DEBUG模式，等待测试完成后转为Release
* 尝试引导 成功
* 尝试睿频 12490F 成功
* 尝试蓝牙连接magic keyboard 成功
* 尝试WIFI搜索与连接 成功
* 免驱显卡驱动 成功
* USB我自己生成的有问题，发现的状况是前面板只有USB2.0设备可以使用，TYPE-C和3.0均无法加载，后面板USB3.0一切正常
看说明是需要对USB设备进行Mapping，具体的使用可以看[`这篇文章`](https://github.com/yzchan/MSI-MAG-B660M-MORTAR-DDR4-12600K-EFI/blob/master/USB%E5%AE%9A%E5%88%B6.md)

2023-08-16
尝试去修复SMBUS的问题，采用了SSDT-SBUS-MCHC.dsl opencore文档的方式进行修复，在查询到PCI驱动的同时发现以下问题。
```txt
kextstat | grep -E "AppleSMBusController|AppleSMBusPCI"
Executing: /usr/bin/kmutil showloaded
No variant specified, falling back to release
  155    0 0xffffff7f95df9000 0x1000     0x1000     com.apple.driver.AppleSMBusPCI (1.0.14d1) 3B3CBC6F-07BD-3D7E-9F2F-D738A31C290D <17 7 6 3>
  178    1 0xffffff7f95ded000 0x6ffd     0x6ffd     com.apple.driver.AppleSMBusController (1.0.18d1) 18305D5D-1310-37BC-B654-6C034FD346E7 <177 17 16 7 6 3>
```
这个`No variant specified, falling back to release`，我

# [🎨] TODO 接下来的准备

## 1. 神光同步实现 
对于现代主流主板来说ARGB同步控制器都是基于内建在主板的USB port上
具体通过[USBToolBox工具](https://github.com/USBToolBox/tool/releases)可查询到`MYSTIC LIGHT`这是一个内建在主板的USB1.1设备，专门用来调整灯效的。

```
Intel(R) USB 3.20 可扩展主机控制器 - 1.20 (Microsoft) | USB 3.0 (XHCI) | 25 ports
  Port 1 | USB 2.0 | Type C - with switch (guessed)
  Port 2 | USB 2.0 | Internal (guessed)
    - MYSTIC LIGHT - operating at USB 1.1
```
软件方面有一个现成的方案[OpenRGB](https://openrgb.org/) 支持三大主流平台

## 2. 主板功能
* 睡眠 唤醒 成功
* 节能四项 `目前只实现了三项`
* 长按关机出现电源选项 未实现