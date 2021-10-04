---
title: Git的使用心得
author: Mark
summary: 讲述了Git的安装，配置，工作流程，和文件各个状态之间的转变，以及在Intellij idea和Vscode软件下的运用
tags:
  - Git
  - 代码托管
categories:
  - 软件技术
abbrlink: 547feeee
date: 2021-09-24 11:30:00
---

## 1.Git在Windows上的安装

官方版本可以在 Git 官方网站下载。 打开 https://git-scm.com/download/win，下载安装即可。



## 2.Git的配置

安装完 Git 之后，要做的第一件事就是设置你的用户名和邮件地址。 这一点很重要，因为每一个 Git 提交都会使用这些信息，它们会写入到你的每一次提交中，不可更改：

```console
$ git config --global user.name "li-niuniu"
$ git config --global user.email myloveislizihao@163.com
```

#### 检查配置信息

如果想要检查你的配置，可以使用 `git config --list` 命令来列出所有 Git 当时能找到的配置。

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924125903265.png)



## 3.Git文件的各种状态

#### Git工作流程

一般工作流程如下：

- 克隆 Git 资源作为工作目录。
- 在克隆的资源上添加或修改文件。
- 如果其他人修改了，你可以更新资源。
- 在提交前查看修改。
- 提交修改。
- 推送到远程库

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924165839084.png)

#### Git的工作区、暂存区和版本库

- **工作区：**就是你在电脑里能看到的目录。
- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924170020844.png)

#### 文件的已追踪和未追踪

工作目录下的每一个文件都不外乎这两种状态：**已跟踪** 或 **未跟踪**。 已跟踪的文件是指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后， 它们的状态可能是未修改，已修改或已放入暂存区。简而言之，已跟踪的文件就是 Git 已经知道的文件。

工作目录中除已跟踪文件外的其它所有文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有被放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态，因为 Git 刚刚检出了它们， 而你尚未编辑过它们。

编辑过某些文件之后，由于自上次提交后你对它们做了修改，Git 将它们标记为已修改文件。 在工作时，你可以选择性地将这些修改过的文件放入暂存区，然后提交所有已暂存的修改，如此反复。

![](https://cdn.jsdelivr.net/gh/cumark/picBed/lifecycle.png)

#### 克隆远程仓库

克隆仓库的命令是 `git clone <url>` 。 比如，要克隆提交作业的仓库，可以用下面的命令：

```console
$ git clone https://gitee.com/fengjie_zstu/graduate-single-program2021.git
```

#### 检查当前文件状态

可以用 `git status` 命令查看哪些文件处于什么状态。 如果在克隆仓库后立即使用此命令，会看到类似这样的输出：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924140554567.png)

所有已跟踪文件在上次提交后都未被更改过。 此外，上面的信息还表明，当前目录下没有出现任何处于未跟踪状态的新文件，否则 Git 会在这里列出来。

现在，创建一个新的`test/test.txt`文件。 如果之前并不存在这个文件，使用 `git status` 命令，你将看到一个新的未跟踪文件：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924142740202.png)

使用命令 `git add`可以跟踪一个文件。 所以，要跟踪 `test/test.txt` 文件，运行：

```
git add test
```

此时再运行 `git status` 命令，会看到 `test/test.txt` 文件已被跟踪，并处于暂存状态:

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924143124340.png)

如果修改一个已被跟踪的文件，运行`git add`命令可以重新放到暂存区

#### 提交更新

已修改但未暂存的文件只会保留在本地磁盘。 所以，每次准备提交前，先用 `git status` 看下，你所需要的文件是不是都已暂存起来了， 然后再运行提交命令 `git commit`：

```
git commit
```

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924144147905.png)

#### 查看提交历史

在提交了若干更新，又或者克隆了某个项目之后，你也许想回顾下提交历史。 完成这个任务最简单而又有效的工具是 `git log` 命令。

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924144625010.png)

#### 去掉已经托管在本地的文件

如果想去掉已经托管在本地的文件，将文件变为未追踪的文件，可以使用`git rm`命令：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924165155686.png)

## 4.远程仓库

#### 查看远程仓库

如果想查看你已经配置的远程仓库服务器，可以运行 `git remote -v`  命令。 它会列出你指定的每一个远程服务器的简写和对应的URL。 如果你已经克隆了自己的仓库，那么至少应该能看到 origin ——这是 Git 给你克隆的仓库服务器的默认名字：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924145511192.png)

#### 添加远程仓库

运行 `git remote add <shortname> <url>` 添加一个新的远程 Git 仓库，同时指定一个方便使用的简写：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924145802838.png)

现在可以在命令行中使用字符串 `abc` 来代替整个 URL。 例如，如果你想拉取URL对应的仓库中有但你没有的信息，可以运行 `git pull origin`：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924150355597.png)

这说明目前远程仓库的内容已经全部被抓取到本地仓库

#### 推送到远程仓库

当你想分享你的项目时，必须将其推送到上游。 这个命令：`git push <remote> <branch>`。 当你想要将 `master` 分支推送到 `origin` 服务器时（克隆时通常会自动帮你设置好那两个名字）， 那么运行这个命令就可以将你所做的备份到服务器：

```console
$ git push origin master
```

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924151226584.png)

只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先抓取他们的工作并将其合并进你的工作后才能推送。

#### 远程仓库的重命名与移除

以运行 `git remote rename` 来修改一个远程仓库的简写名。 例如，想要将 `abc` 重命名为 `def`，可以用 `git remote rename` 这样做：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924151528374.png)

值得注意的是这同样也会修改你所有远程跟踪的分支名字。 那些过去引用 `abc/master` 的现在会引用 `def/master`。

如果想要移除一个远程仓库,可以使用 `git remote remove` 或 `git remote rm` ：

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924151808763.png)



## 5.Git分支

### 分支创建

Git 是怎么创建新分支的呢？ 很简单，它只是为你创建了一个可以移动的新的指针。 比如，创建一个 testing 分支， 你需要使用 `git branch` 命令：

```console
$ git branch testing
```

这会在当前所在的提交对象上创建一个指针。

当需要在非当前分支上工作时，需要使用`git checkout`命令:

```
$ git checkout testing
```

某些场景下，需要合并两个分支，则需要使用`git merge`命令:

```
$ git checkout master

$ git merge testing
```

这样testing分支中的内容会合并至master之中



## 6.在Intellij Idea中暂存，提交并推送

#### 暂存

当做了更改之后，

右键文件，点击git分支下的add，将其放到暂存区中

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924174240592.png)

#### 提交

点击git分支下的commit file，并在弹出的对话框中输入提交信息，将其提交本地库中

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924174427415.png)

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924174600718.png)

#### 推送

点击右下角branch分支，核对本地分支及远程库之后，点击local branches下的branch，点击push即可

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924174715285.png)



## 7.在Vscode中暂存，提交并推送

#### 暂存

当做了更改之后，

点击左边第三个，源代码管理

点击更改栏目下的test_vscode.md右边的加号，将其放到暂存的更改中

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924173240036.png)

#### 提交

点击源代码管理右侧的对号，并在弹出的对话框填入提交消息

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924173517226.png)

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924173606680.png)

#### 推送

核对本地分支及远程库之后，在如下界面点击推送即可

![](https://cdn.jsdelivr.net/gh/cumark/picBed/image-20210924173740184.png)





参考链接：

https://git-scm.com/doc
