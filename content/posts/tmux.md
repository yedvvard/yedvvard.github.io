---
title: "Tmux用法"
date: 2023-04-07T22:50:51+08:00
draft: false
toc: true
---

默认Prefix = Command/Ctrl + B
## 会话
- tmux new -s name 新建session
- tmux ls  显示当前有多少后台session
- Prefix + d  detach会话session
- Prefix + s 选择session

## window
- Prefix + c  新建window
- Prefix + &  删除当前window
- Prefix + n  切换下一window

## 分屏
- Prefix + % 左右分屏
- Prefix + "  上下分屏
- Prefix + z  全屏/取消全屏某pane
- Prefix + ⬆️⬇️⬅️➡️ 移动焦点到某个pane
- Prefix + x  删除某个pane
