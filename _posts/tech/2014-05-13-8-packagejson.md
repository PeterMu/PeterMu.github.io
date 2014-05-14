---
layout: post
title: package.json中的波浪线(~) 
description: 
category: tech
---

## 1. 含义

如果指定版本的module有更新补丁出现时, 它将自动升级到开发中的版本。

## 2. 注意

如果你的module依赖的module的更新会对自己的module出现兼容问题，那这个波浪线可就邪恶了，如果要明确指定依赖的module，请去掉波浪线，指定固定的版本号！
