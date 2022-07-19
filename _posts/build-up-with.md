---
title: 超详细使用GitHub pages和Hexo搭建个人博客
date: 2022-02-05 7:30:00
categories:
- 教程分享
tags: 
- web前端
- 教程
---

之前尝试过搭建过不同的博客类型,折腾了不少工作,最终决定定型在此,采用 Hexo + Github Pages 的方式。今天就带大家一起来搭建自己的博客。

<!--more-->

# 准备工作
## Git
### 安装

1. Windows:[下载并安装](https://git-scm.com/download/win)
2. macOS: [下载并安装](https://sourceforge.net/projects/git-osx-installer/)
3. Linux(Debian,Ubuntu):`sudo apt-get install git-core`
4. Linux(Fedora、RedHat、CentOS):`sudo yum install git-core`

### 相关设置
安装成功后,将 git 与 GitHub 账号绑定,右键打开 Git Bash,然后设置配置信息:![](https://pic.imgdb.cn/item/61f9c0802ab3f51d91856174.png)
接下来配置用户名和邮箱

``` bash
git config --global user.name "github 用户名"
git config --global user.email "github 注册邮箱"
```
接着生成 ssh 密钥文件,输入如下命令后直接三次回车即可,一般不需要设置密码;

``` bash
ssh-keygen -t rsa -C "github 注册邮箱"
```
一般执行上述命令之后,会生成 id_rsa 和 id_rsa.pub 两个文件,前者是我们私有的,而后者则是对外开放的。接着在 `C:\Users\Administrator\.ssh` 目录下找到生成的 .ssh 的文件夹中的 id_rsa.pub 密钥,将内容复制。

然后打开 [Gitub/Settings/Keys](https://github.com/settings/keys),创建一个新的 SSH key,填写 Title 和 Key,Title 可以随意,而 Key 的内容则是我们刚才复制的 id_rsa.pub 中的内容,最后点击 Add SSH key 即可。

# NodeJS
## 安装

去官网下载最新的稳定版[NodeJS](https://nodejs.org/en/),并安装(安装教程可自行搜索)

### 检验

安装完成后,要查看我们是否安装成功,可以打开命令提示符(Win + R),输入 cmd 打开控制台,输入如下命令,如果出现对应版本号,说明安装成功了;

``` bash
node -v
npm -v
```

![](https://pic.imgdb.cn/item/61f93b6c2ab3f51d91138b5e.png)

## 设置

**下载包是从国外服务器,所以速度较慢,因此推荐用阿里的国内镜像进行设置;**
``` bash
npm config set registry https://registry.npm.taobao.org
```

# Hexo安装

*你的硬盘上找个地儿,用来存放你的博客文件,比如我的就在 E:\Blog,这个文件夹你可以根据自己的喜好来设置。然后从命令台进入当前文件夹,接下来就是安装过程了;(由于已经安装过了,所以没有办法再去截图,更为详细的安装过程可以详见[这篇文章](https://zhuanlan.zhihu.com/p/370635512))*

1. 首先安装hexo

``` bash
npm i hexo-cli -g
```

2. 新建一个文件夹用于存放你的博客,比如我的是 blog,然后进入该文件夹,并用如下命令进行初始化并安装必备组件;

``` bash
hexo init .
npm install
```

3. 初始化后,目录结构如下;

```
├── _config.yml # 网站配置信息
├── package.json # 应用程序信息
├── scaffolds # 模板文件夹
├── source # 存放用户资源
|   ├── _drafts
|   └── _posts
└── themes # 主题文件夹
```

4. 配置
建站完成后我们需要进行 [配置](https://hexo.io/zh-cn/docs/configuration),hexo 中主要有两项配置。一项是站点配置文件,路径为 /_config.yml。另一项是主题配置文件,路径是/themes/(下载的主题)/_config.yml。

我们可以先在站点配置文件修改以下基础选项:

``` yaml
#Site
#网站主标题,SEO元素之一
title: 旖旎若鸿的小站
#网站副标题,可选
subtitle: '驻足现实,仰望星空,率性而活'
#网站描述, SEO元素之一,用于告诉搜索引擎关于这个站点的描述
description: '记录生活,热爱生活'
#网站的关键词,如:
keywords: Diary
#网站作者,如:
author: YiniRuohong
#网站使用的语言, 由于 Hexo 具备多语言配置,默认为英文,我们需要修改回中文语言
language: zh-CN
timezone: ''
```
5. 输入如下命令,然后在浏览器中打开 http://localhost:4000 ,就可以预览您的站点啦

``` bash
# 新建博客
hexo new "博客名"
# 生成静态网页
hexo g
# 打开本地服务器
hexo s
```
***此时建议先配置您的主题再进行下一步推送操作(主题配置教程见下文进阶教程)***

# 配置您的GitHub个人仓库

*完成上面的步骤之后,我们就能在本地进行预览了,不过我们如果想要发布到网上供别人看的话,那就得利用 Github Pages 的功能了,下边就来介绍如何结合 Hexo + Github Pages ,将我们的博客推送到网上去,方便大家在任何地方访问!*
> 首先你得有个 GitHub 账号,没有的请在[这里](https://github.com/)进行注册
> 
有了账号之后,新建一个仓库,而且得确保你的仓库是 public,时,仓库名一定要是:

**用户名.github.io
用户名.github.io
用户名.github.io**
（重要的事情说三遍）

![](https://pic.imgdb.cn/item/61f93b382ab3f51d91134f92.png)

# 部署到 Github

完成上面的步骤后,你应该能在本地进行预览了,接下来就是推送网站到 Github Pages 了,然后我们就能被其他人访问了。

只需要在我们刚才的博客根目录中的站点配置文件 _config.yml
完成上面的步骤后,你应该能在本地进行预览了,接下来就是推送网站到 Github Pages 了,然后我们就能被其他人访问了。

只需要在我们刚才的博客根目录中的站点配置文件 _config.yml结尾处添加如下语句:(注意按照图片格式缩进)

``` yml
deploy:
  type: git
  repo: git@github.com:GitHub用户名/GitHub用户名.github.io.git
  branch: master
```

![](https://pic.imgdb.cn/item/61f93d272ab3f51d9115ac72.png)

完成上述步骤之后,主要使用如下命令,就能将我们本地的内容推送到远程 GitHub 仓库了

``` bash
hexo clean
hexo g
hexo d
```
然后在浏览器中访问:

https://用户名.http://github.io 

***初级教程到此结束,接下来是进阶教程~***

# 安装主题

我们熟悉完博客系统的操作后,接下来就是美化博客。Hexo 支持主题,我们可以根据[官网的创建主题教程](https://hexo.io/zh-cn/docs/themes.html)自己来设计,也可以直接在[主题商城](https://hexo.io/themes/) 中找现成的主题。这里以笔者推荐的主题 Next 为例:
![](https://pic.imgdb.cn/item/61fa33762ab3f51d91e2af2b.png)

安装主题可以通过git clone克隆至blog/theme/下:(在博客根目录打开gitbash)

``` bash
# 启动主题前需要清除缓存与已部署的文件
hexo clean

# clone 主题
git clone https://github.com/iissnan/hexo-theme-next themes/next
```

接着在 站点配置文件(/_config.yml) 中启动 theme。
![](https://pic.imgdb.cn/item/61fa34392ab3f51d91e36b75.png)

再打开主题配置文件(/themes/next/_config.yml)选择 Scheme:
![](https://pic.imgdb.cn/item/61fa34ef2ab3f51d91e41d91.png)

***评论、订阅、数据统计、SEO 等部分功能配置已经集成至 next 主题配置中,但大多还需要额外添加依赖还需要根据[文档](https://theme-next.org/)来配置。next 在主题配置中集成了由于配置自定义项过多,读者可以根据自己所需添加相应的统计、SEO 相关的 app key 等就不进一步展开讲。***

# 绑定域名并使用cloudflare加速访问
## 前言

github page 在国内访问速度非常慢,而且近期 github.io 的域名经常被干扰解析成127.0.0.1,迫于无奈在网上找到了一个能白嫖加速 github page 的办法,就是套一层 cloudflare CDN,虽然它在国内没有 CDN 节点,但是整体效果是完爆 github.io,不过要注意的是免费版本是有请求次数限制的,每天 10W 次,当然这足够我的小博客使用了,这里记录一下操作步骤。

## 准备工作
### 域名

域名购买可以自行搜索购买(注意国内需要实名认证),免费域名可以白嫖[freenom](https://www.freenom.com/zh/index.html?lang=zh)或[pp.ua](https://love2wind.cn/archives/2210.html)的,请自行搜索。(注意ppua现在需要银行卡验证)
这里使用我的域名 yiniruohong.cf 为例

### GitHub page设置

通过 github 仓库中的设置页面找到对应的设置,把要用到的域名配置上去,示例图:
![](https://pic.imgdb.cn/item/61fa37e82ab3f51d91e710b1.png)

保存之后 github 会自动的在仓库根目录里生成一个CNAME文件,里面存储着域名配置信息,示例图:
![](https://pic.imgdb.cn/item/61fa38572ab3f51d91e77aab.png)

### 设置域名解析

通过域名提供商,修改刚刚的域名解析,通过 A 记录分别解析到以下 4 个 IP:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
当记录全部解析生效时,就可以通过http://monkeywie.cn访问到博客了,这个时候再开启HTTPS,示例图:
![](https://pic.imgdb.cn/item/61fa39042ab3f51d91e81e75.png)

然后 github 会自动签发提供给monkeywie.cn域名使用的 SSL 证书,等待一段时间后,就可以通过HTTPS访问博客了。

### 使用 cloudflare CDN

***~~开始白嫖~~***
1. 你需要[注册](https://dash.cloudflare.com/sign-up)一个cloudflare(以下简称cf)账号
2. 添加站点,把对应的域名填写进去
![](https://pic.imgdb.cn/item/61fa39d92ab3f51d91e8e859.png)
3. 提交之后会自动扫描域名对应的解析记录:
4. 查看 cloudfalre 对应的 NS 记录:
![](https://pic.imgdb.cn/item/61fa3a5a2ab3f51d91e984f5.png)
5. 通过域名的运营商修改对应的 NS 记录,这里每个运营商的修改方式都不一样,我这里是用的Freenom的:
![](https://pic.imgdb.cn/item/61fa3ac22ab3f51d91e9ed47.png)
6. 此时可以看到 dns 解析的 ip 已经变了,已经被 cloudflare 接管了,
然后清除下浏览器 DNS 缓存,chrome 浏览器输入chrome://net-internals/#dns进入清除页并清除DNS缓存

7. 再次访问 https://yiniruohong.cf,F12 打开网络面板可以看到已经用上了 CDN 了

# 发布文章

1. 首先进入博客所在文件夹,然后右键进入控制台,用如下命令进行创建新的文章;

``` bash
hexo n "博客标题名"
```

![](https://pic.imgdb.cn/item/61fa3c932ab3f51d91eba621.png)

2. 接着在 blog/source/_posts 目录下应该就会有创建好的以文章标题名命名的 Markdown 文件;

![](https://pic.imgdb.cn/item/61fa3d422ab3f51d91ec4e10.png)

3. 接着打开该文件,编写你自己想要的内容即可;

![](https://pic.imgdb.cn/item/61fa3ebc2ab3f51d91eda925.png)

*编辑器我这里用的是[BookPad](https://www.microsoft.com/zh-cn/p/bookpad/9n6p5zh2sjsx?activetab=pivot:overviewtab)——一款支持实时预览的markdown编辑器,如果想选择其它的可以自行搜索*

4. 接着在控制台使用如下命令,将其推送到远程 GitHub 仓库,等过一会儿之后,访问即可看到刚才推送的新文章了!

``` bash
hexo g
hexo d
```

***进阶教程到此结束,接下来是高级教程\~***

# 重定向次数过多
## 出现原因

github pages 设置好了 CNAME 自定义域名之后,便强制用户的浏览器跳转到 用户自定义域名。 同样,我们在不使用CDN时,打开 yiniruohong.github.io会自动跳转到 yiniruohong.cf,而CDN中错误的设置了回源host,会导致出现一个死循环,即 github 通知跳转了,结果CDN依旧使用 yiniruohong.github.io去回源取资源。

## 解决方法

以cf为例:cf的cdn界面有四种选择
1. Off:不开启https。

2. Flexible:当我们的源网站没有配置 HTTPS 支持时,启用这个选项,Cloudflare 会在回源的时候通过 HTTP 协议访问我们的网站。

3. Full:当我们的源网站支持 HTTPS,但是 HTTPS 证书和域名不匹配或者是自签名证书时,Cloudflare 会通过 HTTPS 协议访问源网站,但不会验证证书,也就是说,即使我们的源网站提供的 HTTPS 证书不受浏览器信任,Cloudflare 也会通过 HTTPS 回源网站。

4. Full(strict):当我们的源网站支持 HTTP ,并且证书有效时(未过期且受信任)。Cloudflare 会通过 HTTPS 协议访问源网站,并在每个请求过程中验证证书。

***知道了循环重定向的原因,我们也就知道了怎么解决这个问题,通过测试,下面的两种设置方法都可以解决 Cloudflare 循环重定向的问题。***

1. SSL 中选择 Full 或者 Full(strict),让 CDN 回源的时候使用 HTTPS 的方式回源,没有 HTTP 什么事了,就不会跳来跳去了(推荐)

2. 源网站不设置 HTTPS 支持或者 不设置 HTTP 跳转 HTTPS,让 Cloudflare 回源的时候使用 HTTP 方式获取资源。

***清理浏览器缓存后即可生效***

# 更新NEXT主题并优化

***++请首先备份您的文件并检查hexo版本(升级hexo请自行搜索)++***

## 更新NEXT主题

在blog根目录下输入:

``` bash
git clone https://github.com/theme-next/hexo-theme-next themes/next-reloaded
```

这个指令下载最新的v7.8.0版本(今天是2022.2.3)到名字为next-reloaded的文件中(网络错误就多试两次)

![](https://pic.imgdb.cn/item/61fb7d5f2ab3f51d910e4dc5.png)

然后在修改站点配置文件:

``` yaml
theme: next-reloaded
```

这一版本需要注意,中文由原来的zh-Hans变成了zh-CN(Blog\themes\next-reloaded/_config.yml 622行)

最后 `hexo s --debug`

别忘了

``` bash
hexo g
hexo d
```
这样就是全新版本了,下面是优化部分

## 优化
### 给文章添加阴影效果

首先主题配置文件取消如下代码的注释

` style: source/_data/styles.styl`

在 blog/source/_data下创建 styles.styl文件,_data文件也是我手动创建的,在styles.styl文件中添加如下内容:

``` css
// 主页文章添加阴影效果
.post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
}
```
### 给文章添加 本文结束 标记

首先主题配置文件取消如下代码的注释
`postBodyEnd: source/_data/post-body-end.swig`

在 blog/source/_data下创建post-body-end.swig文件,(_data文件也是我手动创建的)在post-body-end.swig文件中添加如下内容:

```
<div>
    {% if not is_index %}
        <div style="text-align:center;color: #ccc;font-size:14px;">-------------本文结束<i class="fa fa-hand-peace-o"></i>感谢您的阅读-------------</div>
    {% endif %}
</div>
```

### 侧边栏显示当前浏览进度

打开 themes/next-reloaded/_config.yml ,搜索关键字 scrollpercent ,把 false 改为 true
如果想把 top 按钮放在侧边栏,搜索关键字sidebar ,把 false 改为 true
![](https://pic.imgdb.cn/item/61fcc2ba2ab3f51d913a01eb.png)

### 右上角添加github入口

首先到GitHub Corners或者GitHub Ribbons选择自己喜欢的图标,然后copy相应的代码
然后将刚才复制的代码粘贴到themes/next/layout/_layout.swig文件中下面一行
`<div class="headband"></div>`
把代码中的href后面的值替换成你要跳转的地址,比如你的GitHub主页

### 隐藏网页底部的Hexo驱动,next主题链接,next版本信息

打开主题配置文件,搜索关键字copyright

``` yaml
copyright:
 # -------------------------------------------------------------
 # Hexo link (Powered by Hexo). 
 powered: true #将true改成false,隐藏Hexo驱动

 theme:
   # Theme & scheme info link (Theme - NexT.scheme).
   enable: true  #将true改成false,隐藏next主题链接
   # Version info of NexT after scheme info (vX.X.X).
   version: true  #将true改成false,隐藏next版本号信息
```

### **添加搜索功能**

* 站点目录下,下载hexo插件

`npm i --save hexo-wordcount`

![](https://pic.imgdb.cn/item/61fcc5702ab3f51d913d1b70.png)

* 打开Hexo的配置文件,添加配置

``` yaml
search:
  path: search.json
  field: post
  format: html
  limit: 10000
```

![](https://pic.imgdb.cn/item/61fcce402ab3f51d9146a34f.png)

* 打开next的配置文件,搜索关键字local_search,设置为true
![](https://pic.imgdb.cn/item/61fcc6702ab3f51d913e341d.png)

### **设置博客摘要显示**

![](https://pic.imgdb.cn/item/61fcc6eb2ab3f51d913ebafd.png)

对于摘要显示,首先我们需要开启摘要功能,修改主题配置文件,打开阅读全文按钮

``` yaml
# Automatically excerpt description in homepage as preamble text.
excerpt_description: true

# Read more button
# If true, the read more button will be displayed in excerpt section.
read_more_btn: true #显示阅读全文按钮
```

![](https://pic.imgdb.cn/item/61fcc7572ab3f51d913f2fae.png)

设置摘要方法参考 [这里](https://jiangding1990.github.io/2017/04/25/Hexo%E4%BD%BF%E7%94%A8NexT%E4%B8%BB%E9%A2%98%E8%AE%BE%E7%BD%AE%E4%B8%BB%E9%A1%B5%E6%98%BE%E7%A4%BA%E6%96%87%E7%AB%A0%E6%91%98%E8%A6%81%E6%96%B9%E6%B3%95/)

### 头像与简介

*  **添加头像**
打开主题配置文件,搜索关键字avatar,将avatar前面的#号去掉
![](https://pic.imgdb.cn/item/61fcca112ab3f51d9142249b.png)

可以将本地头像复制到 themes/next-reloaded/source/images 目录下,或者使用网络链接

下面两个选项根据需求打开即可
分别为:
* 将头像显示为圆形
* 鼠标放到头像上会旋转

***最后,感谢您的观看,希望对您有所帮助!
有问题可以在下面联系到我:
https://t.me/Yini_Ruohong
andyzhao2005@163.com***

**本文参考资料与延伸阅读**
* https://zhuanlan.zhihu.com/p/78880987
* https://zhuanlan.zhihu.com/p/370635512
* https://monkeywie.cn/2020/08/20/fast-github-page-with-cloudflare/
* https://blog.tcpsoft.app/
* https://losophy.github.io/post/71afd747.html
* https://meowxue.gitee.io/2021/01/15/next%E4%B8%BB%E9%A2%98%E7%BE%8E%E5%8C%96/