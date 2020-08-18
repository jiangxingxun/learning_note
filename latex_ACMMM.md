# Latex Note for ACM MM 
author : Xingxun Jiang
## Overview
* [初稿写作时](#初稿写作时)
* [Accepted之后](#Accepted之后)
* [其他说明](#其他说明)

## 初稿写作时
1. 整体架构：original Tex template File
    * acmart.cls   : 格式文件
    * MM_2020.bib  => MM_2020.bbl (编译后文件，提交时用)   : 参考文献文件
    * MM_2020.tex (sample-sigconf.tex)                  : Tex主文件

2. 论文写作细节
```tex
%% 超链接
\usepackage{hyperref}
\url{https://dfew-dataset.github.io/}

%% 段落
\section{Section}        % 段落
\subsection{subSection}  % 子段落
```

3. 表格
```tex
%% 表格
% 表格基本结构
\begin{table*}[h]    % *占两列，无则一列   here,top,bottom,page浮动页
\begin{center}
  \caption{Table Title.}   % 表名，需带句号
  \label{tab:tab1}         % 表的引用名，与~\ref{tab:tab1}相对应

\begin{tabular}{cccccc} % 各列排版状况，c表示居中，其数量与列数对齐
\toprule % 表格最上线(粗)
Database & \#Sample & Source & Expression Distribution & \#Annotation Times & Available?\\ 
         % \# 该列表示数目

\midrule % 表格中线(粗)
DFEW & 16,372 & 1500 movies & 7 basic expressions &10 &\href{https://dfew-dataset.github.io/}{Yes}\\  
                   % \href{...}需引\usepackage{hyperref}包

\bottomrule % 表格最下线(粗)
\end{tabular}

\end{center}
\end{table*}


% 多列表格与多行
% \multirow{多行的数目}{排版要求:自动或居中}{内容}
% \multicolumn{多列的数目}{排版要求:自动或居中}{内容}
\toprule
\multirow{2}{*}{Emotions} & \mutlicolumn{4}{c}{Clips} & \multirow{2}{*}{Percent} \\
                          \cline{2-5}      % 在第2-5行中画横线
                          & 0-2s & 2-5s & 5s+ & Total &\\
\midrule

% 表格微调：表格间留小空隙，用~充当一行
Emotions&~&Metric 
```

4. 图
```tex
%% 图
% 转换图片，可用shell命令
convert xxx.png xxx.eps 

% 图片基本结构
\begin{figure*}[t]          % *占两列，无则一列   here,top,bottom,page浮动页
\includegraphics[width=\textwidth]{pic/dataset_demo} % 文件夹/无后缀文件名，.eps格式
               % [width=\textwidth]    [width=\columnwidth]    [width=8.2cm]   [width=0.75\textwidth]
               % [scale=1] 与原文件比例为1
               % [angle=90] 将图像旋转90度
\caption{Figure Title.}     % 图名，以句号结尾
\label{fig:pipeline}        % 图的引用名，与~\ref{fig:pipeline}相对应
\end{figure*}
```

5. 图表引用
```tex
%% 图表引用
~\cite{zheng2006facial,zhao2007dynamic}    % 引用参考文献
Table~\ref{tab:tab1}                       % 引表格，与\label{tab:tab1}相对应
Fig.~\ref{fig:pipeline}                    % 引图片，与\label{fig:pipeline}相对应
```

6. 常用命令
```tex
%% 需要转义的常用字符
\#     \%    \{    \}   \&   \left[    \right]  

%% 常用符号
\bar{P} 平均 
\phi    核函数的希腊字母
\times  乘法符号
\textless 小于号
\leq    小于等于号
\max_{k=1,2,...,k} % 上下结构
max_{k=1,2,...,k}  % 左右结构

%% 常用表达
k \notin \{ 1,2,3,4,5,6,7 \}   % k 不属于集合{1,2,3,4,5,6,7}
x \in \mathbb{R}^d             % x 属于d维实数域 
\textbf{48.26}           % 加粗
```

7. 公式
```tex
% 左边大括号，将多个式子合并
\begin{align}
\left \{   
    \begin{array}{l}
      p_j = \frac{1}{N \times n} \sum_{i=1}^N \limits n_{ij}\\ % \limits 使字母完全位于 求和符号上下端
      \sum_{j=1}^{K} \limits p_j=1
    \end{array}
\right.
\end{align}

% 分段函数
\begin{align}
P_{ij} = 
  \begin{cases}
     0, & \text{if $x_i$ and $x_j$ has the same label}\\
     1, & \text{otherwise}   % 数学公式中的文字用\text{...}包起来
  \end{cases}
\end{align}

```

## Accepted之后
1. 论文细节
```tex
%% 标题：强制换行，美化排版
\title{DFEW: A Large-Scale Database for Recognizing Dynamic \\ Facial Expression in the Wild}

%% 提交时隐藏页眉
\fancyhead{}

%% 关键字用 ; semicolon
\keywords{Dynamic facial expression; Facial expression database; in-the-wild facial expression recognition; deep learning}

%% 可用于列宽过长的单词拆分: 上行有- 下行无
\noindent where $n=10$ is the annotation time % \noindent 此行无缩进； 
```

2. 作者：共同一作 & 通讯作者
```tex
% 共同一作
\author{Xingxun Jiang}
\authornote{Both authors contributed equally to this research.}
\email{jiangxingxun@seu.edu.cn}
\orcid{0000-0002-2139-8623}
\author{Yuan Zong}
\authornotemark[1]
\email{xhzongyuan@seu.edu.cn}
\affiliation{
  \institution{School of Biological Science and Medical Engineering, Southeast University}
  \city{Nanjing}
\country{China}
}

% 通讯作者
\author{Wenming Zheng}
\authornote{Corresponding author}
\affiliation{
  \institution{Key Laboratory of Child Development and Learning Science, Southeast University}
  \city{Nanjing}
\country{China}}
\email{wenming\_zheng@seu.edu.cn}
```

3. 参考文献：平衡各列，美化排版
```tex
\usepackage{balance}

\bibliographystyle{ACM-Reference-Fomat}
\balance
\bibliography{MM_final}   % MM_final.bib
```

4. 致谢
```tex
\begin{acks}
Grant 2242018K3DN01.  % 不用 \section{your section title}
\end{acks}
```

5. 论文备注信息：完成Rights form之后，文章加上权利声明、会议说明、论文分类等
```tex
% 权利管理信息：提交Right form后，由系统产生
\acmYear{2020}
\setcopyright{acmlicensed}\acmConference[MM '20]{Proceedings of the 28th ACM International Conference on Multimedia}{October 12--16, 2020}{Seattle, WA, USA}
\acmBooktitle{Proceedings of the 28th ACM International Conference on Multimedia (MM '20), October 12--16, 2020, Seattle, WA, USA} \acmPrice{15.00}
\acmDOI{10.1145/3394171.3413620} \acmISBN{978-1-4503-7988-5/20/10}

% 会议说明：提交Right form后，由系统产生
\acmConference[MM '20]{Proceedings of the 28th ACM International Conference on Multimedia}{October 12--16, 2020}{Seattle, WA, USA}
\acmBooktitle{Proceedings of the 28th ACM International Conference on Multimedia (MM '20), October 12--16, 2020, Seattle, WA, USA}
\acmPrice{15.00}
\acmISBN{978-1-4503-7988-5/20/10}

% 论文分类：用户从 http://dl.acm.org/ccs.cfm 选择论文分类标准
\begin{CCSXML}
<ccs2012>
   <concept>
       <concept_id>10003120.10003145.10011770</concept_id>
       <concept_desc>Human-centered computing~Visualization design and evaluation methods</concept_desc>
       <concept_significance>500</concept_significance>
       </concept>
   <concept>
       <concept_id>10010147.10010178.10010224</concept_id>
       <concept_desc>Computing methodologies~Computer vision</concept_desc>
       <concept_significance>500</concept_significance>
       </concept>
 </ccs2012>
\end{CCSXML}

\ccsdesc[500]{Human-centered computing~Visualization design and evaluation methods}
\ccsdesc[500]{Computing methodologies~Computer vision}
```

## 其他说明
* [arXiv提交](https://zhuanlan.zhihu.com/p/109405192)
* [论文格式其他细节](https://zhuanlan.zhihu.com/p/30944610)
* [程明明写作课|Res2Net(TPAMI) Tex File](https://mmcheng.net/writing/)
* [希腊字母表](https://jingyan.baidu.com/article/4b52d702df537efc5c774bc9.html)


















