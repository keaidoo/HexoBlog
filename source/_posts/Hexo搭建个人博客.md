---
title: 一篇非常详实的Hexo搭建个人博客教程
author: 可爱多
avatar: https://cdn.jsdelivr.net/gh/keaidoo/CDN/img/custom/avatar.jpg
authorLink: 
authorAbout: 你肉眼可见的，只能看见美的东西，而不能看见美本身。
authorDesc: 你肉眼可见的，只能看见美的东西，而不能看见美本身。～
categories: 技术
date: 2019-10-27 16:46:01
comments: true
tags: 
 - 博客
keywords: 
description: 
photos: https://cdn.jsdelivr.net/gh/keaidoo/cdn@1.2/img/custom/paperPhoto/1.jpg
---

## 前言
博客是作为一个程序猿的标配，由于工作的原因，我们记录笔记的方式早已不是高中阶段的在笔记本上用手抄的形式。作为一个计算机的从业者，我们后面会接触到很多新的知识点和技术。我们应当学会在互联网上记录自己这些心得笔记，所以搭建一个属于自己的个人博客就显得很有必要了。

首先要明确一点，就是我们的目的不仅仅是学会搭建博客，博客只是一个个人平台。更重要的是养成定期写博客，更新技术笔记的习惯。

- 我的博客:https://keaidoo.github.io 

## 配置环境
### 1.Git
- 介绍
  Git 是当下全球计算机从业者使用最多一个代码版本控制工具，也是我们必须要掌握并熟练使用的一个工具。我们能够使用它进行代码的备份，回退。并且在多人开发时，能够进行代码合并。通常，大型的项目开发都必须使用 Git 进行版本控制，开发人员负责提交代码，项目经理负责代码的合并，这一切都是采用 Git 来完成的。

- Git 和 Github
  - 目前有很多同学都不清楚 Git 和 Github 之间的区别，认为 Git 就等同于 Github。实际上两者是完全不同的，Github 只是一个网站，一个专门用于存储 Git 上传的代码仓库。我们将本地的代码使用 Git 上传到 Github 上面托管，我们所有的数据都存储在上面，多人开发时，也是大家同时使用 Github 上面的同一个仓库进行代码管理。

  - Git[1]是一个工具，Github[2]是当下全球最大的一个开源代码托管平台。全世界的程序员都将代码放到上面进行托管，各种开源的语言、库都可以在上面找到源代码。国内也有类似的代码网站，由于 Github 是一个国外的网站，国内访问加载和上传速度都很慢，所以我们有时候采用国内的码云[3]。功能和使用方法都是一样的，只不过一个在国内一个在国外。

- 安装
Git 是一个开源的工具，可以直接在官网下载然后通过一键安装即可。这里我们选择一个 Git Bash 一键安装 Git，如果电脑不是 windows 系统自行下载相应的系统的版本即可。

- Git 下载地址[4]
安装步骤: 直接运行 exe 文件，全部 next，不用修改任何配置即可
安装完成，在任意文件夹下右键即会出现 Git Bash 选项，点击进入 Git Bash 界面，输入git version指令出现 Git 的版本信息则表示安装成功

### 2.安装 NodeJs
- 介绍
  node.js 是运行在服务端的 ```JavaScript```，通常我们知道的 ```CSS/HTML/JS ```是网页前端开发的标准三件套。HTML 负责搭建网页的主体框架和布局，CSS 负责跳转每个版块之间的间距，各种控件的颜色大小等等，JS 则用于实现网页上的一些动态元素，例如一些动画效果，并接受一些动态的参数。通常 JS 作为一种胶水语言都是用于前端开发的。

  但是``` node.js ```为 js 搭建了一个平台，使得 js 也能像``` Java/Python/PHP ```一样用于后台开发。由于我们使用的 hexo 框架是基于 ```node.js ```实现的一个博客框架，所以我们首先要搭建一个服务端的 JS 环境。

- 安装
NodeJs 下载地址[5](下载 LTS 版本)
下载好 msi 文件后，也是一键安装，不过记得在``` Custom Setup ```这一步勾选下面的```Add To PATH```，把 node 添加到你电脑的环境变量中
在任意文件夹下打开 ```Git bash```，输入```node -v```出现了 node 的版本信息即为安装成功
如果安装时忘记勾选```Add to PATH```，可以在电脑左下角搜索编辑系统环境变量，点击打开，点击环境变量，然后再用户配置或者系统配置中Path点击编辑，将你的 ```node.js ```的 bin 文件目录添加进去即可。

### 3.安装 hexo
- 介绍
  Hexo[6] 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

  简单来说，就是一个别人写好的博客网站模板，你直接下载下来试用就可以了。并且 hexo 支持便捷的更换网站主题，就像你的电脑更换壁纸一样，你可以在网上下载一个 hexo 主题，复制到相应的文件夹下就可以一键更换你整个网站的界面和功能了。

