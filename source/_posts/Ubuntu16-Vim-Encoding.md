---
title: 如何解决Ubuntu下系统中文乱码及Vim编辑器中汉字乱码问题?
description: 在Ubuntu 16 和item2终端的环境下，遇到了Ubuntu中文乱码和Vim编辑器中的汉字乱码问题。VIM乱码修改当前的.vimrc后显示正常，item2则修改~.zshrc后显示正常。
---

# 首先看Vim编辑器内的中文乱码问题
Google 了一下，VIM显示中文会乱码可能是由于4个原因引起的：
1. Encoding: Vim 内部使用的字符编码方式，包括 Vim 的 buffer (缓冲区)、菜单文本、消息文本等。用户手册上建议只在 .vimrc 中改变它的值，事实上似乎也只有在 .vimrc 中改变它的值才有意义。
2. Fileencoding: Vim 中当前编辑的文件的字符编码方式，Vim 保存文件时也会将文件保存为这种字符编码方式 (不管是否新文件都如此)
3. Fileencodings: Vim 启动时会按照它所列出的字符编码方式逐一探测即将打开的文件的字符编码方式，并且将 fileencoding 设置为最终探测到的字符编码方式。因此最好将 Unicode 编码方式放到这个列表的最前面，将拉丁语系编码方式 latin1 放到最后面。
4. Termencoding: Vim 所工作的终端 (或者 Windows 的 Console 窗口) 的字符编码方式。这个选项在 Windows 下对我们常用的 GUI 模式的 gVim 无效，而对 Console 模式的 Vim 而言就是 Windows 控制台的代码页，并且通常我们不需要改变它。        


在知乎（[https://www.zhihu.com/question/22363620][1]）上找到的一个回答，编辑\~vimrc后解决了这个问题。

1. 设置\~下的.vimrc文件，加上fileencodings、enc、fencs，代码如下：
````
set fileencodings=utf-8,gb2312,gb18030,gbk,ucs-bom,cp936,latin1        
set enc=utf8        
set fencs=utf8,gbk,gb2312,gb18030       
````

2. 打开py文件检查一下中文字符是否正常显示


照这个操作后已经能正常显示。
# 再看Ubuntu 16下，ls显示所有文件中文会乱码的问题
参考[https://www.cnblogs.com/qiuxiangmuyu/p/6385528.html][2]
1. `cat /usr/share/i18n/SUPPORTED` 查看系统支持的字符集，是否包含  
	````
	zh\_CN.GB18030 GB18030  
	zh\_CN.GBK GBK  
	zh\_CN.UTF-8 UTF-8  
	zh\_CN GB2312  
	````
2. `vim /var/lib/locales/supported.d/local` 打开系统字符集配置文件，将支持的中文字符集添加进去，格式如1中得到所示
3. `locale-gen` 更新。如果2中添加正确应该没有问题，如果出问题再次编辑2，后再3直至解决。

此时乱码依旧存在，再参考[https://segmentfault.com/q/1010000002426378][3]，在item2 中，输入：  
````
vim ~/.zshrc
export LC\_ALL=en\_US.UTF-8
export LANG=en\_US.UTF-8
````

重启终端或者输入：
``
source ~/.zshrc
``

大功告成。

[1]:	https://www.zhihu.com/question/22363620
[2]:	https://www.cnblogs.com/qiuxiangmuyu/p/6385528.html
[3]:	https://segmentfault.com/q/1010000002426378
