# Latex**相关资源汇总**

[TOC]

##  前言

Latex并不难，也不是艺术。Latex只是给Knowledge Engineer的一个撰文工具，仅此而已。一篇文章真正的价值在于里面的发现和思维逻辑，文本、图片、排版都只是形式。如果没有好的内容，做的再漂亮，也不会得到别人的认可。可是，形式很多时候也不可缺。大家都是俗人，都会喜欢美轮美奂的东西。好的形式可以帮助推销自己的论文。认同了这两点就可以开始下面的阅读。

## Latex简介

Latex排版软件和MS Word不同，不是“所见即所得”(WYSIWYG，what you is see what you get)，而是“所想即所得”(WYWWYG，what you want what you get)。风格上迥然不同，因此需要稍微改变一下自己的习惯。

TeX/LaTeX本质是一种制作文档的语言编译器，所以它有

- 源代码，后缀名.tex。
- 目标文件，后缀名.pdf。
- 编译临时文件，包括.dvi和.ps等。
- 编译工具集。包括TeX/LaTeX实现版本和版本号，比如[miktex](http://miktex.org/)-2.9。
- 编译路径。到达目标pdf文件，可能的编译路径有pdflatex、latex+dvipdfm(x)、latex+dvips+ps2pdf等。有时ps2pdf无法完成ps转换pdf，可以改用acrobat distiller。

| ![tex-workflow.jpg](http://fmn010.xnimg.cn/fmn010/blog/20080819/22/37/A663672558934CHA.jpg) |
| ------------------------------------------------------------ |
| 图. LaTex编译过程的workflow                                  |

在各种编译路径中，个人推荐pdflatex。因为这样编译遍数较少，还方便在pdf文档里面加bookmarks。但注意pdflatex缺省加载的图片格式是.pdf。所以尽量将所有图片转成.pdf格式(有个小麻烦psfrag用不了了)，而且.tex文件里面包含图片的时候别加后缀名。另外，pdflatex要配合新的pdf阅读器[sumatrapdf](http://blog.kowalczyk.info/software/sumatrapdf/free-pdf-reader.html)。因为acrobat reader打开一个pdf文件的时候会加锁，而且不会在文档修改过之后自动reload。最后，pdflatex最好配合natbib包的\citep{...}来做citations，否则citation过长容易跑到\columnwidth之外。

关于TeX(LaTeX)的学习，毫无疑问，Donald E. Knuth (高德纳)的《The TeX book》是权威之选，本书排版堪称完美，从中可以看出大师的魅力。此外，最好的一个简短详细的文献是《lshort》，这个有中文版《一份不太简短的LaTeX介绍》。最后，IEEEtran_HOWTO (in [IEEEtrans template](http://www.ieee.org/web/publications/authors/transjnl/index.html))也有很不错的latex用法介绍。

## Latex编译环境的安装

CTex下载： [http://www.ctex.org/HomePage](http://www.ctex.org/Homepage) 
常用论坛，答疑解惑： [http://bbs.ctex.org](http://bbs.ctex.org/) 
搜索和下载package的站点：http://www.ctan.org/ 
Wikibooks about Latex: http://en.wikibooks.org/wiki/LaTeX/
一个有趣的blog: http://latex.yo2.cn/articles/latex_blog.html

## Latex源文件的编辑工具

常用工具是WinEdit。同时我也挺喜欢Eclipse环境下的[TeXlipse](http://texlipse.sourceforge.net/)（特别是从版本1.4.0后，[TeXlipse已经无需外界程序来支持Spell Checking](http://texlipse.sourceforge.net/manual/spelling.html)）。

**如何配置WinEdit的界面Layout? 比如说，达到下面的简洁形式。**

![img](http://fmn022.xnimg.cn/fmn022/blog/20081126/14/51/A226549257482TON.jpg)

Menu的Options->Apperances->Docking可以改变Gather视口的Layout。
然后点击Menu的Project->Gather...，显示Gather视口。
要控制其他Viewer窗口的显示与否，对Menu点鼠标右键，就可以看到相关选项。

**如何在WinEdit里面修改快捷键？**

1. 点击菜单项Options->Menu Setup...，打开Menu Set对话框。
2. 在[Main Menu] Tab框里面找到要设置的内容进行快捷键设置。

**如何在WinEdit中改变编辑窗口的字体？**

点击菜单项Options->Preferences->Font。比如把字体改成Consolas Regular 12pt。

**如何在WinEdt中把自动换行设在第n个字符处？**

1. 点击菜单项Options->Preferences...
2. 在Editor tab的Right Margin栏里，设置Margin的字符数，比如为宽屏电脑设置120字符。
3. 点击菜单项Edit->Format->Format Document，按新的margin字符数整理整个tex文档。

**如何去掉tex文件编译时弹出的DOS窗口？**

1. 点击菜单项Options->Execution Modes...。
2. 在Accessories框里面点击常用的编译工具，比如LaTex或者PdfLatex。
3. 选择Run in the Background Mode。

参考：
Tips for WinEdit: http://physics.harvard.edu/~lahiri/tex/wdttip.html
WinEdit 使用技巧：[http://www.math.pku.edu.cn/teachers/tanghz/private/homepage/winedt.htm](http://www.math.pku.edu.cn/teachers/tanghz/private/homepage/winedt.htm)

## Latex源文件中对矢量图的加载

写文章最重要的就是形象思维，精致的图能给Reviewer良好的第一印象，也体现了Author的专业与否。 各IEEE journal都只接受矢量图。使用点阵图的paper很可能在上传的时候被拒绝。常用矢量图的格式有eps,pdf,ai,svg等.

**怎么载入一张矢量图到latex中？**

```latex
\usepackage{graphicx}

\begin{figure}[htb]
    \centering
    \includegraphics[width=xx.xx cm]{xxxx} 
    \caption{xxxx}
    \label{xxxx}
\end{figure}
```

有时latex编译上面的代码的时候会提示此图片没有bounding box。这是因为LaTeX在编译的时候必须知道图片的大小尺寸，称作bounding box。以下方法可以告诉LaTeX bounding box：使用Acrobat Reader的Document->Crop Pages。这样不会损害矢量图特性，能被各IEEE conference & journal接受。具体的参考下面的网页。

引用：Latex载入图形技巧 http://www.math.sinica.edu.tw/www/tex/latex_graphic.jsp

**Latex中并列子图的实现**

下面是个例子，详细说明请参考IEEEtran_HowTo。

```latex
\usepackage{graphicx} 
\usepackage{subfigure} 

%跨越多列的subfigure（假设是two columns的文档）
\begin{figure*}[htb] 
\centering \mbox{ 
\subfigure[figure a]{\includegraphics[width=.30\textwidth]{yours}}%
\quad 
\subfigure[figure b]{\includegraphics[width=.20\textwidth]{yours}}}% 
\caption{Several figures}\label{fig:xxxxx} 
\end{figure*} 

%单列的并列子图  
\begin{figure}[htb]
\centering \mbox{ 
\subfigure[figure a]{\includegraphics[width=.30\columnwidth]{yours}}%
\quad 
\subfigure[figure b]{\includegraphics[width=.20\columnwidth]{yours}}}%
\caption{Several figures}\label{fig:xxxxx}
\end{figure}
```

用\mbox命令是强迫多个图必须在同一行里面。如果省去了\mbox，当个图的宽度大于\textwidth或者\columnwidth的时候，有些图就会被放到下一行。

**用pdflatex编译的时候无法加载.eps格式的图像文件？**

问题的原因是pdflatex缺省处理.pdf格式的图片，无法处理eps格式。解决方法可以用acrobat distiller批量将所有的eps文件转成pdf格式。然后在.tex源程序里面将所有的.eps图片的后缀名去掉。pdflatex编译程序会自动加载相应pdf格式的文件。
参考： http://hi.baidu.com/jiyeqian/blog/item/edbef54faeac1930aec3ab5b.html

## 使用External Tools创建和编辑矢量图

### 矢量图的常用编辑工具列表

- Adobe Illustrator: 鼠标绘图中最好的工具，做出来的图可以很艺术化。Adobe的东西强于CorelDraw。自己整理了一个网上的教程，下次上传上来。
- MetaPost: 一种功能强大但比较底层的绘图语言。差不多就在DC的级别画像素点。适合画几何图形，尤其是因为它递归函数调用的能力。
- PGF/TikZ：语言描述层面的绘图工具。在node和connection那个逻辑层面上的，有节点自动布局和自动布线的功能。用它画Venn图的语法也很简单。
- Xfig: 非常强大的绘图工具，http://www.xfig.org/xfigcarlo/xfig-carlo.html
- visio: 适合画流程图。
- xymatrix: 适合pi演算那样的公式推导。
- gnuplot: 适合数据图
- matlab: 适合数据图
- origin: 适合数据图

### MetaPost相关资料

MetaPost适合几何图形绘制，有强大的递归执行能力，比如下面的分形结构。
![tree.jpg](http://fmn006.xnimg.cn/fmn006/blog/20080820/12/29/A654853945791CHA.jpg) 

- MetaPost Examples: [http://www.math.zju.edu.cn/ligangliu/LaTeXForum/MetaPost/Metapost_Examples.htm](http://www.math.zju.edu.cn/ligangliu/LaTexForum/Metapost/Metapost_examples.htm)
- MetaPost Intro: http://people.ku.edu/~syliu/shredderyin/metapost.html
- MetaPost Configuration http://huagw.blog.hexun.com/15332414_d.html
- 王垠的个人主页 http://people.ku.edu/~syliu/shredderyin/
- John Hobby为MetaPost写的用户手册''A User's Manual for MetaPost''
- MPS的图片文件转EPS - 不用再纠缠于prologues的设置 http://www.ida.liu.se/~joned/download/mps2eps/
- Learning METAPOST by Doing: [http://www.tlhiv.org/MetaPost/documentation/MetaPost_Learning.pdf](http://www.tlhiv.org/Metapost/documentation/Metapost_Learning.pdf)
- MetaPost illustration examples (for a mathematics textbook):http://www.topology.org/tex/conc/mp/

### PGF/TikZ

1. 什么是pgf？

   pgf是一个在tex系统中的画图宏包，tex尤其是beamer中使用pgf作图，“作精确图还比较方便, 色彩锐丽”（huangzh73）。除了可以精确的作图外，对于某些不要求精确控制的图形绘制，如：流程图，树图，等等，也提供了简便易用的支持。

2. pgf的作者？
   pgf也是beamer 的作者 Till Tantau 教授开发的. 起初只有 pgf, 后来有了 tikz and pgf 宏包的说法, 一般还是称为 pgf 宏包. 在使用中 \usepackage{tikz} 就自动加入了 pgf. 也许 tikz 可以认为是 pgf 进一步发展的产物.正因为两者出自同一个牛人之手，所以beamer和pgf结合使用确实非常的完美。

3. 安装和更新的方法: 
   pgf在ctex下的安装可参考beamer的安装。它们的关系差不多是beamer requires pgf，pgf requires xcolor。

4. 下面是一些展示pgf绘图效果的图库

- PGF and TikZ examples gallery： 
  http://www.fauskes.net/pgftikzexamples/
- A comprehensive list of PGF and TikZ examples:
  http://www.texample.net/tikz/examples/all/list/
- Edward Tufte’s book Beautiful evidence: 
  http://www.edwardtufte.com/bboard/q-and-a-fetch-msg?msg_id=0001TV&topic_id=1

5. 下面是一些自己用过的例子

- 数据流图：http://www.fauskes.net/pgftikzexamples/simple-flow-chart/
- 基于数据流的系统架构图：http://www.fauskes.net/pgftikzexamples/inertial-navigation-system/
- 时序图: http://www.fauskes.net/pgftikzexamples/pgf-umlsd/
- 二维的数据图plot2d：http://www.fauskes.net/pgftikzexamples/tkz-plot2d/
  http://www.fauskes.net/pgftikzexamples/pgfplots/
- 有限状态机图：http://www.fauskes.net/pgftikzexamples/state-machine/
- 二维几何图：http://www.fauskes.net/pgftikzexamples/tkz-2d/
- 三维几何图：http://www.fauskes.net/pgftikzexamples/3d-cone/
- 正则表达式图：http://www.fauskes.net/pgftikzexamples/diagram-chains/
- 图论相关图样：http://www.fauskes.net/pgftikzexamples/diagram-chains/
- 分类图：http://www.fauskes.net/pgftikzexamples/computer-science-mindmap/
- 公式说明图：http://www.fauskes.net/pgftikzexamples/beamer-arrows/ 
- 负反馈系统控制图：http://www.fauskes.net/pgftikzexamples/control-system-principles/
- 便签条图：http://www.fauskes.net/pgftikzexamples/boxes-with-text-and-math/
- 绘制二维迷宫：http://www.fauskes.net/pgftikzexamples/maze/
- 神经网络图：http://www.fauskes.net/pgftikzexamples/neural-network/
- 三维曲面： http://cs.nju.edu.cn/yangxc/dcc2003.files/matlab/matlab/2_3_2.htm
- pgf画Venn图的例子 http://bbs.ctex.org/viewthread.php?tid=36595
- 下面是用MetaPost画Venn图的另一个例子 http://bbs.ctex.org/viewthread.php?tid=35348
- 有个法国教师做了2d几何图的扩展包tkz-2d：
  主页： http://www.altermundus.fr/
  下载： http://www.altermundus.fr/pages/downloads/

### Matlab画数据图的一个例子

```matlab
hand = plot(xx, yy, 'k^-.', xx, yy, 'ko-.', xx, yy, 'b^--', xx, yy, 'bo--', xx, yy, 'r^-', xx, yy, 'ro-');
set(hand, 'LineWidth', 2);
set(hand, 'MarkerSize', 14);
hand = legend('label1', 'label2', 'label3', 'label4', 'label5', 'label6', 1);
set(hand, 'FontSize', 24); 
hand = xlabel('xlabel'); 
set(hand, 'FontSize', 24); 
hand = ylabel('ylabel'); 
set(hand, 'FontSize', 24); 
xlim([xmin, xmax]); 
ylim([xmin, ymax]); 
set(gca,'FontSize',20);
```

Origin画的数据图比Matlab好看些，但有时也感觉Origin太艳丽了，不那么正统。也还推荐gnuPlot。

Making Pretty Graphs by MATLAB: http://blogs.mathworks.com/loren/2007/12/11/making-pretty-graphs/
[![img](http://s10.sinaimg.cn/middle/6cec1179g76c8762529a9&690)](http://blog.photo.sina.com.cn/showpic.html#url=http://s10.sinaimg.cn/orignal/6cec1179g76c8762529a9)

### GnuPlot的安装和使用

个人感觉GnuPlot做出来的图没有Pgf和Origin的效果好。
推荐资料： Plotting with GnuPlot:  http://f3wm.free.fr/linux/gnuplot.html

1. Windows下的安装
   安装很简单。在 http://www.gnuplot.info/ 下载安装包gp424win32.zip. 解压后找到bin/wgnuplot.exe，双击运行即可。测试一下安装。运行命令：

```
gnuplot> plot [-3.14:3.14] sin(x)
```

2. 和Latex的整合
   gnuplot提供了直接输出tex文件的功能，只需要把output设置为latex就可以了。在命令行下输入：

```gnuplot
set terminal latex
set output "sin.tex" 
plot [-3.14:3.14] sin(x)     
```

把这个文件直接插入你的文章中，例如

```latex
\begin{figure}  
\begin{center}  
\input{sin.tex}   
\end{center} 
\end{figure}
```

3. 生成xy axis和label

```gnuplot
set terminal latex    
set output "sinagain.tex" 
set size 5/5.,4/3.  #设置图片的大小 
set format xy "$%g$" #设置x、y轴文字的格式 
set title "This is a plot of $y=sin(x)$" #设置图片标题 
set xlabel "This is the $x$ axis" #设置x轴的文字 
set ylabel "This is the $y$ axis" #设置y轴的文字 
plot [0:6.28] [0:1] sin(x)
```

4. 多条曲线的对比

```
set terminal latex 
set output "combine.tex" 
set size 5/5.,4/3.  #设置图片的大小 
set format xy "$%g$" 
set title "Combination" 
set xlabel "$x$ axis" 
set ylabel "$y$ axis" 
plot [-3.14:3.14] 0.2*x with points, sin(x) with lines
```

5. 一个3d作图和并列子图显示的例子

```latex
set terminal latex 
set output "tic.tex" 
set format y "$%g$" 
set format x "$%.2f$" 
set title "This is $\sin(x)$" 
set xlabel "This is the $x$ axis" 
set ylabel "$\sin(x)$" 
set xtics -pi, pi/4 #设置x的间距 
plot [-pi:pi] sin(x) 
set terminal latex 
set output 'plot3d.tex' 
set samples 20, 20 
set isosamples 21, 21 
set contour base 
set cntrparam levels auto 10 
set title "3D gnuplot demo - some more interesting contours" 0.000000,0.000000  font "" 
set xlabel "X axis" -5.000000,-2.000000  font "" 
set ylabel "Y axis" 4.000000,-1.000000  font "" 
set zlabel "Z axis" 0.000000,0.000000  font "" 
splot [x=-3:3] [y=-3:3] sin(x) * cos(y)

\begin{figure*}[!t] 
\centerline{
\subfigure[Case I]{\input{tic.tex
\label{fig_first_case}} 
\hfil 
\subfigure[Case II]{\input{plot3d.tex}
\label{fig_second_case}}
} 
\caption{Simulation results} 
\label{fig_sim} 
\end{figure*}
```

## LaTeX2html安装及在winEdt界面中的配置

任何Academic person都有需要构建个人主页，加强与外界的交流；撰写课件，教书育人。Html因为其易访问性成为最适合的格式。Latex2html和TtH能将tex文档编译成html，并较好的支持公式的输出，当然它们look and feel也比较academic，可以用来装学者。

**系统**
Windows XP SP2 
CTeX-2.4.6-Full 
Perl编译器：ActivePerl 5.10.0.1003 for Windows (x86). [http://www.activestate.com/Products/Downlo...x?id=ActivePerl](http://www.activestate.com/products/Downlo...x?id=Activeperl)
NetPBM 图形软件(CTeX-2.4.6-Ful l没有安装) ：现在网上很难找到合适的版本(据说1.2是work的)．用TtH还是比Latex2html简单一点． 
Postscript 解释器： CTeX-2.4.6-Full 已安装好了Ghostscript，在目录`C:\CTeX\Ghostgum\`下。
注册序列码如下。Name: Registered s/n: 195938022 5598
其余的安装参考：http://bbs.ctex.org/redirect.php?fid=7&tid=43334&goto=nextnewset

Tex4ht在CTex中的配置，参考 http://xaero.mmiyy.cn/notes/latex/tex4ht.htm

1. 把`C:\CTeX\WinEdt\Bin\TeX\TtH.bat`改名为TtH.bat.bak
2. 把`C:\CTeX\...\htlatex.bat`（具体路径在`C:\CTex`下面search一下，不同CTex版本不同）复制到`C:\CTeX\WinEdt\Bin\TeX\`下，改名为TtH.bat，则`Accessories/HTML/TtH (Tex—>HTML)`菜单变得可用。

**Tex4ht中数学公式的转换**

Tex4ht 先将数学公式转为dvi, 再利用外部软件, 如：ImageMagick, 转换为.png, .jpg or .gif文件。
依据我的经验，尚需要以下步骤才能使Tex4Ht正确转换数学公式为png文件：
\4. 安装ImageMagick 最新版本，Google搜索可以找到很多下载地址。 注意，为了避免在转换Tex时出现莫明其妙错误， Ctex以及ImageMagick安装目录中不要带有空格，中文等特殊字符。
\5. 测试ImageMagick是否安装成功，运行终端程序cmd，输入convert, 如果能正确找到文件就安装成功。
\6. 依然要修改 ％Ctex%\texmf\tex4ht\base\win32\tex4ht.env 文件，找到：alternative instructions for old versions of convert 将该节中 Gconvert 前的 % 全部去掉。
至此大功告成。 应该可能正常转换带数学符号的， 可以试试以下Tex文档：

```latex
\documentclass{article} 
\usepackage{CJK} 
\usepackage{tex4ht} 
\begin{document} 
\begin{CJK*}{GBK}{song} 
测试文档\\ test document\\ 
\begin{math}\frac{\pi}{\gamma} 
\\\frac{a+b-c}{d+e-k } 
\end{math} 
\end{CJK*} 
\end{document}
```

## Latex下幻灯片的制作：Beamer

Slides和Presentation的重要性就不必说了。

- A Beamer Quickstart (推荐) ：http://heather.cs.ucdavis.edu/~matloff/beamer.html
- A practical guide to beamer: http://faq.ktug.or.kr/wiki/uploads/beamer_guide.pdf
- 黄正华老师的总结: http://bbs.ctex.org/viewthread.php?tid=27695&extra=&page=1
- Beamer的在线教程: http://www.math.umbc.edu/~rouben/beamer/quickstart.html
- Beamer的安装：[http://dsec.math.pku.edu.cn/~yuhj/wiki/TeXSlides.html#sec-1](http://dsec.math.pku.edu.cn/~yuhj/wiki/Texslides.html#sec-1)
- 一个即刻上手的模板：http://www.bossh.net/forums/index.php?showtopic=1638
- 推荐一个好的Beamer模板库-非常简洁: http://www.math.sinica.edu.tw/www/tex/beamer_template.jsp
- Beamer Tips: [http://xueruini.myipcn.org/publish/TeX/Beamer.html](http://xueruini.myipcn.org/publish/Tex/Beamer.html)
- 用 Beamer 做相册: http://linux.cs.nthu.edu.tw/~clark/nb/archives/2008-02-03T23_32_45.php

 **Beamer的安装配置**

1. 下载beamer：http://sourceforge.net/projects/latex-beamer/
   下载pgf：http://sourceforge.net/projects/pgf/ 
   下载xcolor：http://sourceforge.net/projects/xcolor/
   
2. 解压到各自文件夹beamer、pgf、xcolor

3. 将beamer、pgf、xcolor复制到`TeXHOME\ctex\localtextmf\tex\latex`，并删除 `TeXHOME/texmf/tex/latex/` 下的beamer、pgf、xcolor

4. 进入TeXHOME\tex\localtextmf\tex\latex\xcolor，用“记事本”打开 xcolor.ins，启动cmd，定位到这个文件夹运行命令：

   ```
   latex xcolor.ins
   latex xcolor.dtx
   latex xcolor.dtx
   makeindex -s gind.ist xcolor.idx
   latex xcolor.dtx
   latex xcolor.dtx
   ```


   (这些命令在xcolor.ins文件里都写出来了)

5. 测试安装是否成功，运行命令：`latex xcolor1.tex`， `latex xcolor1.tex`

6. 然后运行 WinEdt 的 Accessories 菜单下 MikTex options 的 refresh now 即可。

注意事项： 当beamer做幻灯片时，需要使用 \usepackage[square, authoryear, comma]{natbib} 和 \citep{xxx} 做文章引用。因为用 natbib 和 citep 才能在beamer下很好的显示 square bracket。另外，做幻灯时，推荐用 \bibliographystyle{authordate1}。这样方便通过引用标记（作者+年份）看到该引文的分量。

## Bibtex的使用

Reviewer在读论文时，第一件事是读标题，了解你的Niche，你的论文要解决的问题；第二件事就是查阅你的Bibliography，这样做目的有三。(1) 看看你有没有很合适的引用他的文章。Academic guys对自己的论文的引用率impact ratio是很在意的。(2) 看看你引用的文章都来自于什么级别的刊物和会议，大概的年份分布，有没有反映最新的研究进展。从这里就能看出related work做得够不够，治学严谨与否。如果是reviewers是领域的专家的话，也会注意本领域的经典文章有没有引用。(3) 查看一下paper quality如何。虽然bibliography算是paper的小角落，但处理不好就会给reviewers留下这篇文章文字排版工作不够细致的印象。比如说, 作者名字缩写, 会议名的缩写, etc。这方面别全依赖于工具，如reference manager或endnotes。它们的items也都是从IEEE、ACM 这样的站点下载的。

Bibtex的作用是从.bib生成latex可直接识别的\bibitem的.bbl格式。这个格式转换的风格由bib style决定。常用的bib style如下。
Latex bibliography and citation style：http://www.stat.psu.edu/~surajit/present/bib.htm
IEEEtranBST：[http://www.ctan.org/tex-archive/macros/latex/contrib/IEEEtran/bibtex/](http://www.ctan.org/tex-archive/macros/latex/contrib/ieeetran/bibtex/)
中文的文章的bst：http://bbs.ctex.org/viewthread.php?tid=33591

为了在最终的pdf正确的生成bibliography, makefile需要调用latex（或pdflatex）三遍。

```shell
pdflatex %texfilename% 
bibtex %texfilename% 
pdflatex %texfilename% 
pdflatex %texfilename%
```

参考链接 http://bbs.ctex.org/viewthread.php?action=printable&tid=950

在正文里面引用时，IEEE模板需要引用cite package或者natbib package (推荐)。具体参考IEEEtranBST_howto

```latex
\usepackage[nocompress]{cite} 
%或者
\usepackage[square,comma,sort,authoryear]{natbib} % author year citation style
%或者
\usepackage[square,comma,sort,numbers]{natbib} % numerical citation style
```

正文里使用`\cite{label1,label2,label3}`命令或者`\citep{label1,label2,label3}`命令（for natbib）。
新手注意：Reference list里面只会显示那些正文里面引用了的那些文章。如果正文没有\cite，别怪bibtex报错。另外，对图片、表格、公式的引用是\ref命令，别搞混了。
参考：[http://latex.yo2.cn/articles/latex-bibtex-introduction.html](http://latex.yo2.cn/articles/latex-bibtex-introduction.html)

##  细节决定成败：Latex使用细节

**怎么输入左单引号、左双引号、右单引号、有双引号？**

左单引号：`(键盘上1旁边的那个)；左双引号：``；
右单引号：'(键盘分号的右边那个)；右双引号：''或"。
在普通模式下，''和"是一样的；但在数学模式下，''是两个导数符号。

**通过什么命令才能显式的定义生成页码？**

在\documentclass和\begin之间加入\pagestyle{option}，option可以是：

- plain:页码在底部，这是文章和报告的默认格式
- empty：无页码
- headings：页码在顶部
- myheadings：Similar to the headings pagestyle, except that the material to go at the top of the page is determined by \markboth and \markright commands 

怎样才能自定义宏？

当同一个串pattern反复出现在文章中的时候，可以用自定义宏来节省输入时间。\newcommand{}{}命令用来自定义宏。\renewcommand{}{}命令用来更新已经定义过的宏，详见http://hepg.sdu.edu.cn/Service/tips/latex/doc2/Macros.html。

**怎么输入“度数”之类的单位？**

试试SIunits包。

**我用了bib文件来保存citation，但所有title里面的单词都成了小写，怎么保持一些abbrevation的大写状态？**

用括号把title中的abbreviation框起来，如下：
{TOSSIM}: accurate and scalable simulation of entire TinyOS applications。

**怎么把"Chapter x"换成“第x章”，"Figure x"换成“图x”，"Theorem"换成“定理”， "Proof"换成“证明”……？**

前两个建议用CCT或CJK的\CJKcaption{GB}命令来解决。
第三个用\newtheorem{theorem}{定理}。以后这么用：
    \begin{theorem}...\end{theorem}
第四个用\renewcommand{\proofname}{证明}可以解决(需要amsmath包)。
类似的问题可以参考CJK的GB.cap和amsmath的文档。

**我要写算法伪代码/C/C++/Java...代码，怎么办？**

listings包不错，不妨一试。算法伪代码么，个人觉得algorithm2e不错。

**latex提供哪些定理环境？**

定义与否取决于所使用的模板。如果模板里面没有定理环境，可以用下面的命令自己定义，而且amsthm包已经预定义了三种style。

```latex
\theoremstyle{plain} 
\newtheorem{thm}{Theorem} 
\newtheorem{lem}[thm]{Lemma} 
\newtheorem{cor}[thm]{Corollary} 
\newtheorem{clm}[thm]{Claim} 
\newtheorem{prop}{Proposition} 
\newtheorem{fact}{Fact} 
\theoremstyle{definition} 
\newtheorem{defi}{Definition} 
\newtheorem{example}{Example} 
\theoremstyle{remark} 
\newtheorem{remark}{Remark} 
\newtheorem{proviso}{Proviso}
```

amsthm还定义了proof环境，最后会自动加一个QED符号。很方便吧？需要提醒大家：它和一些会议、杂志提供的文档类冲突。这些会议、杂志提供的文档类一般会提供类似的环境，大家要看看它们的文档。

**换行时latex会自动把词拆开。以下几种情况我们不期望拆词，可以使用"~"的小空格。**

1. 如果"."不表示句子的结束，应加入"\空格"，如"Mr. Wang"应输入为"Mr.\空格Wang"。因为当"."表示句号时，TeX会加入一段额外的空隙。
2. TeX遇到一个单词以大写字母结束时会自动认为这并不是句子的结束，故这种情况不必加入\空格。但如果确实是句子的结束，就需要在"."前加上"\@”，如“I study in SJTU\@.”。
3. 中文与英文之间一般加入小空隙排出来才好看，要加上"~"。
4. 中文与行内公式之间也要加。
5. 对Figure、Equation、Table的引用时,要加"~"，比如

```latex
\figurename~\ref{label} 
\tablename~\ref{label} 
\equationname~\ref{label}
```

**我的系统crash，论文稿件都丢了，怎么办？**

丢了的话就没什么特别的好办法了，去找IT guys做disk recovery吧。这很麻烦，所以还是建议预先使用CVS或SVN来做冗余备份和version control。这样boss也方便查看你的进度，一举多得。
WinCVS的使用参考 http://203.68.102.46/online_book/content.php?chapter_sn=223

**如何压缩论文篇幅？**

最自然的办法是靠文字的精炼，或者把证明推导放到Appendix里面(主要是journal)。
比较暴力的办法是用\vspace命令缩小图片与caption的间隔。另外也可以用\small命令把bibliography字体缩小。

```latex
\begin{figure}[htb] 
...... 
\vspace{-0.3cm} 
\caption{xxxx}\label{fig:xxx}
\end{figure}
```

**如何在pdf文档中生成目录书签？**

目的：在Latex生成的pdf文档中建立超链接(如从正文到参考文献，从目录到相应内容，从页码编号到实际页面等)，有利于读者快速定位当前阅读的信息。

1. 先引入以下宏包

```latex
\usepackage{lineno} 
\usepackage{indentfirst} 
\usepackage[pdfborder={0 0 0}]{hyperref} 
```

2. 在正文中分清楚章节

```latex
\section{}  
\subsection{}
```

3. 使用pdflatex编译

引用：http://blog.sina.com.cn/s/blog_5e16f1770100fkcz.html

**如何生成hyper reference？**

```latex
\definecolor{RoyalBlue}{RGB}{65,105,225}
\usepackage[colorlinks,pdfstartview=FitV,linkcolor=RoyalBlue,citecolor=RoyalBlue,urlcolor=RoyalBlue,anchorcolor=RoyalBlue]{hyperref}  
```

具体如何在pdf文档里面加入hyperref, bookmark, thumbnail，参考 [http://en.wikibooks.org/wiki/LaTeX/Hyperlinks](http://en.wikibooks.org/wiki/LaTex/Hyperlinks)

**如何压缩pdf文件？关于pdf文件还有什么其他的后期处理工具吗？**

方法一：用acrobat reader打开要压缩的pdf文件，然后点击菜单项文件->减少文件大小。
方法二：将要压缩文件用pdf打印机打印出来，并为点阵图设置合适的dpi值。
如果还需要其他对pdf文件的操作（如合并、分割、旋转、加水印、加页眉页脚等），可以使用命令行下的工具[pdftk](http://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/)，或者使用图形化工具acrobat reader的Document菜单。

**哪里能找到Thesis写作的排版指导？**

MSc. Thesis - LaTeX explanation：
http://www.markschenk.com/tensegrity/latexexplanation.html

Phd Thesis - LaTeX Template for Computer Science Theses at the Dalhousie University：
http://web.cs.dal.ca/~vlado/dalcsthesis/

大量的学位论文模板
http://latex.yo2.cn/articles/latex-graduatethesis.html

**tabular环境里面的\footnote在页底没有显示脚注，怎么办？**

用\footnotemark命令在tabular环境里面显示脚注的标号。在出了tabular环境之后再用\footnotetext命令在页底显示脚注。
参考：http://www.tex.ac.uk/cgi-bin/texfaq2html?label=footintab

**Latex里面有没有比较好看的手写字体？**

首先这里有一个较完整的 [Latex 字体列表](http://www.tug.dk/FontCatalogue/allfonts.html)，自己可以根据眼缘来挑选。

另外，关于手写字体，我自己喜欢lucida casual和Century Gothic。
下面是一个lucida casual的gallery： http://tug.org/store/lucida/complete.html
这是sample文档： http://tug.org/store/lucida/lucida-sample.pdf
这个下载地址： http://www.rzuser.uni-heidelberg.de/~t91/analysis-cd/software/miktex_2.0/ 和 http://www.ctan.org/tex-archive/fonts/psfonts/bh/lucida/

**我需要某个符号，我需要写某个样子的数学公式，怎么办？**

Latex 里面有一份文档，Higher Mathematics，很适合你。ctex的用户可以在CTeX\CTEX\doc下找到ch8.pdf，就是它。如果你想要的符号这里面没有，可以去查一查同一目录下的 symbol.pdf

**如何修改文章的行距？**

需要引用setspace包。它能修改正文、定理等环境的行距，但不会改变caption和footnote的行距。

```
\usepackage{setspace}
```

使用如下命令改变全文的行距

```latex
%\singlespacing 
%\onehalfspacing 
\doublespacing 
%\setstretch{1.1}
```

也可以在正文里，为特定段落定制行距

```latex
\begin{doublespace} 
  This paragraph has \\ double \\ line spacing. 
\end{doublespace} 
\begin{spacing}{2.5} 
  This paragraph has \\ huge gaps \\ between lines. 
\end{spacing}
```

引用：http://en.wikibooks.org/wiki/LaTeX/Customizing_LaTeX

**如何使PdfLatex生成的pdf文件嵌入字体？**

很多IEEE的会要求提交的文档嵌入字体。

首先，可以用以下方法查验自己的pdf文档是否嵌入了字体。（1）用Acrobat Reader打开该pdf文档；（2）进入菜单 File / Document Properties，然后点击 Fonts Tab，编辑框里面应该有字体列表。（3）确认字体列表里每一项后面都标注了Embedded Subset。

然后，当有字体尚未嵌入时，用如下方法嵌入所有字体。（1）在miktex安装目录搜索并找到updmap.cfg；（2）把该配置文件里面的 pdftexDownloadBase14 false 改成 pdftexDownloadBase14 true；（3）用updmap命令激活刚才的配置；（4）重新运行pdflatex，生成新版本的嵌入了字体的pdf文件。

引用：http://users.cecs.anu.edu.au/~luke/embedded_fonts.html

**Latex 里面如何输入长等号？**

用如下程序定义一个长等号命令\EqlFill

```latex
\usepackage{graphicx} 
\def\Eqlfill@{\arrowfill@\Relbar\Relbar\Relbar} 
\newcommand{\extendEql}[1][]{\ext@arrow 0099\Eqlfill@{#1}} 
\makeatother 

$$a \extendEql{\mbox{\textrm{def}}} b$$
```

**Latex 里面如何调整列表环境的间隔？**

设置方法一：在列表环境里进行设置，这样每次使用列表时自己随时设置，比较随意些：

```latex
\usepackage{graphicx} 
\documentclass{article} 
\usepackage{times} 
\pagestyle{empty} 
\setcounter{page}{6} 
\setlength\textwidth{159.0pt} 
\usepackage{pifont} 
\renewcommand\labelitemi{\ding{43}} 
\begin{document}
    \begin{itemize}
\setlength{\itemsep}{-\itemsep}
    \item Text of the first item in the list.
    \item Text of the first sentence in the second item of the list. And the second sentence.
    \end{itemize}
    \begin{enumerate}
\setlength{\itemsep}{0pt}
          \item item of the list.
          \item item of the list.
          \item item of the list. 
\end{enumerate}
\end{document}
```

设置方法二：方法一有一个缺陷就是你要随时设置比较麻烦，下面的方法较为简单，可以进行统一的设置。简单方便：

```latex
\documentclass{article} 
\usepackage{times} 
\pagestyle{empty} 
\setcounter{page}{6} 
\setlength\textwidth{159.0pt}  
\usepackage{pifont}  
\renewcommand\labelitemi{\ding{43}} 
\usepackage{atbeginend} % 可选宏包, 能解决许多问题, 
%比如itemize, enumerate环境\item之间的控制 
%用法 
\AfterBegin{itemize}{\addtolength{\itemsep}{-0.5\baselineskip}} 
\AfterBegin{enumerate}{\addtolength{\itemsep}{-0.5\baselineskip}} 
\begin{document}
    \begin{itemize}
          \item item of the list.
          \item item of the list.
          \item item of the list.
    \end{itemize}
    \begin{enumerate}
          \item item of the list.
          \item item of the list.
          \item item of the list. 
\end{enumerate} 
\end{document}
```

**如何产生自定义长度的空格？**

\hspace{xx}  产生xx长的水平空格
\vspace{xx}  产生xx长的垂直空格。

Latex里面的长度单位有：

- pt point     (1 in = 72.27 pt)
- pc pica     (1 pc = 12 pt)
- in inch     (1 in = 25.4 mm)
- bp big point   (1 in = 72 bp)
- cm centimetre  (1 cm = 10 mm)
- mm millimetre
- dd didot point  (1157 dd = 1238 pt)
- cc cicero    (1 cc = 12 dd)
- sp scaled point (65536 sp = 1 pt)

当换行时，\hspace｛xx｝产生的空格会被取消，如果要强制指定产生水平空格，用\hspace*。同理，当换页时，\vspace{xx}产生的空行也会被取消，强制指定用\vspace*。

**Latex 里面如何打印如下常用符号？** 

使用marvosym 宏包
演示： 
![5e16f177h7ac3d2265ca4&690](http://s8.sinaimg.cn/middle/6cec117949f5dda6d2237&amp;690) 
代码：

```latex
\documentclass[a4paper,twoside]{book} 
\usepackage{CJK} 
\usepackage[body={398pt,550pt},footskip=30pt,marginparwidth=60pt,marginparsep=10pt]{geometry} 
%\setlength\textwidth{180.0pt} 
\usepackage{marvosym} 
\begin{CJK*}{GBK}{song} 
\begin{document}
              \noindent\Emailct~XXXXXXX有限公司~~xxxx~xxxx~xxxxxx~xxx-xxx~室\\%
              \Telefon~\underline{0755-12345678}~~\\\Letter~\underline{xxx@xxxxxxxxx.com}~~\\%
              \Mobilefone~\underline{13812345678}~~\\\Pickup~\underline  {http://www.xxxxxxxxx.com/}\\% 
打勾: ${\surd}$\\ 
打叉: ${\texttimes}$ 
\paragraph{} 
\clearpage 
\end{CJK*} 
\end{document}
```

**pdf文件里面如何嵌入字体？**

主要IEEE会议在提交论文的时候，都强制要求嵌入字体。在Windows环境下，可以利用pdf printer。在Linux环境下可以采用如下办法：

1. Convert your PDF file to PS file

   ```
   pdftops mypaper.pdf
   ```

2. Convert back ps file to pdf using "prepress" settings

   ```
   ps2pdf14 -dPDFSETTINGS=/prepress mypaper.ps
   ```

http://kailaspatil.blogspot.com/2011/03/embed-fonts-in-pdf-file-using-pdflatex.html