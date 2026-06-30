---
title: 行为树学习笔记
date: 2026-06-30 19:20:00
categories:
  - 游戏开发
tags:
  - AI
  - 行为树
  - Unity
description: 从 Obsidian 笔记迁移过来的行为树入门记录。
---

状态机是状态驱动，而行为树是决策驱动：它更关心 AI 究竟该做什么。

![行为树示意图](https://goodnighttt221-1327371730.cos.ap-nanjing.myqcloud.com/goodnighttt221-1327371730/Obsidian-%E9%9A%8F%E7%AC%9420260205105521874.png)

行为树从左到右执行所有子节点。如果子节点执行失败，会打断 `Sequence` 的执行。

![NodeCanvas 行为树插件](https://goodnighttt221-1327371730.cos.ap-nanjing.myqcloud.com/goodnighttt221-1327371730/Obsidian-%E9%9A%8F%E7%AC%9420260205110327728.png)

上图是 NodeCanvas 插件中的行为树编辑界面。

