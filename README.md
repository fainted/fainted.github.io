# 基于Hexo的博客搭建

## 1. Hexo 初始化
使用Hexo首先需安装[nodejs && npm][https://nodejs.org/en/download/]
```shell
npm install -g hexo-cli --save
npm install
npm install hexo-deployer-git install hexo-server --save
```

## 2. 基础使用
# [写作备忘手册](https://hexo.io/zh-cn/docs/writing.html)
```shell
# 生成静态资源
hexo generate

# 本地服务预览, 默认0.0.0.0:4000
hexo server [-i <ip>] [-p <port>]

# 部署至远端服务器
hexo deploy [-g]    # -g Generate before deployment
```
