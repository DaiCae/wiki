---
title: Windows 基本设置优化
description: 
published: true
date: 2023-02-01T14:58:47.296Z
tags: windows
editor: markdown
dateCreated: 2022-11-20T13:14:39.742Z
---

## 设置用户默认权限为管理员

1. 打开本地安全策略 (需要专业版系统) 
* WIN + R 键运行 `secpol.msc`

2. 在本地安全策略中设置属性值 

```shell
安全设置 -> 本地策略 -> 安全选项 -> 用户帐户控制：以管理员批准模式运行所有管理员 -> 已禁用
```
3. 重启系统

## Win10专业版系统激活

* 管理员身份运行CMD

```bash
# 卸载旧的密钥
slmgr.vbs /upk
# 安装新的专业版密钥
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
# 设置激活服务器
slmgr /skms kms.yuxuan.work
# 激活系统
slmgr /ato
```
## 设置开发环境

* 通过winget包管理器一键配置

```bash
# java8
winget install BellSoft.LibericaJDK.8
# python3.9
winget install Python.Python.3.9
# git
winget install Git.Git
# vim (需要手动配置环境变量)
winget install vim.vim
```

## 开启休眠选项
```shell
控制面板-> 硬件和声音-> 电源选项-> 选择电源按钮的功能 -> 更改当前不可用的设置
```
* 勾选`休眠选项`

## win下配置curl和wget

* 设置powershell profile删除系统自带别名

```bash
# C:\Windows\System32\WindowsPowerShell\v1.0
del alias:curl
del alias:wget
```
* 通过winget安装curl和wget

```bash
winget install cURL.cURL
winget install JernejSimoncic.Wget
```