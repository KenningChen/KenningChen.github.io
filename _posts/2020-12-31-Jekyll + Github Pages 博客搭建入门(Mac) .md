---
layout: post
title: "Jekyll + Github Pages 博客搭建入门(Mac)"
subtitle: ""
author: "kenning"
header-img: "img/post-bg-web.jpg"
header-mask: 0.4
tags:
  - 技术
---

参考自https://www.jianshu.com/p/9f198d5779e6

mac环境下brew command not found:
在mac输入命令安装brew
<br>
`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
<br>
由于国内某些原因，导致http://raw.githubusercontent.com 被墙了，无法访问，提示以下错误：
<br>
`curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused`

 第一种解决方法：
 <br>
设置mac的DNS为114.114.114.114或者8.8.8.8
<br>
本人测试 无效果 还是无法打开

第二种解决方法(<font color=red>需要翻墙</font>)：
<br>
`/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"`

brew 下载成功
<br>
通过 brew 下载 wget：
<br>
 先申请权限
 <br>
 sudo chown -R $(whoami):admin /usr/local
 <br>
 再下载
 <br>
 brew install wget 
 <br>
 <br>
 nvm install --lts安装最新的官方长期支持的node版本 (<font color=red>貌似这个不需要</font>)

 
 由于网络墙的问题，需要换源:
 <br>
 `export NVM_NODEJS_ORG_MIRROR=https://npm.taobao.org/mirrors/node`
 <br>
 `sudo gem install jekyll`
 
 通过HomeBrew来升级Ruby，复制下面这句到终端回车即可。
<br>
`/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/UpdateRuby.sh)"`

https://www.mscto.com/op/456231.html (<font color=red>貌似这个不需要</font>)
<br>
/usr/local/lib/ruby/gems/2.7.0/bin(本人的目录)，配置到环境变量里


