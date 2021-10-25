---
title: Linux Ubuntu的使用
author: Mark
summary: 讲述了Ubuntu系统的安装，软件安装，美化及遇到的问题
tags:
  - Linux
categories:
  - 软件技术
date: 2021-10-05 20:50:00
---

## 1.Ubuntu系统的安装

Ubuntu镜像可以在官方网站上下载，推荐版本20.04.3 LTS，支持维护至2025年

https://ubuntu.com/download/desktop

下在完成后，清空自己的u盘，用Rufus工具制作启动u盘

https://rufus.ie/zh/

Ubuntu所安装的空间建议在40g以上，在windows桌面上右键点击计算机，管理，磁盘管理，进行分区，分出为Ubuntu安装的空间

重启电脑，进入Bios界面，进入U盘启动，在图形化界面点击Install Ubuntu

按照推荐配置语言等设置，但，在安装类型中，选择其他选项

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005210618.png)

在新出现的界面点击左下角+号分区

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005210820.png)

分区建议分两个分区，如果总空间40g，home分10g，根目录/分30g
+ 第一个分区挂载于/Home，用于存放用户文件
+ 第二个分区挂载于/，用于存放系统及软件文件
    ![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005212058.png)

启动引导器安装于根目录/下

## 2.Ubuntu的软件安装与美化

进入主界面后，点击软件与更新，更换下载服务器，推荐aliyun镜像

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005212817.png)

#### 更新系统

```
更新本地包数据库
sudo apt update

更新所有已安装的包（也可以使用 full-upgrade）
sudo apt upgrade
```
#### 安装git
```
apt install git
```
#### 安装搜狗拼音输入法

+ 添加中文语言支持打开 系统设置——区域和语言——管理已安装的语言——在“语言”tab下——点击“添加或删除语言”
![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005214532.png)

+ 弹出“已安装语言”窗口，勾选中文（简体），点击应用
![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005214611.png)

+ 回到“语言支持”窗口，在键盘输入法系统中，选择“fcitx”
![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005214631.png)

注：如果在键盘输入法系统中，没有“fcitx”选项时，建议先打开终端手动安装fcitx：sudo apt-get install fcitx等安装成功之后再执行上述步骤点击“应用到整个系统”，关闭窗口，重启电脑

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005214824.png)

下载搜狗拼音主程序

https://pinyin.sogou.com/linux/?r=pinyin

用命令行解压搜狗拼音主程序

```
sudo dpkg -i sogoupinyin_2.4.0.3469_amd64.deb
```

如果安装过程中提示缺少相关依赖，则执行如下命令解决：
```
sudo apt -f install
```
注销计算机即可正常使用搜狗输入法

#### 安装Typora软件

```
# or run:
# sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -

# add Typora's repository
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt update

# install typora
sudo apt install typora
```

#### 安装基于docker的微信

安装依赖
```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
用脚本安装docker
```
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
```
启动docker
```
$ sudo systemctl enable docker
$ sudo systemctl start docker
```
拉取微信镜像
```
docker pull bestwu/wechat

# 注意！！！ '把你的用户名' 替换成你的用户名
docker run -d --name wechat\
    --device /dev/snd\
    --ipc=host\
    -v /tmp/.X11-unix:/tmp/.X11-unix\
    -v /home:/home\
    -v /home/你的用户名/WeChatFiles:/WeChatFiles\
    -e DISPLAY=unix$DISPLAY\
    -e XMODIFIERS=@im=ibus\
    -e QT_IM_MODULE=ibus\
    -e GTK_IM_MODULE=ibus\
    -e AUDIO_GID=`getent group audio | cut -d: -f3`\
    -e GID=`id -g`\
    -e UID=`id -u`\
    bestwu/wechat
