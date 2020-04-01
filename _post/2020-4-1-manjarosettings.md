---
published: true
title: Setting After Manjaro Gnome Installed
category: Linux
tags:
- Manjaro
layout: post
---

# Manjaro Gnome安装后的配置

> 注：本文首发于本人知乎账号，故而图片水印上带有“知乎”字样，[阅读原文](https://zhuanlan.zhihu.com/p/64799118)

**2020.3.5更新：关于WPS安装后菜单栏为英文的问题**

正常安装WPS完毕后，如果WPS菜单栏显示为英文，在终端安装WPS中文语言包可以解决问题：

```bash
sudo pacman -S wps-office-mui-zh-cn
```

<hr>

**2020.2.9更新：**

我文章前言里写的那个所谓中国论坛已经挂了，现在变成某野鸡论坛。**大家下载Manjaro镜像的时候请去官网下载**。网址戳[Here](https://manjaro.org)

如果硬件资源足够的话，我还是推荐gnome和KDE这两个版本的，界面友好，而且不需要过多配置。如果是老手的话请随意。

另外，关于**Manjaro KDE 18.1.5**版本安装TIM的问题。除了要执行本文“Manjaro安装必备软件 → QQ&TIM”描述的步骤外，还需要增加一个步骤，具体方法戳[Here](https://www.jianshu.com/p/05f6d277eaae)

<hr>


## 前言（废话）

我试过目前市面上较多个Linux系统的发行版，包括Ubuntu、CentOS等。最近看见有人推荐使用另一个Linux的发行版Manjaro，于是随性所至，去了它的官网上瞧了几眼。没想到中文论坛的标题异常惊悚——号称世界排名前二！

![](imgs/manjaro1.jpg)

虽然我很想知道排名第一的到底是谁，但是现在还是先把注意力放在Manjaro本身吧！

## Manjaro的下载和安装
### 下载
Manjaro的下载非常方便，因为它有中文的论坛，包含中科大和清华大学在内的国内镜像站。你可以很方便得找到Manjaro系统的iso镜像。百度Manjaro就可以找到它的官网和中文论坛。

![](imgs/manjaro2.jpg)

值得一提的是，中文论坛上提供了3个不同的桌面系统——尽管他们都是Manjaro。它们唯一的区别应该只是桌面环境的不同。这三个桌面系统是：

- Manjaro Xfce版：Xfce是一个用于类UNIX操作系统的轻量级桌面环境。 它的目标是快速和系统资源低耗，同时仍然保持视觉上的吸引力和对用户友好的特性。
- Manjaro KDE版：KDE是一个功能丰富多样的桌面环境，提供几种不同风格的菜单来访问应用程序。还有一个优秀的内置界面，可以方便地访问、下载、安装新的主题、小部件等。 虽然在用户友好度上做的非常好，但KDE也是相当消耗系统资源的，跟XFCE比较起来，启动程序、使用桌面环境都明显偏慢。运行Manjaro的64位KDE桌面使用大约需要550MB的内存。
- Manjaro GNOME版：GNOME桌面环境是作为GNU项目的一部分来开发的，它旨在简单易用，并且完全可用。 它的默认显示服务器是Wayland。 虽然外观是独特的，它的可定制性仍然非常高。各种扩展可以从[here](https://extensions.gnome.org/)获取。像KDE一样，它比Xfce使用更多的资源。

因为我有过Ubuntu的使用经验，而Ubuntu18.04使用的是GNOME桌面，因此我选择的是Manjaro GNOME版。在这里我也推荐使用GNOME桌面。下载好后即可使用。

### 安装
我是选择的是在虚拟机VMware上安装，和其他系统的安装过程一样。

如果你想装双系统，可以去找找教程，这里我就不再赘述了。因为毕竟都是分区啥的。

### Manjaro的配置和更新
安装好Manjaro后，有些提前的工作需要做一下。

第一就是更换**国内源**。由于Manjaro默认使用国外的更新地址，如果直接拿来就更新系统和软件的话，那速度不可不谓爽歪歪。

打开终端，输入命令：
```bash
sudo pacman-mirrors -i -c China -m rank
```

这是系统会对国内的镜像进行测速，并在弹出窗口中列出

![](imgs/manjaro3.jpg)

虽然这里显示上海交大的镜像延迟最低，但我还是勾选了中科大的镜像。然后点击OK。

刷新缓存，这时你会发现下载速度何止鸟枪换炮，简直是鸟枪换神舟七号。
```bash
sudo pacman -Syy
```

但是还没完，你还需要添加一下ArchLinuxCN的源。终端输入：
```bash
sudo gedit /etc/pacman.conf
```
**注意**：由于我使用的是GNOME桌面，因此我使用的编辑器是gedit。如果你使用的是Manjaro的其他桌面版本，那么你的系统可能没有gedit，而是nano，或者vim也行。

在打开的文件末尾添加如下内容：
```txt
[archlinuxcn]
SigLevel = Optional TrustedOnly
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
```

同样，在这里我选择的是中科大的源。这里提醒一下诸位，我曾经在这里使用过其他的源，但是好像不太能行。不过我很确定这里使用中科大的源没有问题。所以各位尽量使用中科大的源。这里和之前的那个镜像不需要完全匹配，可以各管各的！

修改好上述两个部分后，终端执行下面的指令：
```bash
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring
```

这一步是为了更新缓存以及导入密钥链。

**注意**，你在执行更新命令时可能会报错，这时你需要再执行一遍。我也不知道这是什么神仙bug，可能是网络问题吧！
```bash
sudo pacman -Syyu
```

![](imgs/manjaro4.jpg)

这个命令不仅是更新系统，而且也更新软件包。可以看到更换为国内源后下载速度非常之快，我的可以达到7m/s。

如果你要安装某个软件，终端输入
```bash
sudo pacman -S [name]
```

最后重启系统。至此Manjaro的配置和更新算是完成了。

## Manjaro安装必备软件
### 中文输入法
作为中华人民共和国的公民，我们都需要一个好用的输入法。据我所知，在Linux下可用的有搜狗输入法等。但是考虑国内的互联网公司时不时的流氓行径，这里不推荐使用搜狗。可以试试谷歌中文输入法和RIME输入法。这里我使用的是RIME输入法。

安装过程很简单，在终端依次执行下列命令：
```bash
sudo pacman -S fcitx-rime
sudo pacman -S fcitx-im
sudo pacman -S fcitx-configtool
```

然后你需要编辑一个文件
```bash
sudo gedit ~/.xprofile
```

注意：我使用的编辑器是gedit。

在文件末尾添加如下文本：
```txt
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"
```

改好后建议重启一下系统。

点击桌面右上角出现的小键盘，然后点击“配置当前输入法”。

![](imgs/manjaro5.jpg)

![](imgs/manjaro6.jpg)

通过下方的+、-和箭头，将“中州韵”汉语输入法添加进列表并置于最上端。其他的输入法可以使用减号移走。

不过安装RIME的小伙伴可能会惊奇地发现，RIME输入法输出的字体是繁体字！切换为简体字非常简单，只需按下F4，然后选择简体字方案就好了。

### 代码编辑器：VSCode

当然啦，既然你已经开始使用Linux系统，那我真的不得不默认你和我一样都是不得不将996当作福报的程序员。那么一个好用的代码编辑器绝对是必需品。

这里我使用的是巨硬出品的开源编辑器Visual Studio Code。这一款编辑器的优点真的不需要我多说些啥了。反正用过的人都说好。终端输入：
```bash
sudo pacman -S visual-studio-code-bin
```

话说回来，如果是喜欢用IDE的同学，那么在Linux下你肯定是逃不过Jet brains的全家桶的。安装也非常简单，输入IDE的名字就行了。以安装CLion为例（CLion较特殊，其他的都是直接输入名字，CLion是还需安装特定的cmake和一个库）：
```bash
sudo pacman -S clion clion-cmake make clion-lldb
```

### Google Chrome
```bash
sudo pacman -S google-chrome
```

### Lantern
```bash
sudo pacman -S lantern
```

### Markdown编辑器：Typora
虽然VSCode可以满足markdown文档的编辑。但是我觉得不太好用。还是Typora给力。
```bash
sudo pacman -S typora
```

再一次提醒，如果安装中出现错误，如果确定命令没有打错，再执行一遍命令就可以解决问题。这个神仙bug在我写这个笔记的时候出现了无数次。。。

### QQ & Tim
安装QQ：
```bash
sudo pacman -S deepin.com.qq.im
```

安装Tim：
```bash
sudo pacman -S deepin.com.qq.office
```

### WPS

虽然Manjaro自带Microsoft Office Online，但是这个软件只有联网的时候才能用，而且office online在国内的服务貌似有点问题，长期报错。我还是比较推荐大家使用金山出品的WPS，而且现在已经更新到WPS2019了，UI和以往完全不同，看起来非常舒服。执行下面2步即可安装WPS：
```bash
sudo pacman -S wps-office
sudo pacman -S ttf-wps-fonts
```