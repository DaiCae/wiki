# ESXI 直通 NVIDIA 显卡

## 设置 ESXI:

- 选择要直通的显卡 设置切换直通
- 重新引导 ESXI 主机以应用设置

## 设置虚拟机:

- 添加 PCI 设备 => 选择显卡设备
- 预留所有主机内存
- 虚拟机选项 => 高级 => 编辑配置
- 添加 hypervisor.cpuid.v0 = FALSE
