---
layout: post
title: Nginx-install
categories: Web Server
description: Linux(CentOS 8 x64)系统下安装Nginx。
keywords: Nginx, Linux
---

# Nginx Linux(CentOS 8 x64)系统下进行安装

## 主要内容

*  安装编译工具及库文件
*  安装PCRE，让NGINX支持Rewrite功能
*  安装NGINX
*  安装过程中遇到的问题


# 一. 安装编译工具及库文件

	`# yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel`

# 二. 安装PCRE，让NGINX支持Rewrite功能

	`# yum install pcre`

# 三. 安装NGINX

## 3.1 下载NGINX

可以在官网http://nginx.org/en/download.html下载最新版本的NGINX

    `# wget http://nginx.org/download/nginx-1.16.1.tar.gz`

## 3.2 解压

    `# tar -zxvf nginx-1.16.1.tar.gz`

## 3.3 进入安装包目录

    `# cd nginx-1.16.1`

## 3.4 编译安装

    `# ./configure --user=nobody --group=nobody --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_gzip_static_module --with-http_realip_module --with-http_sub_module --with-http_ssl_module && make && make install && make clean
	--with-pcre=/usr/src/pcre-8.42 指的是pcre-8.42 的源码路径。
	--with-zlib=/usr/src/zlib-1.2.11 指的是zlib-1.2.11 的源码路径。`
删除回车和解释，注意空格 --with-pcre=/usr/src/pcre-8.42 --with-zlib=/usr/src/zlib-1.2.11 应为自己下载的

## 3.5 查看安装路径并进入

    `[root@localhost nginx-1.13.7]# whereis nginx
	nginx: /usr/local/nginx
	[root@localhost nginx-1.13.7]# cd /usr/local/nginx`

## 3.6 启动NGINX

    `[root@localhost nginx]# sbin/nginx`

启动后可在浏览器上访问 host:port，如 127.0.0.1:80 。若打开后出现如下页面则安装完成 
![Alt text](http://www.wangzhixian.club/images/posts/nginx/welcome to nginx.png "welcome to nginx")

# 四. 安装过程中遇到的问题

## 4.1 使用make编译时报错

    `在包含自 src/core/ngx_core.h：71 的文件中，
                 从 src/core/nginx.c：9:
	src/core/ngx_regex.h:15:18: 错误：pcre.h：没有那个文件或目录
	In file included from src/core/ngx_core.h:71,
                 from src/core/nginx.c:9:
	src/core/ngx_regex.h:24: 错误：expected specifier-qualifier-list before ‘pcre’`

原因及解决方法： 
未安装pcre-devel

    `# yum install pcre-devel

	yum -y install openssl openssl-devel`

更改后再次运行出错，提示信息：

    `cd /srv/pcre2-10.21 \
        && make libpcre.la
	make[2]: Entering directory `/srv/pcre2-10.21'
	make[2]: *** 没有规则可以创建目标“libpcre.la”。 停止。
	make[2]: Leaving directory `/srv/pcre2-10.21'
	make[1]: *** [/srv/pcre2-10.21/.libs/libpcre.a] 错误 2
	make[1]: Leaving directory `/srv/nginx-1.13.7'`

原因及解决方法： 
将pcre安装成了pcre2，NGINX不支持pcre2，换成pcre

## 4.2 启动NGINX失败

提示信息：

    `nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
	nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
	nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
	nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
	nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
	nginx: [emerg] still could not bind()`

原因及解决方法： 
NGINX所使用的端口号被占用，默认端口为80，可以在配置文件中修改或者关闭占用端口的进程

NGINX配置文件如下：

    `[root@localhost conf]# vi nginx.conf

	#user  nobody;
	worker_processes  1;

	#error_log  logs/error.log;
	#error_log  logs/error.log  notice;
	#error_log  logs/error.log  info;

	#pid        logs/nginx.pid;


	events {
    	worker_connections  1024;
	}


	http {
    	include       mime.types;
    	default_type  application/octet-stream;

    	#log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    	#                  '$status $body_bytes_sent "$http_referer" '
    	#                  '"$http_user_agent" "$http_x_forwarded_for"';

    	#access_log  logs/access.log  main;

    	sendfile        on;
    	#tcp_nopush     on;

    	#keepalive_timeout  0;
    	keepalive_timeout  65;

    	#gzip  on;

    	server {
        	listen       80;
        	server_name  localhost;

        	#charset koi8-r;

        	#access_log  logs/host.access.log  main;

        	location / {
            	root   html;
            	index  index.html index.htm;
	"nginx.conf" 117L, 2656C written`
