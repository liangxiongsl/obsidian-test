---
{"dg-publish":true,"permalink":"/docs/obsidian/","tags":["gardenEntry","gardenEntry"]}
---


!!! ad-note sd

内容

--- admonition

### 1.文档

[obsidian文档](https://docs.obsidian.md/Themes/App+themes/Build+a+theme)

[超好用笔记软件！神奇的Obsidian黑曜石Markdown文本编辑知识管理工具，成为你的第二大脑【方俊皓同学】_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Ya4y1E7Mo/?spm_id_from=333.788&vd_source=208302bb40f651c78a4db5c2fd649412)

[obsidian不就是个记笔记的软件吗_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1yg41147YG/?spm_id_from=trigger_reload&vd_source=208302bb40f651c78a4db5c2fd649412)


obsidian拥有强大的插件生态，(前段)程序员友好，关系图谱神经网络等特地

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


- 以下是插件的一些例子：
	1. 第三方插件代理：[juqkai/obsidian-proxy-github](https://kkgithub.com/juqkai/obsidian-proxy-github)
{ #b3704d}

	2. mermaid：[GitHub - dartungar/obsidian-mermaid: Tools for improved Mermaid.js experience in Obsidian.md (kkgithub.com)](https://kkgithub.com/dartungar/obsidian-mermaid)
	3. 主题：
	4. [[docs/obsidian#dataview——笔记查询插件\|dataview]]：[GitHub - blacksmithgu/obsidian-dataview: A high-performance data index and query language over Markdown files, for https://obsidian.md/. (kkgithub.com)](https://kkgithub.com/blacksmithgu/obsidian-dataview)


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


