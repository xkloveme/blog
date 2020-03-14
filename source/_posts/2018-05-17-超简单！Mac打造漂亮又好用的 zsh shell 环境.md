---
title: 超简单！Mac打造漂亮又好用的 zsh shell 环境
tags:
  - 技术
  - 工具
date: 2018-05-17 08:16:48
---

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/QQ20180517-1@2x.png)身为开发者，很大一部分的时间是在用 command line 做事，如果能把 command line 调整成好用又酷炫的模样，不只是效率提升非常多，用起来爽度也比较高,上面放了一张我自己的 item，是不是觉得高大上了许多

- 本片文章适用于 MAC 开发的 developer，学习时间大概十分钟
- shell 默认选中 ZSH，已经安装过**iTerm2，oh-my-zsh**
- 避免搞乱你的开发环境：仅可能使用 homebrew 来安装需要的套件
- 安装 zsh theme: **powerlevel9k**

#### **安装 iTerm2：**

虽然不是必要，内建的 Terminal app 也可以，不过 iTerm2 还是比较好用，下面的示范也全都是用 iTerm2,个人用的自带其实还好

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/QQ20180517-3@2x.png)

#如果你从来没有用过 brew cask 的话需要先跑这行
brew tap caskroom/cask

#安装 iTerm2
brew cask instal iterm2

安装好以后，打开 iTerm2 检查 Report Terminal Type 的设置，路径： `Preferences > Profiles > Terminal > Report Terminal Type`

设为`xterm-256color`，等等在 terminal 才能看得到漂亮的颜色

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/QQ20180517-5@2x.png)

#### **修改 iTerm2 的 color scheme**

这步骤很重要，预设的很丑，想要自己的 command line 看起来赏心悦目就绝对要换掉预设的