- 安装
  创建一个文件夹用于存放整个博客网站的文件，建议和你的仓库一样命名为```yourname.github.io```
  进入该文件夹右键进入 Git bash 界面
  先使用```git --version和node -v```确认都能正常出现版本信息没有报错方可进入下一步
  输入```npm install -g hexo-cli```，安装 hexo 指令
  输入```hexo -v```确认指令安装成功
  确认上一步没有报错后，使用hexo init进行 hexo 博客框架的初始化安装完成后，会出现如下文件夹
  - 解释一下
    ```node_modules：```是 node.js 的依赖包
    ```public：```存放的是生成的网页前端页面
    ```scaffolds：```命令生成文章等的模板
    ```source：```存放你的 markdown 博客文件
    ```themes：```网站主题，可自行下载，默认是landscape
    ```_config.yml：```整个博客的配置
    ```db.json：```source 解析所得到的
    ```package.json：```项目所需模块项目的配置信息

  到此我们的博客就已经在本地搭建完成了，依次输入下面三个指令可以在本地预览博客的效果：

  ```hexo clean``` 清空 hexo 缓存
  ```hexo generate```根据 markdown 文件生成相应的资源文件
  ```hexo server```在电脑本地运行 hexo 服务 看到如下信息，就代表你的 hexo 博客已经在本地运行起来了，可以在浏览器中打开```http://localhost:4000```进入博客，按```Ctrl+c```关闭服务。

### 4.连接 Github
- 介绍
  Github 是全面全球最大的一个代码托管平台，他是有许许多多的代码仓库构成，每个人都可以创建仓库，并且仓库的所有代码都是公开的，因此我们能在上面找到各种项目各种语言的源代码。今后我们学习和工作会与它密不可分。学习世界上最顶尖的大牛、最优秀的开源框架的代码也是一种极快提升我们视野和能力的途径。

  刚才我们只是本地运行了 Hexo 博客，这里我们要做的是将我们本地的 hexo 博客的文件夹上传到 Github 的仓库当中，让所有人都能访问到我们的博客。Github 为我们每个注册的用户免费提供了一个```https://yourname.github.io```的域名，因此我们可以将 Github 当成服务器运行我们博客网站。每次我们需要写博客就在本地写好之后同步提交到 Github，然后我们的博客也能自动更新。

- 准备
 首先你需要到Github[7]使用邮箱注册一个账号
然后创建一个 ```repository```(仓库) 仓库的名字一定要是```yourname.github.io```例如: 我的用户名是```keaidoo```然后我们仓库名就是```keaidoo.github.io```因为 Github 只为我们提供这一个可以访问的域名
- Git 配置
  网上有很多方法是使用 ```ssh``` 连接 Github，但是由于初学者难以理解，这里我们采用在 url 链接中直接使用账号密码的方式连接 Github

  打开的``` hexo ```博客文件夹，右键进入 Git Bash
  输入git init，该指令用于将该文件夹初始化为一个 Git 仓库，会生成一个.git文件用于存储该仓库的一些信息
  输入```git remote add origin https://用户名:密码@github.com/xxx/xxx.git```该指令用于指定远程仓库的地址。仓库的最上方可以查看该网址，每个仓库都有两个网址作为该仓库的唯一标识，分别是```https://xxx和git@github:xxx```这里我们使用``` https ```的这个并在链接的中间加入自己的账号密码，注意修改成你自己的 ```github``` 账号密码和仓库地址。最后我们是通过这个链接中的账号密码来登录 Github 的。例如: 我的是```git remote add origin https://ctguqmx:mypassword@github.com/ctguqmx/ctguqmx.github.io.git```

- github仓库的连接
  输入```git config --global user.name "yourname"和git config --global user.email "youremail"```设置你的用户名和注册邮箱地址

- 本地git的配置
  修改 hexo 配置文件，打开博客根目录下的```_config.yml```文件，翻到最下面，按照如下方式修改，注意用你的自己的仓库链接，**并且:后面有一个空格**，多了或者少了都会报错
  ```
  deploy:
  type: git
  repo: https://github.com/yourname/yourname.github.io.git
  branch: master
  ```
最后使用```npm install hexo-deployer-git --save```安装一个插件，hexo3 不自带 Git 上传功能。
- 常见错误:

  - ```fatal: remote origin already exits.```
  原因：你已经绑定过了远程仓库的链接 
  解决办法：```git remote rm origin```删除链接，然后再用```git remote add http://xxx```

  -  ```fatal: Authentication failed for 'https://github.com/xxx/xxx.git'```
  原因：账号或者密码错误 
  解决办法：git remote -v查看的你绑定的链接中的账号密码是否正确
  - ```Template render error: (unknown path)```
   原因：你写的 Markdown 博客文件语法错误，无法解析 
解决办法: 找到相应的语法错误并修正
- 部署博客
  现在我们可以开始部署我们的博客了

  在浏览器中打开```http://localhost:4000```
  看到界面就代表你成功了
  最后按```Ctrl+c```停止本地服务
  使用```hexo deploy```将项目发布到 ```github``` 上
  在浏览器中打开```https://yourname.github.io```
  看到界面就代表你真的成功了

