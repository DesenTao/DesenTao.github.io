---
weight: 1
title: "Mac环境使用Hugo + even + Github部署本站"
date: 2015-03-06T21:40:32+08:00
lastmod: 2021-01-01T10:10:10+08:00
draft: false
author: "陶德森"
authorLink: "https://www.xinyongdan.com"
description: "Mac环境使用Hugo + even + Github部署本站"
resources:
- name: "Mac环境使用Hugo + even + Github部署本站"
  src: "complete-configuration-preview.zh-cn.jpg"

tags: ["installation", "configuration"]
categories: ["documentation"]

lightgallery: true

toc:
  auto: false
---

Mac环境使用Hugo + even + Github部署本站。

<!--more-->

- **GitHub Pages** 是一个静态站点托管服务，直接将个人、组织或项目的页面托管于 `GitHub` 库或仓库 `repository`中。
- **Hugo** 是一个用 `Go` 语言编写的静态站点生成器，它针对速度、易用性和可配置性进行了优化，快速灵活。
- **even** 是 `Hugo` 的一个热门主题。
- **Homebrew** 是一款包管理工具，目前支持`macOS`和`linux`系统。

## 一 本地部署

---

**1、安装**Homebrew

`Homebrew`默认安装脚本：

```
/bin/bash -c "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install.sh)"
```

最后看到 `==> Installation successful!` 就说明安装成功了。

**然后再更新一下**：

`​brew update`

**2、 安装** Hugo

```
brew install hugo
```

> 注意：需要提前安装 homebrew

查看 `Hugo` 是否安装成功，通过**检查版本号**

```
hugo version
```

**3. 创建一个新的站点**

```
// 请先在命令行中进入您的工作目录
cd /Volumes/DesenTao/Blog
hugo new site DesenTao.github.io
```

**4. 添加一个LoveIt主题**

```
cd DesenTao.github.io
git init
git submodule add https://github.com/dillonzq/LoveIt themes/LoveIt
```

**查看目录结构**

```
# 目录结构
tree blog
#blog
#├── archetypes
#│   └── default.md
#├── config.toml
#├── content
#├── data
#├── layouts
#├── static
#└── themes
```

`config.toml` 是**配置文件**，在里面可以定义博客地址、构建配置、标题、导航栏等等。

`themes` 是**主题目录**，可以去 [themes.gohugo.io](http://themes.gohugo.io/) 下载喜欢的主题。

`content` 是**文章目录**。

如果需要**调整更改主题**，需要在 themes/LoveIt 目录下重新 build

`cd themes/LoveIt && npm i && npm start`

**5. 修改配置文件**

**拷贝`even`主题下的配置文件模板**至站点根目录

`cp /themes/LoveIt/exampleSite/config.toml config.toml`

**6. 添加一篇文章**

```
hugo new posts/my-first-post.md  # "my-first-post.md" 是新建文章的文件名。
```

**7. 启动`Hugo`服务器**

`hugo server -D`

通过浏览器访问 [http://localhost:1313](http://localhost:1313) 查看本地部署站点的页面效果。

## 二、部署为Github Pages

---

**1、创建一个 `Github` 仓库**

`New repository` 

在 `Github` 上创建 `<username>.github.io` repository

**2. 将该仓库 clone 到本地**

`git clone <YOUR-REPOSITORY_URL>`

**3. 进入到根目录，创建一个 Hugo 项目，确保在本地可以运行**

`hugo server`

**4. 在 Github Repository 的 Setting 页面，修改 Source 的选项为 master branch /docs folder**

**5. 修改配置文件 config.toml**

同时 config.toml 的 `baseURL` 要设置成 `https://<username>.github.io`

**6. 打包网站到 /docs 文件夹**

`hugo -d docs`

**7. 上传代码至 master**

`git commit -m "updates $(date)"`
`git push origin master`

​**8. 访问 `https://<username>.github.io` 查看效果**

## 三、解析域名

---

通过域名控制台的解析功能，添加一个记录类型为**CNAME**，主机记录为@，解析线路默认，记录值为github的仓库名 `https://<username>.github.io`，TTL可选默认10分钟

回到你的username.github.io仓库，创建一个**CNAME**文件，文件内容为你的`https://<username>.github.io`

至此，你就可以通过输入你自己注册的域名进入你创建的站点啦~

### 四、友情链接

---

1. **[陶德森的随笔](https://www.xinyongdan.com)**
2. **[信托周末&TrustWeekend](https://trustweekend.com)**