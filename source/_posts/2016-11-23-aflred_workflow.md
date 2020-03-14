---
layout: post
title: Alfred Workflow教程与实例
date: 2016-11-24
categories: 教程
---

小帽子 [Alfred](https://www.alfredapp.com) 作为 macOS 上的最佳效率软件应该没太大争议([排名](https://github.com/hzlzh/Best-App))，而其中最强大的部分即为 Alfred 2.0 推出的[Workflow](https://www.alfredapp.com/workflows/)特性；其允许你将日常重复性的工作使用脚本语言(目前支持：bash, zsh, php, python, ruby, perl, osascript(AppleScript, JavaScript))封装起来，以 Alfred 作为统一的入口和呈现来使用，大大提高效率；本文将对其开发的一般流程进行讲述，并最终实现两个实例：

> - `CDto`: 打开 Terminal 并转到任意文件夹或文件所在目录，使用 _bash+osascript_ 实现 [点此下载](https://raw.githubusercontent.com/stidio/Alfred-Workflow/master/CDto.alfredworkflow)
>
> - `Effective IP`: 查询本机和外网 IP 地址，解析任意 URL 和域名的 IP 地址，同时进行归属地和运营商查询，使用 _python_ 实现 [点此下载](https://raw.githubusercontent.com/stidio/Alfred-Workflow/master/Effective%20IP.alfredworkflow)

本文源代码地址：[https://github.com/stidio/Alfred-Workflow](https://github.com/stidio/Alfred-Workflow)，如果喜欢请[Star!](https://github.com/stidio/Alfred-Workflow)，谢谢!

### 概述

Alfred Workflow 的整体架构，极度类似于 Windows 中的 Direct Show，首先由一个 Input 开始，中间经过一堆 filter，然后到一个 Output 结束，中间通过 Pin 连接，上一个 Output Pin 作为输入传递给下一个 Input Pin，从而形成一个完整的 Graph，而最终传递给 Alfred 做输出呈现的内容必须符合下面的形式：

> ```xml
> <?xml version="1.0" encoding="utf-8"?>
> <items>
>     <item valid="yes">
>         <title>10.0.2.11</title>
>         <subtitle>45.76.65.119 美国新泽西州皮斯卡特维 choopa.com</subtitle>
>         <icon>Info.icns</icon>
>     </item>
> </items>
> ```
>
> Alfred 上每一行显示对应一个*item*，如果显示多行，那就在*items*下放入多个*item*即可
>
> - _valid_ 表现为可不可以选择，点击，再次传递
> - _title_ 主标题
> - _subtitle_ 副标题
> - _icon_ 图标

### 开发准备

1. 使用[Option+空格]调出 Alfred，输入 alfred 打开 Alfred Preferences:

2. 点击 Workflows 按钮，然后点击最下面的 **+** 按钮，创建一个 Blank Workflow，按照提示填入信息:

   > **Bundle Id** 作为该 Workflow 的标识为必填内容，如果不填或与其他重复，有可能造成其不能正常运行

### Workflow - CDto

使用 Terminal 的一般步骤大概是运行 Terminal，然后一路 cd 到目标文件夹后开始使用；虽然 Finder 有 cd to 插件，但也需要你一路点到指定文件夹后，才能调起来；虽然 Alfred 的 Right Arrow 按键里面有 Open Terminal Here 操作，但排在太后面了，打开的操作路径至少需要：Right Arrow -> 输入 o -> [Command + 3]三步才能完成:

作为一个需要频繁和 Terminal 交互的码农这完全不能忍，下面我们就利用 Workflow 做个一步到位的 CDto 神器

1. 在 Alfred Workflows 的工作区点右键，选择菜单[Inputs -> File Filter]，并按下图设置好，其他两个选项卡使用默认设置即可:

2. 在刚才插入的[File Filter]上点击右键，选择菜单[Insert After -> Actions -> Run Script]，并按照下图设置好，最下面的 Escaping 表示对指定字符进行转义，比如说:/Users/$a1，如果不对$转义，那外部会把\$a1 一起当做一个变量，而这个变量未定义也就是为空，传递进来的参数最终变成:/Users/，[点此查看代码](https://github.com/stidio/Alfred-Workflow/blob/master/CDto/cdto.bash):

### Workflow - Effective IP

现在我们使用 Python 来做个更复杂的例子，[点此查看源码](https://github.com/stidio/Alfred-Workflow/blob/master/Effective%20IP/effectiveip.py)，具体分析见下图:

我们基于[Full-featured python library for writing Alfred workflows](https://github.com/deanishe/alfred-workflow/)进行开发，具体的内容请参考前面的内容和[官方教程](http://www.deanishe.net/alfred-workflow/tutorial_1.html), 这里我只对两个设置界面进行必要的解释：

1. 主设置界面

   > 1. 直接输入 ip 无参形式是查询本机的本地和公网地址，有参形式是进行 DNS 解析，因此参数是可选的，需要设置为：[Argument Optional]
   > 2. 点击 Run Behaviour 按钮，进行运行行为设置

2. 运行行为设置

   > 1. 如果输入发生变化，我们肯定是希望得到之后的结果，因此我们需要即时结束掉之前的查询
   > 2. 在输入过程中不进行查询，Alfred 通过最后一个字符输入延迟来判断输入结束后才进行查询

### 其他事项

> 1. 左边列表区域里点右键选择[Open in Finder]可以打开该 Workflow 的目录进行文件查看和编辑
> 2. 点此可以调出调试窗口，查看调试信息

### 参考资料

[神兵利器 — Alfred](http://macshuo.com/?p=625)  
[Alfred workflow 开发指南](http://myg0u.com/python/2015/05/23/tutorial-alfred-workflow.html)  
[JavaScript for OS X Automation by Example](http://developer.telerik.com/featured/javascript-os-x-automation-example/)  
[Full-featured python library for writing Alfred workflows](http://www.deanishe.net/alfred-workflow/)

<br/>

> [原始链接]({{page.url}}) 版权声明：自由转载-非商用-非衍生-保持署名 \| [Creative Commons BY-NC-ND 4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/deed.zh)
