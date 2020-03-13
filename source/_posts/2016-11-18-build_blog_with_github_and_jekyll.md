---
layout: post
title: 使用GitHub Pages+Jekyll搭建个人博客
date: 2016-11-21
tags: [Jekyll, GitHub, 教程]
---

### 概述

![](/assets/build_blog_with_github_and_jekyll/01.jpg)

> **`GitHub Pages`** 免费无限容量的站点数据托管工具(_国内访问速度较慢_)，内置 Jekyll 服务，能将特定名称的代码仓库动态编译为静态网页
>
> **`Jekyll`** 基于 Ruby 的静态网页生成系统，采用模板将 Markdown(或 Textile)文件转换为统一的网页
>
> **统计** 统计工具主要是为了方便查看站点的访问情况，目前支持[百度统计](http://tongji.baidu.com)和[Google Analytics](http://www.google.com/analytics/)(可同时使用)
>
> **评论** 评论工具可以为静态页面增加评论和分享功能，目前支持国内的[多说](http://duoshuo.com)和国外的[Disqus](https://disqus.com)
>
> > _本文将重点介绍标注 `` 的必选项目，未标注的可选项目请按照给定地址自行注册即可_

### 建立 GitHub Pages 站点

1. 在 GitHub 上建立一个以 **_.github.io_** 为后缀的和你帐号名一样的代码仓库，如我的帐号是:[xkloveme](https://github.com/xkloveme)，则建立的仓库名为:[xkloveme.github.io](https://github.com/xkloveme/xkloveme.github.io), 同时在底部 Add .gitigore 选择 Jekyll 模板，这样 Jekyll 产生的临时文件，例如\_site 目录就不会添加到源代码管理中，当然你也可以以后手动配置:

   ![](/assets/build_blog_with_github_and_jekyll/02.jpg)

2. 将该代码仓库克隆到地:

   > ```sh
   > $ git clone https://github.com/xkloveme/xkloveme.github.io
   > ```

3) 创建一个测试页面并推送:

   > ```sh
   > $ cd xkloveme.github.io
   > $ echo "Hello World" > index.html
   > $ git add --all
   > $ git commit -m "Initial commit"
   > $ git push -u origin master
   > ```

4. 浏览器中输入[xkloveme.github.io](https://xkloveme.github.io)，如果一切正常，你应该能看到一个显示 Hello World 的页面.

> _请将以上的 **xkloveme** 替换为你申请的帐号名_

### 安装配置 Jekyll

1. 安装 Jekyll:

   > ```sh
   > $ gem install jekyll
   > ```

2. 创建或使用模板, 创建模板使用 _jekyll new **name**_ 命令，但创建出来的测试模板极其简陋，在这里我主要介绍使用第三方主题，在 [这里](http://jekyllthemes.org) 你可以找到各种主题，当然你也可以直接使用我的博客模板:[点击下载](https://github.com/stidio/stidio.github.io/archive/master.zip)，下载后解压到本地代码仓库目录，并运行 _bundle install_ 命令安装项目依赖包.

3. 运行 _jekyll serve_ 启动本地测试服务器，Jekyll 默认使用 4000 端口，如果被占用，可以使用 _jekyll serve -P \$PORT_ 指定其他端口，如果本机从没配置过 Jekyll，可能会给出 _cannot load such file -- bundler_ 的错误，运行 _gem install bundler_ 即可解决，如果还是出现包缺失的错误，可以从以下两点排查：

   > - Gemfile 文件未添加指定包
   > - 运行环境冲突，可以运行 _bundle exe jekyll serve_ 执行，或者运行 _sudo bundle clean --force_(**该命令会对全局环境造成影响，小心使用**) 强制清理无关包后重新运行

4. 在浏览器中输入 [127.0.0.1:4000](http://127.0.0.1:4000) 进行本地预览

> Ruby 包管理工具介绍
>
> - `gem` 全局包管理工具，类似于 Python 的 pip, Node.js 的 npm -g
>
>   - gem install 安装组件
>   - gem install -v 安装特定版本
>   - gem list 列出已经安装组件
>   - gem sources -a 添加源
>   - gem sources --remove 删除源
>
> - `bundle` 项目包管理工具，可以理解为一个独立的运行环境
>   - bundle update 更新项目依赖包
>   - bundle install 安装项目依赖包
>   - sudo bundle clean --force 强制删除不相关的包
>   - bundle exe 在指定环境中运行

### 使用我的博客模板

1. 按照注释说明修改 _\_config.yml_ 配置文件
2. 删除文章目录 _\_post/_ 和文章图片目录 _images/posts/_ 下面的所有内容
3. Enjoy!

我的模板在 [leopardpan](https://github.com/leopardpan/leopardpan.github.io) 基础上进行了修改，主要改进了以下内容:

> - 统一风格，给关于，标签页面添加了标题栏
> - 添加分割改进文章列表的多标签显示
> - 修正了一些翻译不全的文字
> - 代码颜色高亮支持，综合了 Pygments monokai 方案和 Rouge monokai.sublime 方案，[点此查看](/css/code_style_monokai.css)
> - 底部统计和版权排版对齐
> - 更新 Jekyll 及其依赖包到最新版本
> - 修正 jekyll-sitemap 加载失败的问题
> - 支持 GFM 形式的 Markdown Codeblock 解析

如果喜欢请[Star!](https://github.com/xkloveme/xkloveme.github.io)，谢谢!

### 编写文章

推荐

1. 国内在线 md 编辑工具[mdeditor](https://www.zybuluo.com/mdeditor)一款国内的在线 markdown 编辑器
2. 国外在线 md 编辑工具[stackedit](https://stackedit.io/)国外的在线 markdown 编辑器，功能强大，同步云盘国内用户不推荐速度稍慢
   文章为 Markdown 格式，请使用.md 作为后缀名，有以下两个文章目录：

> - `_posts` 文件名格式为：YEAR-MONTH-DAY-title.md
> - `_drafts` 草稿目录，文件名格式为：title.md，即不加日期前缀，如果需要预览草稿，使用 _\--drafts_ 选项运行 _jekyll serve_ 或 _jekyll build_
>
> **\* 尽量避免使用中文文件名, 具体目录结构请参考: [官方文档](http://jekyll.com.cn/docs/structure/)**

每篇文章都必须以参数：

> ```conf
> ---
> layout: post
> title: 使用GitHub+Jekyll搭建个人博客
> date: 2016-11-21 11:29:08 +0800
> tags: [Jekyll, GitHub, 教程]
> ---
> ```

作为头部信息，layout 为布局格式；title 为显示的文章名；date 为显示的发布日期；tags 为文章分类标签

文章正文采用 Markdown 编写，如果不熟悉可以查看: [Markdown 快速入门](http://wowubuntu.com/markdown/basic.html)；强烈建议遵循[Markdown Lint](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md)，规范有一些对书写文章不友好的地方，我做了调整，以下是我的[Visual Studio Code](https://code.visualstudio.com)的配置文件:

> ```json
> "markdownlint.config": {
>         "MD002": false,                                 // 禁用文章开头必须为H1标题栏
>         "MD001": false,                                 // 禁用严格的标题层级关系(H1->H2->H3...)
>         "MD003": { "style": "setext_with_atx_closed"},  // 允许#和===形式的标题风格混用
>         "MD009": { "br_spaces": 2 },                    // 允许末尾两个空格为<BR/>自动换行模式
>         "MD013": false,                                 // 禁用单行长度限制
>         "MD014": false,                                 // 禁用sh命令以 $ 作为开始
>         "MD038": false,                                 // 禁用代码不以空格作为开始或结束
>         "MD041": false,                                 // 禁用代码段必须有标题栏
>         "MD029": { "style": "ordered" }                 // 有序列表格式为顺序方式
>     }
> ```

Jekyll 的 Markdown 解释器从 3.0 开始，默认从 _redcarpet+Pygments_ 换为 _kramdown+Rouge_, 现在已知的问题为：列表下不支持 GFM 形式的代码块(神奇的是 Github 下的 README.md 文件支持)，折中的办法是使用区块引用(Blockquote)，在其下再使用代码块(我的博客模板已针对这种情况在呈现上做了优化)

### 参考资料

[Github 简明教程](http://www.runoob.com/w3cnote/git-guide.html)  
[Git 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)  
[Jekyll 英文文档](https://jekyllrb.com/docs/home/)  
[Jekyll 中文文档](http://jekyll.com.cn/docs/home/)  
[Jekyll 代码高亮的几种选择](http://blog.csdn.net/qiujuer/article/details/50419279)  
[Markdown 语法说明](http://wowubuntu.com/markdown/index.html)  
[Markdown Lint](https://github.com/DavidAnson/markdownlint/blob/master/doc/Rules.md)  
[kramdown Quick Reference](http://kramdown.gettalong.org/quickref.html)
