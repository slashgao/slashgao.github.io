---
title: 搭建基于Hexo和Next主题和Github Pages个人博客教程
date: 2019-06-29 22:55:51
tags:
  - Hexo
  - Next
  - Github Pages
  - Travis CI
Categories:
  - Hexo
---

## Hexo简介

Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。大家可以进入[hexo官网](https://link.zhihu.com/?target=https%3A//hexo.io/zh-cn/)进行详细查看，因为Hexo的创建者是台湾人，对中文的支持很友好，可以选择中文进行查看。

## Hexo搭建步骤

### 安装Node.js

官网下载 https://nodejs.org/en/download/

装好后可以用命令查看版本号。

```
node -v
v10.16.0

npm -v
6.9.0
```

### 安装Hexo

```
#安装Hexo脚手架
npm install hexo-cli -g

#初始化Blog，创建blog文件夹
hexo init blog
cd blog

#安装依赖
npm install
```

此时，文件下结构如下：

```
node_modules: 依赖包
public：存放生成的页面
scaffolds：生成文章的一些模板
source：用来存放你的文章
themes：主题
_config.yml: 博客的配置文件
```

最后，运行程序，显示如下信息就可以访问http://localhost:4000，看到博客已经搭建成功了。

```
hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

设置主目录下的`_config.yml`，里面有网站基本设置

```
#网站标题
title: Hexo     
#网站副标题
subtitle:
#网站描述
description:
keywords:
#作者名字
author: John Doe
#网站语言
language:
#时区
timezone:
```

具体全部配置参考[官方文档](https://link.juejin.im/?target=https%3A%2F%2Fhexo.io%2Fzh-cn%2Fdocs%2Fconfiguration)。



### 安装Next主题

在博客文件夹下运行，安装完成后在themes下多了一个next文件夹

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

修改主目录下的`_config.yml`, 把theme替换成next

```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/

theme: next
```



打开主题配置文件打开`thems/next/_config.yml`

#### 设置scheme外观样式

```
# Schemes
#scheme: Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
#scheme: Mist - Muse 的紧凑版本，整洁有序的单栏外观
#scheme: Pisces - 双栏 Scheme，小家碧玉似的清新
scheme: Gemini
```

选择对应的外观，刷新浏览器即可预览。

#### 设置菜单

```
menu:
  home: / || home
  #about: /about/ || user
  #tags: /tags/ || tags
  #categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
```

当需要`about`、`tags`、`categories` 需要手动创建这个页面，如果不创建点击则不会出现相应页面。

使用如下命令创建这些文件夹

```
hexo new page "about"
hexo new page "tags"
hexo new page "categories"
```

之后`source`文件夹下就会出现三个这样的文件夹。

#### 设置头像

```
avatar:
  # in theme directory(source/images): /images/avatar.gif
  # in site  directory(source/uploads): /uploads/avatar.gif
  # You can also use other linking images.
  url: #/images/avatar.gif
  # If true, the avatar would be dispalyed in circle.
  rounded: false
  # The value of opacity should be choose from 0 to 1 to set the opacity of the avatar.
  opacity: 1
  # If true, the avatar would be rotated with the cursor.
  rotated: false
```

修改字段 `avatar`， url值设置成头像的链接地址

#### 开启打赏功能

需要在**主题配置文件**中开启并填入微信和支付宝收款二维码图片地址 即可开启该功能

先生成微信和支付宝二维码图片，将图片放在`themes/next/source/images`下

微信:

1. 右上角的+
2. 选择我要收款
3. 保存相册

支付宝:

1. 右上角的+
2. 选择我要收款
3. 保存相册

```
# Reward (Donate)
reward_settings:
  # If true, reward would be displayed in every article by default.
  # You can show or hide reward in a specific article throuth `reward: true | false` in Front-matter.
  enable: true
  animation: false
  comment: 感谢您的支持将鼓励我继续创作！

reward:
  wechatpay: /images/wechatpay.jpg
  alipay: /images/alipay.jpg
  #bitcoin: /images/bitcoin.png
```



#### 设置tags 和 categories 

当菜单中有了 `tags` 和 `categories` 时，我们需要添加 `type` 属性

修改tags/index.md

```
---
title: tags
date: 2019-06-23 18:49:03
type: "tags"
---
```

修改categories/index.md

```
---
title: categories
date: 2019-06-23 18:49:14
type: "categories"
---
```

### 安装插件

#### 插件汇总

```
# 更换Markdown渲染器
npm un hexo-renderer-marked --save
npm i hexo-renderer-markdown-it-plus --save
# 站内搜索插件
npm install hexo-generator-searchdb --save
# 网站访问速度优化插件
npm install hexo-filter-optimize --save
# 统计阅读文字字数
npm install hexo-symbols-count-time --save
# sitemap插件
npm install hexo-generator-baidu-sitemap --save
npm install hexo-generator-sitemap --save
# gulp 压缩插件
npm install gulp --save
npm install gulp-clean-css --save
npm install gulp-htmlclean --save
npm install gulp-htmlmin --save
npm install gulp-imagemin --save
npm install gulp-uglify --save
# git depploy 插件
npm install hexo-deployer-git --save
# 固定链接插件
npm install hexo-abbrlink --save
# -leancloud-counter安全插件，暂时未使用
npm install hexo-leancloud-counter-security --save
# valine 评论系统插件
npm install valine --save
# RSS插件
npm install hexo-generator-feed --save
```

#### 添加 Disqus 评论服务

访问主页 https://disqus.com/，点击 `GET STARTED`

注册Disqus

选择 `I want to install Disqus on my site`

创建网站

- `Website Name` 填写网站的名字
- `Shortname` 网站在Disqus的唯一标识
- `Category`：网站的类别，我这里创建的是技术类

订阅

订阅图上所示的 `Free`：针对小型，个人、非盈利性，不提供任何广告的网站。除了 `Plus` 中的 `Direct Email Support`，其他特性都支持。

修改配置文件

```
# Disqus
disqus:
  enable: true
  shortname: Shortname - 换成刚才设置的Shortname
  count: true
  lazyload: false
```



### 写博客

hexo new "Hello World"

会在`source`目录下自动创建一个名为 `Hello World.md` 的文件，打开这个文件写文章就行了。

同样我们需要每篇文章指定一个或多个 `tags` 和 一个 `categories`。这样你的菜单中`tags` 页面 和`categories`页面就会有内容了。

```
title: Hello World
date: 2019-06-29 22:55:51
tags:
  - Hexo
  - Next
Categories:
  - Hexo
```



## 部署到Github Pages

Github Pages 是 Github 公司提供的免费的静态网站托管服务，用起来方便而且功能强大，不仅没有空间限制，还可以绑定自己的域名。很多非常著名的公司和项目也都用这种方式来搭建网站，如[微软](http://microsoft.github.io/)和 [twitter](http://twitter.github.io/) 的网站，还有 [谷歌的 Material Design 图标](http://google.github.io/material-design-icons/) 网站。



到 https://pages.github.com/ 上，看到可以创建的网站有两类，一类是为自己或者是自己的组织创建站点，就是新建一个仓库，仓库的名字叫做，username.github.io 或者是 orgnizationname.github.io ，注意这里的 username 和 orgnizationname 要严格替换成你自己的用户名或者组织名，大小写也要区分，不然就会有问题。然后就往仓库里面放页面内容就行了。第二类是为项目创建网站，这个其实主要步骤都是一样的，只不过稍微比创建用户或组织网站复杂一点点。

### 安装Git

官网下载 https://gitforwindows.org/

装好后可以用命令查看版本号

```
git --version
git version 2.22.0.windows.1
```

### GitHub创建个人仓库

登录or注册一个Github账号

New repository，新建仓库

创建一个和你用户名相同的仓库，用户名.github.io



### 创建SSH Key 

在命令行（即Git Bash）输入以下命令

```
ssh-keygen -t rsa -C "youremail"
```

生成的Key在当前用户的.ssh文件夹下

```
id_rsa
id_rsa.pub
```

把公钥id_rsa.pub放在GitHub上，这样当你连接GitHub自己的账户时，它就会根据公钥匹配你的私钥，当能够相互匹配时，才能够顺利的通过git上传你的文件到GitHub上。

在GitHub的setting中，找到SSH keys的设置选项，点击New SSH key 把你的id_rsa.pub里面的信息复制进去。



### 配置Git Bash

```
git config --global user.name "yourname"
git config --global user.email "youremail"
```

yourname输入你的GitHub用户名，youremail输入你GitHub的邮箱

查看是否配置成功

```
ssh -T git@github.com
Warning: Permanently added the RSA host key for IP address '13.229.188.59' to the list of known hosts.
Hi slashgao! You've successfully authenticated, but GitHub does not provide shell access.
```

### 部署到GitHub

先安装部署到Github的依赖

```
npm install hexo-deployer-git --save
```

然后修改站点配置文件 _config.yml，找到deploy，修改为 YourgithubName为你的GitHub账户

```
deploy:
  type: git
  repository: https://github.com/YourgithubName/YourgithubName.github.io.git
  branch: master
```

生成及推送至Github

```
#清除已经生成的本地静态文件
hexo clean
#生成本地静态文件
hexo generate
#将本地静态文件推送至Github
hexo deploy
```

效果参考我的博客，打开浏览器，访问http://slashgao.github.io



## 基于Travis CI实现自动部署

在使用 Hexo 写博客的时候，每次总是要使用 hexo deploy 将博客部署到 GitHub Pages，然后在把博客的源文件 push 到自己的 GitHub repository ，这就要求每次发布博客的时候要求搭建好Hexo环境。

有一个方便方法是引入Continuous Integration，简称 CI：意思是，在一个项目中，任何人对代码库的任何改动，都会触发 CI 服务器自动对项目进行构建，自动运行测试，自动编译，甚至自动部署到测试环境。这样做的好处就是，随时发现问题，随时修复。因为修复问题的成本随着时间的推移而增长，越早发现，修复成本越低。

Travis CI 是在线托管的 CI 服务，用 Travis 来进行持续集成，不需要自己搭服务器。

[官网对使用 Travis CI 有详细的使用步骤](https://docs.travis-ci.com/user/tutorial/)：

* 前往 [Travis-ci.com](https://travis-ci.com/) and Sign up with GitHub.

* 接受授权

* 选择你想要使用 Travis CI 的仓库 或者 你也可以在 Github-settings-Applications-TravisCI-Configure 中去更新配置；

* 在你仓库怎增加 .travis.yml 文件，这个文件定义了构建的步骤，例如[安装依赖](https://docs.travis-ci.com/user/job-lifecycle/#customizing-the-installation-phase)等等。

* 将 .travis.yml 文件推送到你的远端仓库，然后就会触发 Travis CI 构建；

* 登录 [Travis CI](https://travis-ci.com/)然后选择你的仓库查看构建任务的执行详情；



**Job Lifecycle – Job 生命周期**

Travis CI 为每种编程语言提供默认构建环境和默认的阶段集。 创建虚拟机为你的Job提供构建环境，将存储库克隆到其中，安装可选的插件，然后运行构建阶段。

job 的声明周期，主要包含两大部分：

install：安装依赖，官网有专门讲解的 [Installing Dependencies](https://docs.travis-ci.com/user/installing-dependencies/)

script：运行构建脚本；在 installation 阶段之前（beofore_install）、在 script phase 之前（before_script）或之后（after_script），你可以运行自定义命令；当构建成功或失败置换后，可以使用 after_success（例如构建文档）或 after_failure（例如上载日志文件）阶段执行其他操作（actions）。 

在 after_failure 和 after_success 中，您可以使用 $TRAVIS_TEST_RESULT 环境变量获取构建结果。

完整的 job 生命周期(包括三个可选的部署阶段，以及在检出 git 存储库 和更改到存储库目录) 

如下：

```
apt addons 可选安装
cache components 可选安装
before_installinstall
before_script
script
before_cache (for cleaning up cache) 可选
after_success or after_failure
before_deploy 可选
deploy 可选
after_deploy 可选
after_script
```



### 配置Travis

为了能够实现代码推送到 Github，需要在Github 生成一个 Persional access tokens，在 [settings- Developer settings](https://github.com/settings/tokens)可以生成。

然后进入 Travis 中的[项目设置界面](https://travis-ci.com/account/repositories)，可以给具体的代码库进行设置，比如增加环境变量：主要加了一个环境变量 GITHUB_TOKEN，这个在后面的 .travis.yml 文件中会用到。



### 配置Github Repository

之前的博客代码库只有一个 master 分支，存放的都是 hexo g 命令生成的静态文件。

现在改成把博客代码库放到dev分支，再由Travis CI 生成博客再部署到master分支上。

* 本地准备好博客代码库

* 新建一个dev分支：

  git checkout -b dev

* 添加 .travis.yml 文件

  Travis CI 会执行用户定义的 .travis.yml 脚本。我想在这个脚本中实现：使用 Hexo 生成博客内容，再将博客内容部署到 YourgithubName.github.io 项目的 master 分支 上。

  ```
  language: node_js
  node_js: stable
  
  env:
    global:
      - GH_REF: github.com/YourgithubName/YourgithubName.github.io.git
  
  branchs:
    only:
      - dev
  
  cache:
    directories:
      - node_modules
  
  # Start: Build Lifecycle
  before_install:
    - npm install -g hexo-cli
  
  install:
    - npm install
  
  #before_script:
  
  script:
    - hexo clean
    - hexo generate
  
  after_script:
    - cd ./public
    - git init
    - git config user.name "yourname"
    - git config user.email "youremail"
    - git add .
    - git commit -m "Update docs"
    - git push --force --quiet "https://${GITHUB_TOKEN}@${GH_REF}" master:master
  # End: Build LifeCycle
  ```

* 把主题文件下的 .git 目录删除了，不然主题不会提交

### 推送到Github

```
#查看当前branch
git branch
git add .
#提交修改
git commit -m "init documents"
#推送到dev分支
git push origin dev
```

此时在Travis CI中自动生成已启动，并查看日志。