---
template: deck
theme: black
transition: fade
cover:
  title: 模板能力全景
  subtitle: 一份 markdown 能做的事,一页一页摊开给你看
  author: x-cmd
  date: 2026-11-25
  tag: reveal.js as a service
  qr: https://github.com/x-cmd/ppt
  background: aurora-blue
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

**能住进仓库,能住进 issue,能住进 URL。**

--

<!-- .slide: data-layout="two-col" -->

# 怎么读这份 deck

- **横向**是**系列**:六个系列,一个一个讲
- **纵向**是**系列里的页**:每个系列 3–4 页,一页一件事
- 每个系列的**第一页是钩子**:标题 + 一句摘要,其余是详情

```text
---            ← 新系列
# 钩子
一句摘要
--
## 详情一
--
## 详情二
```

--

<!-- .slide: data-layout="fact" data-title="18" data-background-gradient="radial-gradient(#1d4e5f 0%, #14323e 52%, #0a161c 100%)" -->

# 18

十八页 · 六个系列 · 十二种内置版式,全都真的用上了。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 一 · 源

三种住法,一个入口。

--

<!-- .slide: data-layout="two-col" -->

# 三种源,一个入口

- **仓库文件** —— 整个 markdown 就是 deck
- **issue / PR / release** —— 扫正文与评论里的 `x-cmd/ppt` 围栏块
- **URL 直传** —— `?content=` 一段原文,应急两页

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt?content=<URL 编码的 markdown>
```

--

<!-- .slide: data-layout="fact" data-title="1" data-background-gradient="radial-gradient(#1d4e5f 0%, #14323e 52%, #0a161c 100%)" -->

# 1

一个链接,就是一场演讲。

--

<!-- .slide: data-layout="quote" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

> 内容住在仓库里,链接只是它的门。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 二 · 结构

横向分主题,纵向分页 —— 每个系列的第一页是钩子,后面是详情。

--

<!-- .slide: data-layout="two-col" -->

# 二维结构

`---` 横向分页(换主题),`--` 纵向分页(同一主题的第二页)。

所以一份 deck 天然长这样:

- **系列首屏**:钩子 + 一句摘要(`section` 版式)
- **系列详情**:该系列的每一页(`--` 接在后面)

```text
---            ← 新系列
# 钩子
--
## 详情一
--
## 详情二
```

--

<!-- .slide: data-layout="fact" data-title="2×" data-background-gradient="radial-gradient(#2c4630 0%, #1c2c20 52%, #0e1610 100%)" -->

# 2×

两个维度,两种讲法:横向换章,纵向推进。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 三 · 图

数据图与结构图,都是内联矢量。

--

<!-- .slide: data-layout="two-col" -->

# 图是矢量的

- **数据图**:pie / bar / line / radar / sankey / gauge …
- **结构图**:seq / arch2 / erd / lifecycle / kanban / gitgraph …

围栏里写参数,渲染成原生 SVG —— 放大不糊,还能点进 explore 改参数。

```draw
type=bar&labels=一月,二月,三月&values=12,19,14&w=340&h=340
```

--

<!-- .slide: data-layout="two-col" -->

# 结构图也内联

```draw/seq
n=u;fe;浏览器&n=api;be;API&e=u;api;GET /draw
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 四 · 排版

代码、表格、清单、引用,都是原生的。

--

<!-- .slide: data-layout="two-col" -->

# 代码逐行聚焦

围栏信息串写步进:

- `[1|3-5]` —— 第 1 行起编号,聚焦 3–5 行
- 高亮插件负责着色,reveal 原生的行号表负责排版

```js [1|2-3]
const deck = await fetch(markdown);
render(deck);
```

--

<!-- .slide: data-layout="two-col" -->

# 表格也是版式

| 参数 | 作用 |
|---|---|
| `url` | markdown 链接 |
| `slide` | 渲染第几页 |
| `theme` | 主题 |
| `mode` | 封面图的四种样式 |

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 五 · 外观

封面、章节、宫格、整页底图 —— 每一页都能有自己的样子。

--

<!-- .slide: data-layout="gallery" data-columns="2" -->

# 四种封面图

服务端把任意一页排成矢量 SVG,还能出四种海报样式:信息卡 / 章节大纲 / 思维导图 / 关键页网格。

```text
cover.svg?mode=info|chapters|mindmap|pages
```

--

<!-- .slide: data-layout="two-col" -->

# 封面图与讲台同源

封面图不是截图,是**同一套排版引擎**另画一遍:配色走 `palette:` 机制,
几何装饰与页面外框走同一份数值 —— 所以 issue 里嵌的那张图,和点开之后
看到的那一页,是同一副样子。

| | 讲台 | 封面图 |
|---|---|---|
| 渲染 | 浏览器里的 reveal.js | 服务端排版成 SVG |
| 配色 | `--r-*` 变量 | 同一批变量 |
| 尺寸 | 跟随窗口 | 960×700(可 `?w=` `?h=`) |

--

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#24406e 0%, #16233d 48%, #0b1120 100%)" data-title="Q&A" -->

# 把 markdown 变成一场演讲

```draw
type=qr&d=https://github.com/x-cmd/ppt&fg=%230a0a12&bg=%23ffffff&w=240&h=240
```
