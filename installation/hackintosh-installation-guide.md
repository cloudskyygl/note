本文基于 RehabMan 教程

https://github.com/RehabMan/OS-X-Clover-Laptop-Config

# ssdtPRGen.sh

# DSDT

[gfx0] Disable/Enable on \_WAK/\_PTS (DSDT)

# 识别只用于保存数据的机械硬盘

从其他来源的 `config.plist` 发现的，可能只对我的笔记本电脑起作用，作为临时的解决办法

添加键 `config.plist/SMBIOS/Mobile` 并将值设为 `no`

# Wi-Fi - AR9285

安装从 macOS High sierra 13.6 S/L/E 中提取的 IO80211Family.kext

安装位置为 /S/L/E

需要修改 IO80211Family.kext/Contents/PlugIns/AirPortAtheros40.kext/Contents/Info.plist

在 IOKitPersonalities/Atheros Wireless LAN PCI/IONameMatch/`pci168c,2a` 下添加 `pci168c,2b`

在终端安装

```
$ sudo cp -R IO80211Family.kext /S/L/E
$ sudo kext -i /
```

# Audio - ALC269

* 安装 acidanthera/AppleALC.kext 到 /L/E

* `config.plist/Devices/Audio/Inject` 设为 `28`

* `config.plist/Devices/Properties/PciRoot(0x0)/Pci(0x1b,0x0)/layout-id` 取消注释并设为 `28`

* 启用 `config.plist/ACPI/DSDT/Fixes/FixHPET`

* 安装 Rehabman 的 CodecCommander.kext 解决睡眠唤醒后无声的问题

# CPUFriend

https://github.com/acidanthera/CPUFriend/blob/master/Instructions.md

https://github.com/Piker-Alpha/ssdtPRGen.sh

# GPU

acidanthera/WhateverGreen

https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.cn.md

# SSD Trim

应用 https://github.com/RehabMan/OS-X-Clover-Laptop-Config/blob/master/config_patches.plist 中的 **Trim** 补丁


# References

https://www.insanelymac.com/forum/topic/339012-e3-1225v2%E2%86%92p4000-10144drive-failed-and-turbo-boost-bad/
