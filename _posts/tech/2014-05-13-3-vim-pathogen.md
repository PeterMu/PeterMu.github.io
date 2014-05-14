---
layout: post
title: Vim 插件管理（pathogen） 
description: 捣鼓linux有段时间了，Vim这伙计真是华丽丽，各种插件各种有。工欲善其事必先利其器，Vim绝对是个响当当的利器，要打造一个属于自己的Vim，需要安装N种插件，一个个安装一个个配置，麻烦！有了 pathogen，everything is ok！

category: tech
---

捣鼓linux有段时间了，Vim这伙计真是华丽丽，各种插件各种有。工欲善其事必先利其器，Vim绝对是个响当当的利器，要打造一个属于自己的Vim，需要安装N种插件，一个个安装一个个配置，麻烦！有了 pathogen，everything is ok！

##1. 准备工作

###下载pathogen

可以通过以下两种方式获得安装文件

1. 下载zip包：[pathogen.zip](https://github.com/tpope/vim-pathogen/archive/master.zip)

1. 通过git检出

```java
git clone git://github.com/tpope/vim-pathogen.git
```    

##2. 安装

1. 创建安装目录


```java
mkdir -p ~/.vim/autoload ~/.vim/bundle
```
    
bundle文件夹下是放置插件的地方。
        
2. 拷贝文件

将下载的文件中autoload下的pathogen.vim拷贝到    `~/.vim/autoload

##3. 配置.vimrc

将以下代码假如到.vimrc中。

```java
execute pathogen#infect()
```
    
到此就安装完成了。

##4. 举例：使用pathogen安装NERDTree

```
cd ~/.vim/bundle
git clone https://github.com/scrooloose/nerdtree.git
```

Ok!NERDTree安装成功了！安装的所有插件都在bundle文件目录下了。
    
使用`:NERDTreeToggle`命令，是不是出现目录树了。:-D
