---
layout: post
category: "linux"
title:  "Linux系统中搭建openVPN(客户端)"
tags: [linux,openVPN]
---

### 简介
>搭建openVPN流程(客户端)  
>本文以CentOS 7.8 64位  
>转自 http://www.zhangblog.com/2020/05/09/openvpn01/  

### 下载openVPN客户端
官网下载对应的系统版本 https://openvpn.net/download-open-vpn/ 

### 客户端client用户配置文件
从之前服务端复制ca.crt、client.crt、client.key、ta.key出来。  
ca.crt、client.crt、client.key、ta.ke、client.ovpn放在同一个文件夹内。  
client.ovpn需要自己单独写(remote为服务器的IP地址)：  
~~~
client
dev tun
proto udp
remote 0.0.0.0 1194
resolv-retry infinite
redirect-gateway def1
nobind
;user nobody
;group nobody
persist-key
persist-tun
ca ca.crt
cert client.crt
key client.key
remote-cert-tls server
tls-auth ta.key 1
cipher AES-256-CBC
compress lz4-v2
verb 3
~~~

### 使用openVPN打开client.ovpn，则可以连上
