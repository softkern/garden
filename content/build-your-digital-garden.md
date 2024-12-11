---
title: 使用 Quartz 搭建自己的数字花园
date: 2024-12-09
tags:
    - quartz
    - cloudflare
---

## 在本地电脑上安装Quartz

要安装Quartz，至少需要`Node v20.9.0` 和 `npm v9.3.1` 才能够正常运行，需要先安装好，然后执行以下命令从 Github 上下载源码:

```shell
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
npx quartz create
```

本地运行：
```shell
npx quartz build --serve
```

## 将代码上传到自己的 Github

###  在 Github 上创建一个新项目
![](https://img.softkern.com/images/2024/12/1b45db1ec695bb5916a21dd2fcf83fa4.webp)

###  拷贝自己的仓库地址:
![](https://img.softkern.com/images/2024/12/318cc28faed37f224136e4449cce0f0f.webp)

### 设置本地项目的远程仓库

```shell
git remote set-url origin <REMOTE-URL>
```

示例如下， 可以使用 `git remote -v` 查看是否设置成功：

```shell
❯ git remote -v
origin	https://github.com/jackyzha0/quartz.git (fetch)
origin	https://github.com/jackyzha0/quartz.git (push)
upstream	https://github.com/jackyzha0/quartz.git (fetch)
upstream	https://github.com/jackyzha0/quartz.git (push)

❯ git remote set-url origin git@github.com:softkern/digital-garden.git

❯ git remote -v
origin	git@github.com:softkern/digital-garden.git (fetch)
origin	git@github.com:softkern/digital-garden.git (push)
upstream	https://github.com/jackyzha0/quartz.git (fetch)
upstream	https://github.com/jackyzha0/quartz.git (push)
```
### 同步本地内容到 Github 仓库

首次同步内容:
```shell
npx quartz sync --no-pull
```

后续内容如果发生变化，可以使用以下命令继续同步:
```shell
npx quartz sync
```

## 部署

本文使用 Cloudflare Pages 来进行部署，如若需要使用其他方式，可以查看官网 [hosting](https://quartz.jzhao.xyz/hosting)。

具体的流程如下，主要就是在 Cloudflare 中创建一个新的 Pages 项目，然后连接到 Github 指定项目进行部署：
![](https://img.softkern.com/images/2024/12/a9b33c73a64f26399c63f11db8022aa6.webp)

![](https://img.softkern.com/images/2024/12/5705a23f09fd5efe41e61fc2a6df866b.webp)

![](https://img.softkern.com/images/2024/12/b0c7f13478002e4c38bfa2be07686a61.webp)

![](https://img.softkern.com/images/2024/12/32cc530be9a4c6d7667e39b40f1bbf54.webp)

![](https://img.softkern.com/images/2024/12/d65a4c1290902f3b887a86c232eb82aa.webp)

![](https://img.softkern.com/images/2024/12/a9bb0548b30920542fa9b092cbde593f.webp)

![](https://img.softkern.com/images/2024/12/26e15b62ed56fcf08ed31d7bac4c1dbe.webp)

另外在部署成功后，如果有域名挂在 Cloudflare 上，可以自定义域名，方便访问:

![](https://img.softkern.com/images/2024/12/cfe137dc4bfe4228a8cecd3639236e12.webp)

![](https://img.softkern.com/images/2024/12/ea67f49f1828da07f9a0f755fae5e30f.webp)

然后就可以使用 Cloudflare 给的子域名 或者 自己的自定义域名来访问。

## 参考链接:

- [quartz 官网首页](https://quartz.jzhao.xyz/)
- [Github 仓库配置](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository)
- [部署相关内容](https://quartz.jzhao.xyz/hosting)

