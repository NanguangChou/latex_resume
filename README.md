# latex_resume
一个简单的Xelatex编译的简历模板

# 为什么使用XeLatex 和MacTex
又到了每年的9月10月的求职高峰季，填简历的时候看到一个非常充实又十分清爽的简历，可惜排版有些瑕疵，应该是word写的，于是自己开始折腾用Latex来制作一个风格相似的简历。并且在自己写resume的时候遇到的一些坑顺道一块记下来。

LaTeX 的简历模板其实是有不少的，坊间流传较广的有 [moderncv][1], 这货使用起来比较简单，样式改起来也很方便，但是不太适合作为一页纸简历模板，因为空白太多了。另外其他的一些模板要么不够简洁，引入的包太多，编译调试运行的时间就很长。另外一方面，由于原生latex对中文支持不够友好，刚开始尝试[CJK][2]，后来发现文档太少，tex论坛里交流的也不多。目前来说，结合 xeCJK 宏包使用 XeLaTeX 编译，应该是最方便的方式了。

CJK和Xelatex主要区别在引入的包和编译方式的不同：
``` latex
usepackage{CJK} % CJK方案+CJK包装的六套中文字体 
```
``` latex
usepackage{xeCJK} % 编译内核记得换成Xelatex
```

一开始用windows下的cTex套装，由于mikTex很久没更新，经常报错`undefined control sequence` 。后来实在找不到解决办法决定换成Mac桌面，加入中文字体过程快了很多。

XeLaTeX 要求 .tex 文档保存为 UTF-8 编码。所以要做的事情只有两件：

- 配置一个 UTF-8 的编辑环境；
- 用 xeCJK 的语法选择合适的字体。

参考知乎回答：[如何配置 MacTeX 的中文支持？][3]

# 使用xeLatex快速写个人简历

## 环境搭建
### Mactex+textStudio
mac环境直接下载完整版，比较新，关键是省掉自己下宏包的过程时间。熟悉WinEdit的同学建议用TexStudio，开源多平台，Linux下也可以使用，关键是右侧栏预览的功能可以提升效率。秒杀**texShop**和**SublimeText**。
**MacTex下载地址**[http://www.tug.org/mactex/](http://www.tug.org/mactex/)
**TexStudio 下载地址** [https://sourceforge.net/projects/texstudio/](https://sourceforge.net/projects/texstudio/)
![TexStudio界面](http://img.blog.csdn.net/20170904104508011?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXdvcDQ0Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### 导入头文件，预处理

``` latex
\documentclass{resume}
\usepackage{xltxtra,fontspec,xunicode}
\usepackage[slantfont,boldfont]{xeCJK} % 允许斜体和粗体
\usepackage{tabularx}
\usepackage{zh_CN_fonts_internal} % Simplified Chinese Support using system fonts
\usepackage{titlesec}
```

### 选择中文字体

``` latex
\setCJKmainfont{STHeitiSC-Light}   % 设置缺省中文字体
\setCJKmonofont{STHeitiSC-Light}   % 设置等宽字体
\setmainfont{ArialMT}   % 英文衬线字体
\setmonofont{Monaco}   % 英文等宽字体
```
这里已经打包成一个`.sty` 文件

### 表格排版 tablurx
宏包`tabularx` 增强了标准LaTeX制表环境`tabular*` 的功能，它能根据表格的总宽度自动计算特定表格列的宽度。`tabular*`环境与tabularx环境的主要区别在于:

- `tabularx`环境改变列的宽度，而`tabular*`环境改变列与列之间的空白宽度。
- `tabular*`环境与`tabularx`环境都可以嵌套使用。但是`tabularx`环境嵌套使用时，内部表格必须包含在一对花括弧{}之中。

[官方文档地址][4]
格式：

``` latex
\begin{tabularx}{hwidthi}[hposi]{hpreamblei}
```
样例：

``` latex
\begin{tabularx}{300pt}{|c|X|c|X|} 
```
输出结果：
![这里写图片描述](http://img.blog.csdn.net/20170904131401272?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXdvcDQ0Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


### fontawesome 图标库使用 
fontawesome是一套开源图标字体，使用这些字体可以免去插入图标图片的动作，通过代码就可以解决。
要求：

- 本地有fontawesome字体安装 (下载地址 `.otf`  [这里][5]).
-  你需要有 `XeLaTeX` 编译环境 和`fontspec` 包

使用：

- 下载 `fontawesome.sty` 并放在相同的tex文件夹目录下
- `\usepackage{fontawesome}`
- 通过\fa{大写图标名} 来引用图标。图标名转换规则可以在[这里][6]查看。example: \faGroup\ 

## 完整代码

- resume.tex 主文件
- resume.cls 格式文件
- fontawesome.sty 图标格式文件
- zh_CN_fonts_internal.sty 中文字体选择

项目已经开放在[我的github][7]上

输出：
![这里写图片描述](http://img.blog.csdn.net/20170904134207373?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXdvcDQ0Ng==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 其他简洁简历(由此启发)：

- [billryan/resume](https://github.com/billryan/resume/tree/zh_CN)
- [使用Latex/Tex创建自己的简历。](http://www.cnblogs.com/aoaoblogs/archive/2013/01/24/2874595.html)
- [JianXu's CV](http://www.jianxu.net/en/files/JianXu_CV.pdf)
- [Web Front-End Wenli Zhang.pdf](http://zhangwenli.com/cv/Web%20Front-End%20Wenli%20Zhang.pdf)
- [paciorek's CV/Resume template](http://www.stat.berkeley.edu/~paciorek/computingTips/Latex_template_creating_CV_.html)
- [How to write a LaTeX class file and design your own CV (Part 1) - ShareLaTeX](https://www.sharelatex.com/blog/2011/03/27/how-to-write-a-latex-class-file-and-design-your-own-cv.html)



## License

[The MIT License (MIT)](http://opensource.org/licenses/MIT)

Copyrighted fonts are not subjected to this License.

## 总结

\LaTeX 的中文支持除了在系统配置文件内指定外还可以在当前项目内指定，这种方式适合大范围分发，正是这个模板中采用的方式，缺点就是大部分中文字型都是有版权的，使用上需要注意。在制作这个模板的过程中还发现合理使用 \LaTeX 现代宏包能大大减轻后期维护和升级的工作，需要使用的命令更少更清晰。ShareLaTeX 网站上有很多简单易懂的范例，当教材来使都不过分。\LaTeX 中文方面的教程精品的不多，刘海洋老师的《LaTeX 入门》 算是精品中的精品！

总的来说这个模板适合找工作用，而且是偏技术型的一页纸简历。


-------
[1]:https://github.com/xdanaux/moderncv
[2]:https://en.wikipedia.org/wiki/CJK_characters
[3]:https://www.zhihu.com/question/22906637/answer/32816910
[4]:http://ctan.mirrors.hoobly.com/macros/latex/required/tools/tabularx.pdf
[5]:https://github.com/FortAwesome/Font-Awesome/blob/master/fonts/FontAwesome.otf?raw=true
[6]: https://github.com/plorcupine/latex-fontawesome
[7]: https://github.com/NanguangChou/latex_resume
