# PVE SATA 控制器直通

## 直通准备

`vim /etc/default/grub`

```shell title='/etc/default/grub'
GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt video=efifb:off pcie_acs_override=downstream,multifunction"
```

配置生效 `update-grub`

## 直通配置

查找设备

```shell
lspci -nn | grep -i sata
# 02:00.1 SATA controller [0106]: Advanced Micro Devices, Inc. [AMD] 500 Series Chipset SATA Controller [1022:43eb]
# 39:00.0 SATA controller [0106]: ASMedia Technology Inc. ASM1166 Serial ATA Controller [1b21:1166] (rev 02)
```

添加设备 `vim /etc/modprobe.d/vfio.conf`

```shell title="/etc/modprobe.d/vfio.conf"
options vfio-pci ids=1b21:1166
```

屏蔽驱动

```shell
echo "blacklist ahci" > /etc/modprobe.d/blacklist-ahci.conf
```

更新生效

```shell
update-initramfs -u
reboot
```

## 检查状态

`lspci -nnk -s 39:00.0`

## 注意

ACS Override 为实验性功能，存在一定 DMA 风险。
