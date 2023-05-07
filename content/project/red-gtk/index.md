---
title: 在deepin os 上面安装使用Red语言（调用GTK库）
summary: 本文基于red在2019-02-12时的版本，不确定是否适用于后续版本
tags:
  - deepin
date: 2019-02-12
#external_link: https://bbs.deepin.org/zh/post/174674
---

**本文基于red在2019-02-12时的版本，不确定是否适用于后续版本**

1. 先安装32位的gtk依赖，因为red的图形界面需要用到这个库（我用的是deepin15.9基于debian9.0）

在终端输入  （at-spi2-core, libgtk-3-bin 这两个库是必须的) :

```sudo apt-get install libgtk-3-bin:i386```

中途会询问你，输入y即可

![img](https://storage.deepin.org/forum/201902/12/225909cz0vuj38f6xczfxe.jpg)

2. 然后去下载rebol的core文件（用rebol文件去编译出red的GUI）

www.rebol.com/downloads/v278/rebol-core-278-4-3.tar.gz

解压之后会有一个releases文件夹，打开rebol-core文件夹，把rebol文件复制到步骤3的文件夹中去

![img](https://storage.deepin.org/forum/201902/12/225952wzspv5v75nc56b06.jpg)

3. 下载red语言的非官方GTK+分支https://github.com/rcqls/red/tree/GTK

我已经打包好了上传，方便你们，可以不用再去下载了

4. 把步骤2的rebol文件复制到解压出来的red-GTK文件夹中

5. 此时，开始要在red-GTK打开终端，（假如终端打开的路径不对或者不清楚可以用cd命令或者pwd命令）

修改`environment/console/CLI/console.red` 文件 用编辑器打开在 Red [] 区块里面输入`Needs: View `（注意冒号后面必须要有空格）

`console-view.red`文件也是加入同样的代码`Needs: View `（注意冒号后面必须要有空格）

![img](https://storage.deepin.org/forum/201902/12/230031al1x717us5271120.jpg)

终端输入`./rebol   `

如图显示即为成功运行rebol

![img](https://storage.deepin.org/forum/201902/12/230116su3gdddz44n4pu5n.jpg)

输入` do/args %red.r "-r %environment/console/CLI/console.red"`

![img](https://storage.deepin.org/forum/201902/12/230153qmlnu7sm5jsu4zpn.jpg)

如上图显示即为编译red语言控制台成功

6.接着就可以运行red-GTK目录下的（建议先打开终端在输入运行./console）

![img](https://storage.deepin.org/forum/201902/12/230311pd2naxwwa2dccj1r.jpg)![img](https://storage.deepin.org/forum/201902/12/230311eyeyaew3qe6i6qew.jpg)![img](https://storage.deepin.org/forum/201902/12/230312qdatn4yyd24t4a8q.jpg)





出现一个警告，什么意思我也不是很清楚，有知道的可以告诉我一下，先来测试一下是否安装成功

输入`view [button "hello world "]`

![img](https://storage.deepin.org/forum/201902/12/230405jsjzzlhj8wiicttl.jpg)

安装成功！

---

2019.02.14

进入并运行/usr/lib/x86_64-linux-gnu/gdk-pixbuf-2.0/gdk-pixbuf-query-loaders 这个可执行文件，貌似警告就取消了，大家可以试一下，反馈给我。

---

有个疑问为什么word里面编辑好的图文直接复制不能粘贴到论坛编辑框里面自动上传生成图片，我一张一张上传超级累。。。。。

[rebol-core-278-4-3.tar.gz](https://storage.deepin.org/forum/201902/12/230828q566w9aw5aa9bgyg.attach)