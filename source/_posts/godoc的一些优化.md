---
title: godoc的一些优化
date: 2017-03-19 10:34:04
tags:
- go
- godoc
---

## 前言
一般安装golang会附带godoc。
命令行下执行godoc -play -http :8686，然后在浏览器访问http://localhost:8686。
可以看到一个同[go blog](https://blog.golang.org)“一样”的页面

## 示例代码的执行
go的注释化文档支持添加示例代码，比如下图**strconv.Atoi**的例子
{% asset_img strconv-Atoi-example.png %}

点击Run将运行看到的示例代码，整个过程是这样的：
*1. POST http://godoc-server/compile*
*2. godc-server将请求转发至https://play.golang.org/compile*
*3. 返回响应*

由于最终会访问官方playground。于是会有以下原因导致示例无法运行。
*1. 代码写错了*
*2. 引入了第三方包（github或公司服务器），或自己写的本地包*
*3. 国情*

当然，只要能将 */comile* 接口改为本地编译运行就可以避免后两种情况。
研究了一下[go-tools](https://github.com/golang/tools)/[go-playground](https://github.com/golang/playground)
对源码进行一下“组装”，就可以将示例在本地运行了。
```sh
git clone https://github.com/fainted/tools.git
gopm get -g golang.org/x/tools

cd tools/cmd/godoc && go build
cp godoc $(which godoc) # 替换当前godoc程序
cd -
rm -rf tools
```
