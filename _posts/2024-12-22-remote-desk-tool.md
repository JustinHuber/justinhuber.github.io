---
layout: mypost
title: rustdesk 最好用的免费开源远程软件
categories: [rustdesk, 远程桌面, 免费]
---

# 需求 
远程协助，客户端，串流
可选软件：rustdesk toDesk 向日葵 teamviewer anydesk 微软自带远程桌面

# 对比
rustdesk优势：开源免费 自建服务器无限制 多客户端
完全免费，无需安装，开箱即用
支持局域网端到端发现、支持 IP 白名单、剪贴板互通 (复制粘贴文件)、收发文本消息等功能。
支持 Windows、macOS、Liunx、IOS、Android、Web 等多个平台
支持远程文件传输
支持控制安卓手机
界面简洁易用，使用简单，无需太多学习成本
端到端加密，基于角色的访问控制权限，保证数据传输安全
自定义画面质量
内置文件传输和TCP隧道功能

# 搭建
服务端建议docker compose安装
services:
  hbbs:
    container_name: hbbs
    image: rustdesk/rustdesk-server:latest
    command: hbbs
    volumes:
      - ./data:/root
    network_mode: "host"
    depends_on:
      - hbbr
    restart: unless-stopped
  hbbr:
    container_name: hbbr
    image: rustdesk/rustdesk-server:latest
    command: hbbr
    volumes:
      - ./data:/root
    network_mode: "host"
    restart: unless-stopped

    # 因为使用 docker host 模式
    # 以防您忘记端口：
    # 21114 TCP 用于网页控制台，仅在 Pro 版本中可用
    # 21115 TCP 用于 NAT 类型测试
    # 21116 TCP TCP 打洞
    # 21116 UDP 心跳/ID 服务器
    # 21117 TCP 中继


### 端口使用说明
默认情况下，hbbs 监听21115(tcp), 21116(tcp/udp), 21118(tcp)，hbbr 监听21117(tcp), 21119(tcp)。
务必在防火墙开启这几个端口，请注意21116同时要开启TCP和UDP。
其中21115是hbbs用作NAT类型测试，21116/UDP是hbbs用作ID注册与心跳服务，21116/TCP是hbbs用作TCP打洞与连接服务，21117是hbbr用作中继服务, 21118和21119是为了支持网页客户端。如果您不需要网页客户端（21118，21119）支持，对应端口可以不开。



TCP(21115, 21116, 21117, 21118, 21119)
UDP(21116)
21118, 21119端口非必须

### 客户端 使用自建服务器
https://github.com/rustdesk/rustdesk/releases
首先去官网下载客户端 windows，MAC，ubuntu，安卓，iOS，都有客户端，甚至还有网页版，只要你下载安装了软件，就可以控制别人，也可以被别人控制。自建服务器的好处是没有数量限制也没有并发限制。

### 获取key
找到服务端公钥   
id_ed25519（私钥）id_ed25519.pub（公钥）  
文本编辑器打开类似：4hOx9idblsI678JMGJGJ3QgK00zJlLdd8gyvopJIIdM=

### 配置客户端 一般默认端口可不写 只需ID服务器和key
ID服务器：域名/IP:21116
中继服务器：
API服务器：
KEY：上面获取到的Key

被控制端可以不用填写 key ，控制端则必须填写 key

# 福利😄：
阿里云白嫖结束  

 