### 5.开始动手写一篇博客吧
下面我将展示写一篇博客的常规操作

```hexo new "my_first_blog"```
进入到博客文件夹的```source/_posts```目录下应该可以看一个```my_first_blog.md```的文件
你可以使用 ```markdown``` 的语法开始编写一篇博客了。具体语法可以参考```markdown``` 语法[8]
```hexo g -d```是```上hexo generate```和```hexo deploy```的简写，直接一键发布

### 6.换一个更好看的主题
hexo 默认为我们提供了一个网站的主题，实际上我们可以自己在 github 上下载更多更加好看，并且功能强大的主题来替换掉我们原有的主题，并且更换起来十分方便，基本上是一键切换。

我们可以自行在网上搜索hexo 主题，便会出来很多供我们选择，配置起来也很简单。例如我的博客就是在有哪些好看的 hexo 主题 -知乎[9]上面找到的。下面我将以我们所用的主题为例，来实验一下如何切换 hexo 主题。

首先选定一款 hexo 主题找到他的 github 仓库地址。例如我的是：yilia[10]
进入到你的博客文件夹下的 themes 文件夹，里面初始应该只有一个```landscape```主题，也就是你当前博客所使用的主题
打开 ```Git Bash``` 输入```git clone http://xxx.git```，将仓库克隆到本地，也可以在仓库右上角直接下载压缩包解压到 themes 文件夹下，但是注意要修改文件名。
```git clone https://github.com/litten/hexo-theme-yilia.git yilia```
修改博客根目录下的``` _config.yml ```文件，修改``` themes: yilia```
```
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
```
```theme: yilia```
进入```yilia```文件夹，修改```_config.yml ```文件(不是根目录下面的那个)，内容参考yilia 参考配置[11]
OK，主题切换完成，写博客的基本步骤和原来一样

### 7.改进空间
其实上面只是简单复制了别人写好的博客网站，实际上我们还有更大的开发空间和写博客的一些必备技能。我这里详细展开，仅提供一些可以自己学习的方向。

- Markdown
前面已经说过了，Hexo 是一款专门针对 markdown 的博客框架，也就是说我们的博客必须都是用 markdown 文件，因此我们必须要学习 markdown 的基本语法来编写博客，实际上 markdown 的语法非常简单，总共的语法也只有几十条，在编写博客时顺带查询 markdown 语法即可。本文就是由 markdown 自动生成，无需任何手动排版。

- JS 插件
其实我们可以在原有的主题的基础上进行二次开发，增加一些新的功能，例如我们经常在别人博客中看到的一些动态水墨效果，点击出现爱心等特效，还有博客的点赞评论，网站的流量统计等等，网上都有相应的 JS 插件，配置也十分简单，网上也有大量的教程，可自行学习。

- Latex
后面大家在编写博客时肯定会出现一个问题，就是数学公式怎么编辑，实际上 Markdown 中可以直接使用 Latex 进行数学公式的编辑，Latex 可以用编程的方式来编写出一个数学公式，同样的，用 Latex 编辑数学公式，也是我们学习计算机的一个基本技能。我建议和 Markdown 一样，大家都可以从需求出发，需用到什么就学相应的语法来完成你的需求，从用中学，从而达到熟能生巧。

- 图床
  我们在编写博客时，经常需要插入一些图片，我们可以在 Source 文件下新建一个文件专门用来存储图片，然后再 Markdown 博客中用相对路径来引入图片。图片会随着你的博客项目一起推送到 Github 当中，但是这种往往加载速度很慢，加上 Github 容量有限并且是国外的服务器。

  这里我们可以单独将我们的图片文件上传到第三方的服务器上，然后直接通过图片的 url 来访问。目前常用的用阿里云和七牛云，新建一个存储空间用来存放图片，基本都有一定免费的存储额度。并且他们有专业的图片加速算法，通常加载速度都非常快。

- 域名
我们默认的使用的是 Github 提供给我们的域名，实际上我们可以自己申请一个域名，来替换掉这个域名，阿里云，腾讯云等等都能进行域名的申请，例如我使用```.top```的域名，一年只有几块钱，```.com```一年大概 50~60。申请一个自己的个人域名后面也会大有用处，至于后续的域名备案，大家可自行摸索。

## 参考资料
- [1]Git: https://baike.baidu.com/item/Git/12647237
- [2]Github: https://github.com
- [3]码云: https://gitee.com
- [4]Git下载地址: https://gitforwindows.org/
- [5]NodeJs下载地址: https://nodejs.org/en/
- [6]Hexo文档: https://hexo.io/zh-cn/docs/index.html
- [7]Github: https://github.com
- [8]markdown语法: http://xianbai.me/learn-md/index.html
- [9]有哪些好看的hexo主题 -知乎: https://www.zhihu.com/question/24422335
- [10]yilia: https://github.com/litten/hexo-theme-yilia
- [11]yilia参考配置: https://github.com/litten/BlogBackup/blob/master/_config.yml