---
title: 通过Hexo搭建个人博客（一）配置和部署
date: 2024-04-27 16:31:03
categories: 
 - 折腾记录
tags: 
 - 折腾
 - Hexo
 - Git
---

通过hexo和github page从零搭建个人博客。

<!-- more -->

参考材料：[**Hexo文档**](https://hexo.io/zh-cn/docs/)；[**从零开始搭建个人博客（超详细）**](https://zhuanlan.zhihu.com/p/102592286)；[**Hexo+Next主题搭建个人博客+优化全过程（完整详细版）**](https://zhuanlan.zhihu.com/p/618864711)

## 前置

首先下载和配置[**git**](https://git-scm.com/)和[**Nodejs**](https://nodejs.cn/)的环境

Nodejs在可能需要管理员权限才能使用npm工具，遇到问题可以参考[**Windows下使用npm显示权限不够**](https://blog.csdn.net/mr__sun__/article/details/119140624)修改nodejs文件夹Users权限，或以管理员身份打开windows powershell到指定文件夹再操作；npm下载不更换国内镜像源的话可能需要科学上网

## 绑定GitHub

git初始化
`cd [folder]`
`git init`

在github中创建新的资源库，并将repository name改成`你的用户名.github.io`，使得最后repository页面网址为`https://github.com/你的用户名/你的用户名.github.io`的形式；将id_rsa.pub的内容拷贝到Settings的SSH keys里面

验证
`ssh -T git@github.com`

## 配置Hexo

安装Hexo
`cd [folder]`
`npm install -g hexo-cli`
*本命令相当于执行了以下几步：
`git clone hexo-starter`和`hexo-theme-landscape`主题到当前目或指定目录。
使用Yarn 1、pnpm 或npm包管理器下载依赖（如有已安装多个，则在前面的优先）。npm 默认随 Node.js 安装。*

检查npm下载
`npm list -g --depth=0`

初始化
`hexo init [folder]`
`cd [folder]`
`npm install`
生成的文件中
- _config.yml 可以在此配置网站大部分参数
- package.json 记录了Hexo的插件信息
- scaffolds Hexo会根据scaffold中的模板创建文件
- source 存放用户的各种资源，如markdown文章、媒体资源等
- themes Hexo会根据主题来生成静态页面
- node_modules 依赖包下载的位置

编辑blog根目录下_config.yml文件：
```yml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git
  repository: git@github.com:你的用户名/你的用户名.github.io.git  #仓库地址
  branch: main  #git下branch的名字，老版本是master
```

输入指令
`hexo clean` 用于清除缓存文件 (db.json) 和已生成的静态文件 (public)
`hexo generate`或`hexo g` 生成静态文件
`hexo server`或`hexo s` 启动本地服务器，默认情况下的网址为"localhost:4000"
这时就能离线查看网站的样子了

安装部署插件hexo-deployer-git
`npm install hexo-deployer-git --save`
`hexo deploy`或`hexo d` 用于部署网站，构建在GitHub的服务器中

---