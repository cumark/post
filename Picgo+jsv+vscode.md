---
title: Picgo+jsv+vscode/Typora搭建个人图床
author: Mark
summary: 讲述了Picgo与jsv加速在vscode或者Typora之中的使用
tags:
  - 文档使用
categories:
  - 软件技术
date: 2021-10-05 20:24:00
---

## 1.创建github图床仓库

新建图床仓库，即图片上传的远程仓库

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005203605.png)

生成github token

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005203831.png)

保存这个token，在下一步会应用

## 2.Picgo插件下载和使用

在vscode扩展中搜索PicGo，安装

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005202524.png)

打开扩展设置，进行配置，Custom Url前缀使用https://cdn.jsdelivr.net/gh 进行加速，
之后是/你的用户名/你的仓库名

在token中填入上一步所保存的token即可

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005202808.png)

配置完成后，使用快捷键进行快速操作

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005203223.png)

上传图片后，github中会显示所图床上传的图片

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005204300.png)

## 3.图床在Typora之中的使用

下载PicGo客户端，配置与vscode的PicGo插件类似

在Typora中的图像设置中，对Picgo个性化设置

