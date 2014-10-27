---
layout: post
title: "oh-my-zsh and tmux"
description: beigin to use oh-my-zsh and tmux
headline: 
modified: 2014-10-27
category: personal
tags: [zsh,tmux]
image: 
  feature: 
comments: true
mathjax: 
---


#oh-my-zsh

oh-my-zsh基于zsh，所以先需要安装zsh,Ubuntu直接`sudo apt-get install zsh`，oh-my-zsh相当于别人帮我们配置好了zsh，官方网站是[ohmyz.sh](http://ohmyz.sh/ "oh my zsh")

##安装

自动下载安装：

Via curl: `curl -L http://install.ohmyz.sh | sh`

Via wget: `wget --no-check-certificate http://install.ohmyz.sh -O - | sh`

手动安装：
从[oh-my-zsh github](https://github.com/robbyrussell/oh-my-zsh "oh-my-zsh on github")上下载，通过git或者直接下载zip包都可以，解压到～/.oh-my-zsh


##使用

拷贝配置模板：
`cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc`

通过`cat /etc/shells`命令可以查看本机上有那些可用的shell

		~ $ cat /etc/shells
		# /etc/shells: valid login shells
		/bin/sh
		/bin/dash
		/bin/bash
		/bin/rbash
		/bin/zsh
		/usr/bin/zsh

使用zsh为默认shell

		chsh -s /bin/zsh

最后重启终端

tmux
=====
关于介绍自己看维基百科[tmix](http://en.wikipedia.org/wiki/Tmux)

##安装

Ubuntu直接`sudo apt-get install tmux`即可。或者从[psourceforge](http://sourceforge.jp/projects/sfnet_tmux/releases/)下载tmux。
注意需要安装两个依赖包

		sudo apt-get install libevent-dev libncurses5-dev

然后

		Downloads $ tar zxvf tmux-1.9a.tar.gz
		Downloads $ cd tmux-1.9a 
		tmux-1.9a $ ./configure
		tmux-1.9a $ make
		tmux-1.9a $ sudo make install

安装完成

等待配置

		


