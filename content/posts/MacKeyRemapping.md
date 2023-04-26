---
title: "在macOS上修改外接键盘的按键映射并设置开机自动修改"
date: 2023-04-26T23:21:29+08:00
draft: false
categories: ["tool","macOS"]
---

手里有一把支持Mac和Windows的键盘，但是唯独右边的Command键不对劲，使用按键检修的软件查看发现不是Right_Command的映射。
## 解决办法
使用hidutil修改映射，脚本如下
```shell
FROM="\"HIDKeyboardModifierMappingSrc\""
TO="\"HIDKeyboardModifierMappingDst\""

Application="0x700000065" 
Right_Command="0x7000000e7"

hidutil property --matching '{"ProductID":0xb34c, "VendorID":0x46d}' --set "{\"UserKeyMapping\":[
{$FROM: $Application,$TO: $Right_Command}
]}"
```
其中的ProductID和VendorID可以使用`hidutil list`查看

按键的原本的映射使用karabiner-elements查看,目标映射查询网站 https://developer.apple.com/library/archive/technotes/tn2450/_index.html

保存为shell脚本后运行即可修改键位

## 开机自动执行
1. 打开启动台-其他-自动操作，点击文件新建一个，文稿类型选择应用程序，在左边资源库栏中选择实用工具，在子菜单中选择运行Shell脚本，在右边的输入框中输入脚本内容
2. 点击运行，看是否成功修改
3. 保存此程序
4. 在设置中的登录项中加入保存的程序即可