# 首次启动等个1～2分钟 出现扫码登录即可
```
常用命令
```
docker start wechat
docker stop wechat
docker restart wechat
```

#### 安装基于docker的qq
docker安装教程在上文，安装之后
```
# 拉取镜像
docker pull bestwu/qq
# 启动 
# 注意！！！ '把你的用户名' 替换成你的用户名
docker run -d --name qq\
    --device /dev/snd\
    --ipc=host \
    -v /home:/home\
    -v /home/你的用户名/TencentFiles:/TencentFiles\
    -v /tmp/.X11-unix:/tmp/.X11-unix\
    -e XMODIFIERS=@im=ibus\
    -e QT_IM_MODULE=ibus\
    -e GTK_IM_MODULE=ibus\
    -e DISPLAY=unix$DISPLAY\
    -e AUDIO_GID=`getent group audio | cut -d: -f3`\
    -e VIDEO_GID=`getent group video | cut -d: -f3`\
    -e GID=`id -g`\
    -e UID=`id -u`\
    bestwu/qq:latest
```
每次微信和qq打开的时候，会在左上角有一个托盘，可以在 Gnome Tweak Tool插件中启用TopIcons Plus并在设置中选择 托盘水平对齐方式 - 右对齐，至此微信的图标就可以正常显示在桌面右上角了

#### 桌面美化
安装tweak
```
sudo apt install gnome-tweak-tool
```
安装插件
```
# 让 gnome 支持插件扩展
sudo apt install gnome-shell-extensions 

# chrome 浏览器扩展支持，可以使用浏览器安装插件
sudo apt install chrome-gnome-shell
```
常用插件：
dash to dock
Applications Menu
OpenWeather
Hide Top Bar

在https://extensions.gnome.org/ 中可以自行探索个性化的插件

主题/壁纸下载

在https://www.gnome-look.org/browse 中可以下载个性化的主题，解压后复制至/usr/share/themes之中，壁纸复制至/usr/share/background之中

在tweak工具内，设置主题和壁纸

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005222906.png)

#### 终端美化

打开终端后，点击右上角，首选项，在首选项中进行个性化设置，个人喜欢将终端透明化

![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005223021.png)


## 3.使用时遇到的问题

#### 文件权限问题

linux系统的文件权限比较复杂，常遇到无文件权限的问题，有以下两种简易的方法解决
+ chown：修改所属用户与组
+ chmod：修改用户的权限

例如没有aaa.txt文件的权限
```
sudo chown mark aaa.txt
sudo chmod 777 aaa.txt
```
这里mark是用户名，777是所属的最高权限

linux常用命令：
```
sudo root权限
cp -r 复制
rm 删除单一文件
rmdir 删除空的文件夹
rmdir -rf 删除文件夹内所有内容
rm -rf * 删除目录下所有内容
rm -rf /* 删除整个分区的内容，慎用
touch 创建文件
vi 修改编辑vim文件
```

#### boot启动盘的问题

此前个人分区时，单独分了200m的磁盘空间作为启动盘，结果在更新过程之中空间用尽。然后删除linux内核以腾出空间，误删了主内核。

如果boot分区挂在根目录下，则不会出现这类问题。如果已经出现删除启动内核的情况
+ 首先要输入history命令，查看被删除的内核
+ 然后在windows系统内或者u盘内下载已经被删除的内核bat包
+ 用u盘启动，点击试用ubuntu，解压bat包后复制至boot盘内，即可解决

解决内核问题后，则要考虑把boot启动盘挂在根目录下，而不是单独分区
+ 加sudo前缀，输入
  ```
  cp -a /boot /boot2
  umount /boot
  rmdir /boot
  mv /boot2 /boot
  ```
  把boot盘中的内容复制至根目录下的boot目录

+ 删除/etc/fstab中的/boot条目：
  vi /etc/fstab
+ 输入`sudo update-grub`
+ 输入`sudo vi /boot/efi/EFI/ubuntu/grub.cfg，修改根目录磁盘的uuid,和根目录磁盘
    ![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005225852.png)

如果没设置好efi，则在进入时会直接进入grub命令模式，这时依次输入命令
```
linux linux内核地址
initrd initrd文件地址
```
![](https://cdn.jsdelivr.net/gh/cumark/picBed/20211005230400.png)