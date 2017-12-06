---
layout: post
title:  "关于阿里云FileZilla Server的配置"
date:   2017-12-06 
categories: 阿里云
tags:  阿里云
excerpt: 关于阿里云使用FileZilla从客户端传代码到服务器上的配置。
author: YuKang
---

* content
{:toc}

# 关于阿里云FileZilla Server的配置
环境：“专有网络”ECS实例，Windows 2012系统 
 
目标：安装 FileZilla Server , 配置证书安全（TLS）访问 
 
过程： 
 
 ### 1. 下载，安装 FileZilla Server 0.9.60.2 
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_b8fa6ed3ab15632.png?22)
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_3c7c85055c863ac.png?19)

### 2. 登录到FTP控制台 
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_fda2bdfcf18490e.png?22)

### 3. 会自动检测到服务器当前位于NAT网络，没有配置TLS证书，点击 Settings 来设置
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_41d95aac901dbe3.png?12)

###4. 在 Passive mode settings 被动模式中，设置端口范围，如 20000 - 20500 
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_9b9123c6363cc5e.png?37)

###5. 在 FTP over TLS settings 里选择证书的文件（服务器证书和私匙等文件），也可尝试自动创建证书（Generate new cetficiate）
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_0a58a8e7153ed2e.png?36)

### 6. 点击快捷菜单里的用户头像图标，或 Edit -> Users 来添加FTP用户，输入用户名；点击 Password 为新创建的用户设置密码 
![](http://bbs.aliyun.com/attachment/thumb/Fid_239/239_1477160476054779_a96525c62613901.png?33)
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_d05ed2b0f646f18.png?15)

### 7. 点击 Shared folders ，再为FTP用户设置默认目录，及勾选读写等权限（Read Write Delete Append 等）
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_29189de5347214f.png?19)

### 8. 在实例的安全组规则里，添加允许TCP 21 和 TCP 2000 - 20500 访问的规则 
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_4873a5592b74f8c.png?19)

### 9. 在 FileZilla Client 快速连接测试，首次会提示证书的详情，点击“确定”后即可成功连接 
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_26ad5c59d30b640.png?59)
![](http://bbs.aliyun.com/attachment/Fid_239/239_1477160476054779_a14031621017494.png?33)

