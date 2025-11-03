# PVE NVIDIA 显卡直通

## 直通准备

`vim /etc/default/grub`

```shell title='/etc/default/grub'
GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt video=efifb:off pcie_acs_override=downstream,multifunction"
```

配置生效 `update-grub`

## 直通配置

查找设备

```shell
lspci -nn | grep -i nvidia
# 3d:00.0 VGA compatible controller [0300]: NVIDIA Corporation GP104 [GeForce GTX 1070] [10de:1b81] (rev a1)
# 3d:00.1 Audio device [0403]: NVIDIA Corporation GP104 High Definition Audio Controller [10de:10f0] (rev a1)
```

添加设备 `vim /etc/modprobe.d/vfio.conf`

```shell title="/etc/modprobe.d/vfio.conf"
options vfio-pci ids=10de:2484,10de:228b
```

屏蔽驱动

```shell
echo "blacklist nouveau" > /etc/modprobe.d/blacklist-nouveau.conf
echo "options nvidia-drm modeset=0" >> /etc/modprobe.d/blacklist-nouveau.conf
```

更新生效

```shell
update-initramfs -u
reboot
```

## 检查状态

`lspci -nnk -s 3d:00.0`

## 注意

ACS Override 为实验性功能，存在一定 DMA 风险。
