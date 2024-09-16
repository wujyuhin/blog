#latex #软件使用攻略
# 一、下载、安装和配置

##  下载 TeXLive

下载链接： https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/

随便挑一个下载即可

![[Pasted image 20240823173041.png]]

## 安装 texlive

- 双击 texlive. Iso 文件
- 点击 install-tl-windows. Bat 文件
- 自己修改安装路径后点击安装
- 等待 30-60 分钟安装完成

![[Pasted image 20240823173054.png]]

## 下载、安装 TeXStudio

- 下载链接： [TeXstudio - A LaTeX editor (sourceforge.net)](https://texstudio.sourceforge.net/)
- 安装：调好路径，一路下一步安装即可

## 简单配置

选项-设置 TexStudio-构建-默认编译器-选择 XeLaTeX

- 中文用 XeLaTeX
- 英文用 PdfLaTeX

![[Pasted image 20240823173104.png]]

# 二、基本模板

复制一下模板点绿色箭头即可编译

![[Pasted image 20240823173113.png]]

```latex
%\documentclass[supercite]{upcthesis}
\documentclass{ctexart}
\usepackage{lipsum}
\usepackage{makecell}
\usepackage{amsmath}
\usepackage{mathtools}
\usepackage{amsfonts,amssymb}
\usepackage{subfigure}
\usepackage{enumerate}
\usepackage{graphicx}
\usepackage{epstopdf}
\usepackage{etoolbox}
\usepackage{titlesec}
\usepackage[titles,subfigure]{tocloft}
\thispagestyle{empty}
\usepackage{geometry}
\geometry{left=3.18cm,right=3.18cm,top=2.54cm,bottom=2.54cm}
\pagestyle{plain}	
\usepackage{setspace}
\date{}
\usepackage{fancyhdr}
\usepackage{titlesec}
\newfontfamily\sectionef{Arial}	% 设置Arial字体		
% \newCJKfontfamily\sectioncf{STXihei}	% 设置黑体
\titleformat{\section}{\center\zihao{-3}\heiti\sectionef}{第\,\thesection\,章}{1em}{}% 设置一级标题居中，中文字体为黑体，英文字体为Arial，字号为小三号
\titleformat*{\subsection}{\zihao{4}\heiti\sectionef}	% 设置二级标题中文字体为黑体，英文字体为Arial字号为四号

\usepackage[bookmarks=true,colorlinks,linkcolor=black,
citecolor=black]{hyperref}			% 设置超链接

\usepackage[superscript]{cite}		% 引入参考文献格式包
\bibliographystyle{mybst}		% 参考文献格式采用自制的mybst
\newcommand{\upcite}[1]{\textsuperscript{\textsuperscript{
			\citeleft}\cite{#1}\textsuperscript{\citeright}}}	% 设置参考文献序号格式

\usepackage{setspace}
\usepackage{geometry}		\geometry{left=3.2cm,right=3.2cm,top=3.8cm,bottom=3.8cm}	% 设置页边距
\usepackage{fancyhdr}		% 设置页眉
\pagestyle{fancy}	
\fancyhf{}													
\cfoot{\thepage}				% 设置页码
\CTEXsetup[name = {第,章}]{section}		% 设置章节格式
\renewcommand{\sectionmark}[1]{\markboth{第\thesection 章\quad % 设置页眉内容为章标题
		\ #1}{}}

%---------------------------cover.tex-------------------------------
\thispagestyle{empty}						%  当前页不显示页码
%------------------------abstract_cn.tex-------------------------------
\setcounter{page}{1}						% 设置当前页页码编号从1开始计数
\pagenumbering{Roman}						% 设置页码字体为大写罗马字体
%----------------------------main.tex-------------------------------
\setcounter{page}{1}						% 设置当前页页码编号从1开始计数
\pagenumbering{arabic}						% 设置页码字体为小写阿拉伯字体



%定义摘要环境
\fancyhead[C]{英\quad 文\quad 摘\quad 要}
\newcommand{\cnabstractname}{\zihao{-3}摘\quad 要}	% 定义中文摘要环境
\newenvironment{cnabstract}{
	\par\small
	\mbox{}\hfill{\bfseries \cnabstractname}\hfill\mbox{}\par
	\vskip 2.5ex}{\par\vskip 2.5ex}

\newcommand{\enabstractname}{\zihao{-3}Abstract}	% 定义英文摘要环境
\newenvironment{enabstract}{
	\par\small
	\mbox{}\hfill{\sectionef{\enabstractname}}\hfill\mbox{}\par 				% \sectionef：英文摘要使用Arial字体
	\vskip 2.5ex}{\par\vskip 2.5ex} 


\begin{document}
	%\maketitle
	\include{cover}								% 封面
	\include{abstract_cn}						% 中文摘要
	\include{abstract_en}						% 英文摘要
	\fancyhead[C]{\leftmark}					% 设置页眉内容为章标题
	\include{contents}							% 目录
	
	\setcounter{page}{1}
	\pagenumbering{arabic}
	
	\markboth{leftmark}{rightmark}
	\include{conclusion_reference_thanks}
	

	
	\begin{center}
		\quad \\
		%\quad \\
		\heiti \fontsize{45}{17} 毕\quad 业\quad 论\quad 文
		\vskip 3.5cm
		\heiti \zihao{2} 勾股定理	
	\end{center}
	\vskip 3.5cm	
	\begin{quotation}
		\songti \fontsize{15}{15}
		\doublespacing
		\par\setlength\parindent{12em}
		\quad 
		
		学\hspace{0.61cm} 院：\underline{\quad\quad\quad ****学院 \quad\quad\quad\quad }
		
		专\hspace{0.61cm} 业：\underline{机器设计制造及其自动化}
		
		学生姓名：\underline{\quad\quad\qquad Berlin\qquad\quad\quad }
		
		学\hspace{0.61cm} 号：\underline{\quad\quad 00000000000 \quad\quad\quad}
		
		指导教师：\underline{\quad\qquad\quad 傅里叶 \qquad\quad\quad}
		\vskip 2cm
		\centering
		2020年6月6日
	\end{quotation}
	\begin{cnabstract}{数据结构；面向对象；可视化；算法}
		结构算法设计和演示（C++）树和查找是在面向对象思想和技术的指导下，采用面向对象
		
		\textbf{关键字：}中文摘要
	\end{cnabstract}
	
	\begin{enabstract}{Write Criterion；Typeset Format；Graduation Project (Thesis)}
		Abcdeafg Abcdefg Abcdefg Abcdefg Abcdefg Abcdefg Abcdefg Abcdefg 
		
		\textbf{Keywords:}  Abstract
	\end{enabstract}
	
	\tableofcontents
	
	\section{引言}
	计算机与网络技术的高速发展，特别是面向对象技术的出现，使得C++的软件开发得到了迅速普及。
	
	本课题主要………………
	\section{线性表的基本理论知识}
	哈哈哈
	\subsection{线性表的定义}
	线性表是最简单、最常用\cite{Rouse1974Monitoring}的一种数据结构。线性表\cite{贾永红2010数字图像处理}是n（n>=0）个数据元素的有限序列。
	
	……。
	\subsection{线性顺序表}
	线性表的顺序存储结构的特点是为表中相邻的元素$a_i$和$a_{i+1}$ 赋以相邻的存储位置。
	\subsubsection{三级标题名}
	\subsubsection{三级标题名}
	\begin{itemize}
		\item [(1)] 三级以下标题
	\end{itemize}
	
	\subsection{线性链表}
	
	线性表的链式存储结构的特点是用一组任意的存储单元存储线性表的数据元素（这组元素可以是连续的,也可以是不连续的）。
	\section{设计的主体内容}
	在着手进行上机设计之前首先做好大量准备:应熟悉课题，进行调查研究，收集国内、外资料、分析研究；交互界面的设计和实现。
	
	……。
	\subsection{系统结构的设计}
	……。
	\subsection{交互界面的设计和实现}
	交互界面的设计应遵循………。
	\begin{equation}
		b\approx\frac{L_0}{\rho\tan(\theta_0)+z_0}
	\end{equation}
	式中，$z_0$为\textit{Goos-Hanchen}位移；$\theta_0$为光波的入射角。
	
	由公式(3-1)可以看出………。
	\subsection{线性表的OOP序设计}
	计算机内部可以采用两种不同方法来表示一个线性表,它们分别是顺序表示法和链表表示法。
	
	……。
	
	过阻尼响应如图\ref{guozuni}所示。

	\subsubsection{线性表的顺序存储的实现}
	……
	
	以上是顺序表的实现过程,第1-16行包含了list类的说明,接下来是成员函数的定义。
	
	……。
	\subsubsection{线性表的链表存储的实现}
	……
	
	链表的实现包括两个类定义，第一个是link类，第二个是list类。由于一个链表由若干个单独的链结点对象组成，因此一个链结点应当作为单独的link类实现。
	
	……
	
	……
	
	\section{实验及结果分析}
	例如由于起初未能真正掌握各种控件的功能，我设想是要一个下拉菜单，但是学识肤浅的我试了很多种就是达不到我要的效果，……。
	
	关于……的影响如表\ref{data_table}所示。
	
	\begin{table}[htbp]
		\small
		\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}} 
		\centering
		\caption{激光入射功率密度对导轨滚道表面硬化层深和显微硬度的影响}
		\begin{tabular}{ccccc}
			%\toprule
			试验编号 & 功率密度 & 辐照时间 & 显微硬度 	& 硬化层深\\ %\midrule
			t-1	&6.37×103	&0.067	&570，456	&0.354\\
			t-2	&6.37×103	&0.067	&570，456	&0.354\\
			t-3	&6.37×103	&0.067	&570，456	&0.354\\
			t-4	&6.37×103	&0.067	&570，456	&0.354\\
			t-5	&6.37×103	&0.067	&570，456	&0.354\\ %\bottomrule
		\end{tabular}
		\label{data_table}
	\end{table}
	
	
	鉴于表格复杂性，此处提供了可换行示例表见表\ref{kehuanhang}
	\begin{table}[htbp]
		\small
		\newcommand{\tabincell}[2]{\begin{tabular}{@{}#1@{}}#2\end{tabular}}  
		\centering
		\caption{可换行示例表}
		\begin{tabular}{ccc}
			%\toprule
			1	& 2& 3\\ %\midrule
			1&\tabincell{c}{3}&6\\
			1&\tabincell{c}{3}&6\\
			\tabincell{c}{2}&\tabincell{c}{4444444444\\5555555555}&\tabincell{c}{6}
			\\ %\bottomrule
		\end{tabular}
		\label{kehuanhang}
		\vspace{0.5em}
	\end{table}
	
	此处也提供了多列合并示例表如表\ref{duoliehebing}

	
	\section{结论}
	本课题采用C++语言、面向对象的设计方法实现数据结构的重要算法。
	
	而且还存在着许多不足之处。如：
	
	\section{致谢}

	大学四年的学习生活即将结束，在此，我要感谢所有曾经教导过我的老师和关心过我的同学，他们在我成长过程中给予了我很大的帮助。本文能够成功的完成，要特别感谢我的导师XXX教授的关怀和教导。

	\bibliography{./bibs/bibliography.bib}
	
\end{document}
```

# 二、vscode 使用
## 2.1 配置

![[Pasted image 20240627214812.png]] ![[Pasted image 20240627214946.png]]

上述操作后会出现以下配置文件，需要添加配置 
![[Pasted image 20240627215214.png]]
配置细节如下：
```python
"latex-workshop.latex.autoBuild.run": "never",

    "latex-workshop.showContextMenu": true,

    "latex-workshop.intellisense.package.enabled": true,

    "latex-workshop.message.error.show": false,

    "latex-workshop.message.warning.show": false,

    "latex-workshop.latex.tools": [

        {

            "name": "xelatex",

            "command": "xelatex",

            "args": [

                "-synctex=1",

                "-interaction=nonstopmode",

                "-file-line-error",

                "%DOC%"

            ]

        },

        {

            "name": "pdflatex",

            "command": "pdflatex",

            "args": [

                "-synctex=1",

                "-interaction=nonstopmode",

                "-file-line-error",

                "%DOC%"

            ]

        },

        {

            "name": "latexmk",

            "command": "latexmk",

            "args": [

                "-synctex=1",

                "-interaction=nonstopmode",

                "-file-line-error",

                "-pdf",

                "-outdir=%OUTDIR%",

                "%DOC%"

            ]

        },

        {

            "name": "bibtex",

            "command": "bibtex",

            "args": [

                "%DOC%"

            ]

        }

    ],

    "latex-workshop.latex.recipes": [

        {

            "name": "XeLaTeX",

            "tools": [

                "xelatex"

            ]

        },

        {

            "name": "PDFLaTeX",

            "tools": [

                "pdflatex"

            ]

        },

        {

            "name": "BibTeX",

            "tools": [

                "bibtex"

            ]

        },

        {

            "name": "LaTeXmk",

            "tools": [

                "latexmk"

            ]

        },

        {

            "name": "xelatex -> bibtex -> xelatex*2",

            "tools": [

                "xelatex",

                "bibtex",

                "xelatex",

                "xelatex"

            ]

        },

        {

            "name": "pdflatex -> bibtex -> pdflatex*2",

            "tools": [

                "pdflatex",

                "bibtex",

                "pdflatex",

                "pdflatex"

            ]

        },

    ],

    "latex-workshop.latex.clean.fileTypes": [

        "*.aux",

        "*.bbl",

        "*.blg",

        "*.idx",

        "*.ind",

        "*.lof",

        "*.lot",

        "*.out",

        "*.toc",

        "*.acn",

        "*.acr",

        "*.alg",

        "*.glg",

        "*.glo",

        "*.gls",

        "*.ist",

        "*.fls",

        "*.log",

        "*.fdb_latexmk"

    ],

    "latex-workshop.latex.autoClean.run": "onFailed",

    "latex-workshop.latex.recipe.default": "lastUsed",

    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",

    "latex-workshop.view.pdf.viewer": "tab",

    "latex-workshop.view.pdf.ref.viewer":"auto",
```

注意：当把配置文件添加好后，需要 `ctrl + p` 打开命令面板，然后输入 `> reload window`，或者点击查看，选择命令面板，然后输入 `reload window` 让配置文件生效.
## 2.2vscode 使用
快捷键：
```
ctrl + alt + b 编译
ctrl + alt + v 展示编译后的pdf
ctrl + alt j 鼠标指向latex代码，高亮对应的pdf内容位置
```