![](http://www.jixiaokang.com/wp-content/uploads/2018/05/QQ20180517-4@2x.png)

#### **安装 powerline font**

因为我们要用的 theme 会用到很多的特殊 icon，所以 iTerm2 选用的字型必需要支援这种特殊 icon font。这类型的字体统称为 powerline font（另外还有加强版支援更多特殊 icon 的叫的 nerd font）

没有安装的话画面会长这样，遇到 icon 会变框框问号

![](https://cdn-images-1.medium.com/max/1600/1*sB3u7_aAXl6BkRy9UEygPw.png)

非 powerline font

装完并设定新字型后的效果：

![](https://cdn-images-1.medium.com/max/1600/1*0lPAd28LbancmQuHgnDyNg.png)

powerline font

支援 powerline 的字型很多，我推荐**Sauce Code Pro Nerd Font Complete** 安装方式推荐直接用 brew 安装比较快又好管理

安装指令：

#先执行这行，才能用 homebrew 安装字型。曾经执行过的人可以跳过这个指令
brew tap caskroom/fonts

    # 安裝指令
    brew cask install

如果想要装别的，brew 上面也有很多字型可以挑。

关键字是`nerd`：

brew cask search nerd

装完后，记得修改 iTerm2 字型设定否则不会生效。请改成 SauceCodePro Nerd Font 或你自己下载的字型

设定路径：`Preferences > Profiles > Text > Change Font`

#### **安装 oh-my-zsh**

上一步装完 zsh 后，就可以开始调整我们想要的 command line 外观设定了，但是原始的 zsh 因为设定太难搞，所以多年前刚出现的时候没有受到太多关注，直到有人写了一套叫**oh-my-zsh**的 framework 来帮助大家使用 zsh，zsh 才火了起来。现在几乎所有 zsh 好用的工具都有支援 oh-my-zsh，所以当然是要装这东西

安装指令：

    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

> 注：这会直接执行 oh-my-zsh 的有疑虑的人可以先稍微研究一下[oh-my-zsh github](https://github.com/robbyrussell/oh-my-zsh)上的，觉得放心再执行`install.sh` `install.sh`

执行完以后如果没有出现什么错误讯息就代表成功了，同时会发现多了 oh-my-zsh 的资料夹  `~/.oh-my-zsh`

#### **重头戏！！安装 zsh theme **[**powerlevel9k**](https://github.com/bhilburn/powerlevel9k)

刚装完 oh-my-zsh 以后，预设是使用内建的 theme *robbyrussell*，多了 git 资讯，颜色也看起来比原生 bash 好一些：

![](https://cdn-images-1.medium.com/max/1600/1*1TqBIUz998aoEAoepG4mbw.png)

不过 oh-my-zsh 内建很多 theme，在它的[github wiki](https://github.com/robbyrussell/oh-my-zsh/wiki/themes)上有很多截图可以参考

切换内建的 theme 很简单，直接修改你的`~/.zshrc`，把原本改成你想要的：`ZSH_THEME=”_robbyrussell_”`

    # 編輯 ~/.zshrc
    ZSH_THEME=”

任何的 zsh 设定修改过后，还要执行以下指令才会生效

exec \$SHELL

![](https://cdn-images-1.medium.com/max/1600/1*Dj2trYBv3hgFg4LOIlMtWg.png)

agnoster 看起来是不是比 robbyrussell 漂亮多了？

这边推荐一个超强的 theme，powerlevel9k！

文章开头的图片就是撷取自[powerlevel9k 的 github](https://github.com/bhilburn/powerlevel9k)

![](https://cdn-images-1.medium.com/max/1600/1*OwwhfTqbc8IUaZnCAYXt7g.gif)

图片来源：[https://github.com/bhilburn/powerlevel9k](https://github.com/bhilburn/powerlevel9k)

powerlevel9k 不只是像上面的示范图显示一些基本的资讯，还可以做到很屌的事情，比如像下图那样，显示 WiFi 讯号强度、笔电电池电力、CPU loading、system free memory 等等资讯在 command line

![](https://cdn-images-1.medium.com/max/1600/1*Ixhmm4KVixyzZolr-OTV3w.png)

图片撷取自[powerlevel9k github](https://github.com/bhilburn/powerlevel9k)

#### powerlevel9k 安装方式：

1.  [powerlevel9k](https://github.com/bhilburn/powerlevel9k)不是 oh-my-zsh 内建的 theme ，必须另外下载

指令：

    git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

2.编辑你的`~/.zshrc`，把 ZSH_THEME 设为 powerlevel9k，并设定要显示哪些东西在 command line 上：

    ZSH_THEME="powerlevel9k/powerlevel9k"

\# command line 左边想显示的内容
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir) # <= left prompt 设了"dir"

\# command line 右边想显示的内容
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(time) # <= right prompt 设了"time"

上面的例子我们把左边设了一个`dir`，右边设了`time`，代表左边想显示当前资料夹路径，右边显示时间

设定完后 command line 看起来会像这样(记得执行`exec $SHELL`，设定才会生效)：

![](https://cdn-images-1.medium.com/max/1600/1*MY6xGaUv0ksJni-EbeOZQg.png)

左边显示当前资料夹路径，右边显示时间

---

如果想要有版本控制的资讯，可以在`POWERLEVEL9K_LEFT_PROMPT_ELEMENTS`加上`vcs`(vcs 为 version control system 的缩写)

    # 編輯 ~/.zshrc
    POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir vcs) # 加上 "vcs"

command line 会变这样：

![](https://cdn-images-1.medium.com/max/1600/1*BrzqzPH-XOjywfbIekAzEQ.png)

多了 git branch 以及 git status 资讯

---

当你进入了一个没有写入权限的资料夹时还可以给你提醒：

#加上"dir_writable"
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir **dir_writable** vcs)

![](https://cdn-images-1.medium.com/max/1600/1*BYW3MIbGBv9DXzNU72JFKQ.png)

/etc 没有写入权限，多出一个锁头提醒你

---

如果你的 command line 是设成 vi mode ，相信你一定碰过这个困扰，就是不晓得自己是处在 normal mode 还是 insert mode。没关系，powerlevel9k 可以帮你解决这个问题：

#加上"vi_mode"
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir dir_writable vcs **vi_mode** )

结果如下：

![](https://cdn-images-1.medium.com/max/1600/1*bj90M9RvPCFZ6GNVqJUP4g.png)

上图告诉我们现在在 insert mode

按下`ESC`后：

![](https://cdn-images-1.medium.com/max/1600/1*PCsqH7xDf3z4lXCr81QV0A.png)

告诉你变 normal mode 啦~赞吧！

---

我自己习惯左侧的设定放一些常用基本资讯 右边放一些好用但不是每次下指令都要看的东西

command line 右边的设定放在  `POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS`

例如显示上一个指令的 return code：

#加上"status"显示上一个指令的 return code：
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=( **status** time)

如果指令没出错，linux return code 为 0 时会有个绿色小勾勾：

![](https://cdn-images-1.medium.com/max/1600/1*nSS8Df1YlCwI87ICv_jM_Q.png)

指令正确执行，return code 为 0

如果打了错误指令会出现相对应的 return code，并且用红色底色提醒你

![](https://cdn-images-1.medium.com/max/1600/1*DSV5vY-pzNOVcv4jaI-4Wg.png)

指令执行错误，return code 为 127

---

还可以显示目前电脑的 free memory：

#加上 ram，显示目前的 free memory
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status **ram** time)

![](https://cdn-images-1.medium.com/max/1600/1*tgWdaWPdLSn8LMharCTOYQ.png)

还有 4.61G 的记忆体可用

**2017/12/30 更新： 上图的最左方有个资料夹 icon，且 git 资讯多显示了几个 icon，这用原本的设定是看不到的，需要加上这行：**

    POWERLEVEL9K_MODE='nerdfont-complete'

[powerlevel9k 的 wiki](https://github.com/bhilburn/powerlevel9k/wiki/Install-Instructions#option-4-install-nerd-fonts)有解释这个设定的作用，请大家使用时注意一下别忘记加上去

---

加上 CPU load average：

#加上 load 显示 CPU 忙碌程度
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status ram **load** time)

![](https://cdn-images-1.medium.com/max/1600/1*-j1gAm788RbWzRiY0MidCg.png)

CPU 忙碌程度 2.45，还行

显示电量：

POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=( **battery** )

![](https://cdn-images-1.medium.com/max/1600/1*48h7cUsjuzXBV8dhOjHehw.png)

还可以用 6 小时又 11 分

---

示范了不少，但还有非常非常多东西可以用，请参考这个列表自己玩玩看[https://github.com/bhilburn/powerlevel9k#available-prompt-segments](https://github.com/bhilburn/powerlevel9k#available-prompt-segments)

不过有些东西中看不中用，放太多东西也会让 command line 反应变慢，试了各种设定一阵子后，只留下了一些我觉得比较有用的，给大家参考：

#左侧
POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(context dir dir_writable vcs vi_mode)

#右侧
POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status background_jobs history ram load time)

#若当前登入的帐号为你的帐号 xxx，就不用特别显示出来
DEFAULT_USER="xxx"

    # 使用 nerd font 時可以顯示更多 icon。詳情請參考

---

#### 最后…

这篇文章介绍了怎么样把自己的 command line 替换成 zsh，并且使用很厉害的 powerlevel9k theme，不过 zsh 不只是可以换酷炫的 theme 而已，更重要的是还有很多比 bash 好用的功能可以大幅提升工作效率，又可以装各种方便的 plugin，就留待有机会时再介绍啰

---
