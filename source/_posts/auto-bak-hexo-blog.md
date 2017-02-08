---
title: Hexo 博客源文件备份与恢复
date: 2017-02-08 20:06:25
tags: hexo
categories: hexo
---
　　本文记录了两部分：hexo博客系统发布新文章时，自动备份托管到github；根据github上托管的项目，能够将最新的数据恢复到本地。自动备份详细技术原理可参考[文章](http://igeek.wang/2016/09/01/automatic-backup/#more)。

<!-- more -->

### 备份Hexo博客源文件
* Github上新创建一个空的repo，取名hexo-next-blog用于远程仓库备份；进入本地博客源码的hexo文件夹，创建本地仓库：
```sh
git init
```

* 设置远程仓库地址，并更新数据(第一次远程空仓库，无数据更新)：
```sh
git remote add origin git@github:XXX/hexo-next-blog.git
git pull origin master
```

* 修改.gitignore文件，加入*.log, public/ 以及 deploy*/;
* 本地提交Hexo源码：
```sh
git add .
git commit -m "hexo next blog数据备份"
```

* 本地仓库数据推送github仓库:
```sh
git push origin master
```

### 恢复Hexo博客源文件
　　切换电脑后，安装node，git环境，配置github sshkey。
　　创建空目录hexo为工作目录，clone github上的repo：
```sh
git clone git@github.com:xxx/hexo-next-blog.git
```
　　git clone成功后，安装hexo环境:
```sh
npm install hexo
npm install
npm install hexo-deployer-git
npm install --save shelljs   # 使用hexo d写文章时，自动备份时用
```

另外，themes/next主题文件夹下的数据不会备份，若需备份，可删除该文件夹下的.git目录等信息再加入备份。
