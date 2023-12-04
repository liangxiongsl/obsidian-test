---
{"dg-publish":true,"permalink":"/docs/obsidian/","tags":["gardenEntry"]}
---



### 1.文档

[obsidian文档](https://docs.obsidian.md/Themes/App+themes/Build+a+theme)

[超好用笔记软件！神奇的Obsidian黑曜石Markdown文本编辑知识管理工具，成为你的第二大脑【方俊皓同学】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ya4y1E7Mo/?spm_id_from=333.788&vd_source=208302bb40f651c78a4db5c2fd649412)

[obsidian不就是个记笔记的软件吗_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1yg41147YG/?spm_id_from=trigger_reload&vd_source=208302bb40f651c78a4db5c2fd649412)


obsidian拥有强大的插件生态，(前端)程序员友好，关系图谱神经网络等特地 

### 2.插件

灵感：
- [如何在 Obsidian 中建立类似 Notion Database 的数据库？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/632122944)
-  [⭐Obsidian：神奇的 CSS Snippets 代码段_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1eK4y1M7K9/?spm_id_from=333.337.search-card.all.click&vd_source=208302bb40f651c78a4db5c2fd649412)

- 外链
	1. [obsidian插件文档](https://publish.obsidian.md/chinesehelp/01+2021%E6%96%B0%E6%95%99%E7%A8%8B/%E7%AC%94%E8%AE%B0%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%88MOC%EF%BC%89)
	2. [插件下载](https://airtable.com/shrdmp10Lxmf5Wmgl)
	3. [插件下载(腾讯文档)](https://docs.qq.com/sheet/DT3BKQXpoZElyY0VJ)

.obsidian/plugins/xxx 目录代表一个插件，该目录一般有三个文件：(1) main.js，(2) manifest.json，(3) styles.css

注：国内对第三方插件的访问被墙，有两种解决方法：(1) [[docs/obsidian#^b3704d\|代理插件]]，(2) 到 github 上找插件，(3) 翻墙


- 较为重要的插件：
	1. 日记：
	2. 笔记：[笔记方法论（MOC） - Obsidian中文教程 - Obsidian Publish](https://publish.obsidian.md/chinesehelp/01+2021%E6%96%B0%E6%95%99%E7%A8%8B/%E7%AC%94%E8%AE%B0%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%88MOC%EF%BC%89)
	3. 待办(to do list)：[GitHub - HeroBlackInk/ultimate-todoist-sync-for-obsidian (kkgithub.com)](https://kkgithub.com/HeroBlackInk/ultimate-todoist-sync-for-obsidian)
	4. 数据库：dataview，db folder，dataloom
	5. admonitions
	6. 发布到web：vercel+digital garden


- 以下是插件的一些例子：
	1. 第三方插件代理：[juqkai/obsidian-proxy-github](https://kkgithub.com/juqkai/obsidian-proxy-github)
{ #b3704d}

	2. mermaid：[GitHub - dartungar/obsidian-mermaid: Tools for improved Mermaid.js experience in Obsidian.md (kkgithub.com)](https://kkgithub.com/dartungar/obsidian-mermaid)
	3. 主题：
	4. [[docs/obsidian#dataview——笔记查询插件\|dataview]]：[GitHub - blacksmithgu/obsidian-dataview: A high-performance data index and query language over Markdown files, for https://obsidian.md/. (kkgithub.com)](https://kkgithub.com/blacksmithgu/obsidian-dataview)
	5. 笔记拆分：[obsidian-note refactor](https://kkgithub.com/lynchjames/note-refactor-obsidian)
	6. 关联题目搜索（需要chatgpt api-key）：[smart connection](https://github.com/brianpetro/obsidian-smart-connections)
	7. tikz绘图：[obsidian-tikzjax](https://kkgithub.com/artisticat1/obsidian-tikzjax)
	8. 自动补全：[obsidian-various-complements-plugin: This plugin for Obsidian enables you complete words like the auto-completion of IDE. (kkgithub.com)](https://kkgithub.com/tadashi-aikawa/obsidian-various-complements-plugin)
        	- 补充：[Google10000单词](https://kkgithub.com/first20hours/google-10000-english)
        	- 
- d
    - sd

#### 日记

#### 笔记



#### 待办(to do list)

实际上实现 to do list 可以不用安装插件，这些插件更多地只是显示好看，或者方便其他软件同步

markdown 的标准 to do list：
```
- [ ] un
- [x] chec
```

[[docs/obsidian#4.代码段\|代码段]] 提供的 to do list：
```
- [>]  sch
- [-] can
- [?] info
- [!] imp 
```

#### dataview——笔记查询插件

每个目录可以视作一张**表**，该目录下的 .md 文件视作一条**记录**，每个 .md **文件的字段**由两种 yaml 的方式定义——(1) .md 文件开头中 --- 包围的块中的 "key: value" 键值对，(2) yaml 代码块之外的 "key:: value" 键值对

**查询语句：**
```note-gray-background
r[table | list | task]
from [fields] as [alias]
where "condition" 或 #tag
sort [cols] [desc]
```
- "table" 命令相当于 sql 中的 table 命令，只不过前者给每条记录额外添加了一个值为 .md 的文件名的字段

| File                           | time-played | length | rating |
| ------------------------------ | ----------- | ------ | ------ |
| [[docs/obsidian\|obsidian]] | \-          | \-     | \-     |
| [[docs/readme\|readme]]     | \-          | \-     | \-     |
| [[docs/浏览器插件\|浏览器插件]]       | 1周、6天       | \-     | \-     |

{ .block-language-dataview}


- [[docs/obsidian\|obsidian]]: \-
- [[docs/readme\|readme]]: \-
- [[docs/浏览器插件\|浏览器插件]]: 1周、6天

{ .block-language-dataview}

#### Templater——模板插件
注：obsidian 已提供了模板的核心插件

- [obsidian-Templater 文档](https://silentvoid13.github.io/Templater/)
- [obsidian-Templater 仓库](https://kkgithub.com/SilentVoid13/Templater)

- 用法：
	- 使用前需要配置模板所在目录，默认目录为根目录
	- 快捷键 `alt + e` 或左侧边栏中的按钮可以直接插入某个模板
	- `undefined` 可以嵌入特定 js 内容
- 用途：
	- 用于嵌入笔记模板
	- 通过嵌入以 --- 包围的 yaml 代码块，可以实现 .md 文档的属性的快速添加，如：文件创建时间，文件修改时间，以及其他属性；然后可以结合[[docs/obsidian#dataview——笔记查询插件\|dataview]] 来使用
#### Admonition——"卡片块"

- [admonitions](https://kkgithub.com/javalent/admonitions)
- [javalent/admonitions: Adds admonition block-styled content to Obsidian.md (kkgithub.com)](https://kkgithub.com/javalent/admonitions)

```ad-tip
title: 寄吧

$\sum\limits_{i=1}^n=\sum\limits_{i=1}^n$
```

> [!note] 寄吧
> $$\sum\limits_{i=1}^n\sum\limits_{j=1}^nij=\sum\limits_{i=1}^ni\sum\limits_{j=1}^nj=\frac{n^2(n+1)^2}4$$

#### 发布到web

- [obsidian-digital-garden 插件](https://kkgithub.com/oleeskild/obsidian-digital-garden)
- [digitalgarden 仓库模板](https://github.com/oleeskild/digitalgarden)


[流程可参考该链接](https://dg-docs.ole.dev/getting-started/01-getting-started/)

[本站的链接](https://obsidian-test-phi.vercel.app/)

#### tikz绘图示例

[obsidian-tikzjax](https://kkgithub.com/artisticat1/obsidian-tikzjax)

```tikz
\begin{document}
  \begin{tikzpicture}[domain=0:4]
    \draw[very thin,color=gray] (-0.1,-1.1) grid (3.9,3.9);
    \draw[->] (-0.2,0) -- (4.2,0) node[right] {$x$};
    \draw[->] (0,-1.2) -- (0,4.2) node[above] {$f(x)$};
    \draw[color=red]    plot (\x,\x)             node[right] {$f(x) =x$};
    \draw[color=blue]   plot (\x,{sin(\x r)})    node[right] {$f(x) = \sin x$};
    \draw[color=orange] plot (\x,{0.05*exp(\x)}) node[right] {$f(x) = \frac{1}{20} \mathrm e^x$};
    \draw[color=pink] plot (\x,{\x^(0.3*\x)}) node[right] {$f(x) = x^{0.3x}$};
  \end{tikzpicture}
\end{document}
```

```tikz
\usepackage{circuitikz}
\begin{document}

\begin{circuitikz}[american, voltage shift=0.5]
\draw (0,0)
to[isource, l=$I_0$, v=$V_0$] (0,3)
to[short, -*, i=$I_0$] (2,3)
to[R=$R_1$, i>_=$i_1$] (2,0) -- (0,0);
\draw (2,3) -- (4,3)
to[R=$R_2$, i>_=$i_2$]
(4,0) to[short, -*] (2,0);
\end{circuitikz}

\end{document}
```

```tikz
\usepackage{pgfplots}
\pgfplotsset{compat=1.16}

\begin{document}

\begin{tikzpicture}
\begin{axis}[colormap/viridis]
\addplot3[
	surf,
	samples=18,
	domain=-3:3
]
{exp(-x^2-y^2)*x};
\end{axis}
\end{tikzpicture}

\end{document}
```

```tikz
\usepackage{tikz-cd}

\begin{document}
\begin{tikzcd}

    T
    \arrow[drr, bend left, "x"]
    \arrow[ddr, bend right, "y"]
    \arrow[dr, dotted, "{(x,y)}" description] & & \\
    K & X \times_Z Y \arrow[r, "p"] \arrow[d, "q"]
    & X \arrow[d, "f"] \\
    & Y \arrow[r, "g"]
    & Z

\end{tikzcd}

\quad \quad

\begin{tikzcd}[row sep=2.5em]

A' \arrow[rr,"f'"] \arrow[dr,swap,"a"] \arrow[dd,swap,"g'"] &&
  B' \arrow[dd,swap,"h'" near start] \arrow[dr,"b"] \\
& A \arrow[rr,crossing over,"f" near start] &&
  B \arrow[dd,"h"] \\
C' \arrow[rr,"k'" near end] \arrow[dr,swap,"c"] && D' \arrow[dr,swap,"d"] \\
& C \arrow[rr,"k"] \arrow[uu,<-,crossing over,"g" near end]&& D

\end{tikzcd}

\end{document}
```

```tikz
\usepackage{chemfig}
\begin{document}

\chemfig{[:-90]HN(-[::-45](-[::-45]R)=[::+45]O)>[::+45]*4(-(=O)-N*5(-(<:(=[::-60]O)-[::+60]OH)-(<[::+0])(<:[::-108])-S>)--)}

\end{document}
```

```tikz
\usepackage{chemfig}
\begin{document}

\definesubmol\fragment1{

    (-[:#1,0.85,,,draw=none]
    -[::126]-[::-54](=_#(2pt,2pt)[::180])
    -[::-70](-[::-56.2,1.07]=^#(2pt,2pt)[::180,1.07])
    -[::110,0.6](-[::-148,0.60](=^[::180,0.35])-[::-18,1.1])
    -[::50,1.1](-[::18,0.60]=_[::180,0.35])
    -[::50,0.6]
    -[::110])
    }

\chemfig{
!\fragment{18}
!\fragment{90}
!\fragment{162}
!\fragment{234}
!\fragment{306}
}

\end{document}
```

#### 多个库共享单个配置

由于一个库内可能有很多插件，会造成存储空间辅导过重，多库共享一个配置就很有必要

一般配置文件总共为 50mb 左右，如果忽略 assets 内的文件，所有库的总存储量极难超过 100mb

在命令行中执行软链接命令：（注：软链接不是 .lnk 文件）
```cmd
mklink /d [次库的配置目录] [主库的配置目录]
```

如：`mklink /d "D:\lx\sub_vault\.obsidian" "D:\lx\main_vault\.obsidian"`


### 3.主题
.obsidian/themes/xxx.css 代表一个主题


### 4.代码段
.obsidian/snippets/xxx.css 代表一个代码段

[⭐Obsidian：神奇的 CSS Snippets 代码段_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1eK4y1M7K9/?spm_id_from=333.337.search-card.all.click&vd_source=208302bb40f651c78a4db5c2fd649412)

- [obsidian-snippets 仓库](https://kkgithub.com/deathau/obsidian-snippets)
- [awesome-obsidian 仓库](https://kkgithub.com/kmaasrud/awesome-obsidian)


### 其他内容

- 设置里面的内容，如：快捷键，显示行号，缩放字体/界面大小
- 标记 #算法 #kmp
- 书签
- 同步：有多种独立于 obsidian 的同步方法：onedrive，ftp，
- 图床：非必要不建议插入图片，对于特殊需求可以考虑 github 图床
- 关系图谱：每个节点是一个 .md 文件，节点之间的连线是指其中一个 .md 文件通过内部链接连接到另一个 .md 文件（假设每个节点都是相互独立的，那么该仓库的笔记之间没有关联，类似于传统的 mkdocs 项目）


### 笔记系统设计

如果把 obsidian 的仓库视为一个项目，那么每个项目的**首选配置**，**插件**，**主题**，**代码段**都可以视为该项目的模块或配置

一个笔记系统就是一个项目，该项目包含**首选配置**，**插件**，**主题**，**代码段**，也就是项目目录下的 `.obsidian` 文件夹下的内容

通过项目不同模块的组成和组合，就能构建强大的 obsidian 笔记生态

- [开箱即用的obsidian模板库_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV19F411i7Lu/?spm_id_from=333.337.search-card.all.click&vd_source=208302bb40f651c78a4db5c2fd649412)


