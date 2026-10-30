---
template: deck
theme: night
---

# draw

**把数据变成一张图** —— 数据在 URL 里,打开就是 SVG。

`https://x-cmd.com/draw?type=bar&labels=Jan,Feb&values=3,5`

---

# 一条链接,一张图

所有数据都在 URL 里:

```text
https://x-cmd.com/draw?type=bar&labels=Jan,Feb&values=3,5&w=560&h=300
```

- 打开就是 SVG —— 不用注册、不用 key、不用等编译
- 丢进 `<img>`、README、幻灯片,立刻能看
- 每张图都带 `<metadata>`,机器可读

---

# 十几种图型

| type | 图 |
|---|---|
| `bar` | 柱状图 |
| `line` | 折线图 |
| `area` | 面积图 |
| `pie` | 饼图 |
| `radar` | 雷达图 |
| `sankey` | 桑基图 |

--

## 还有这些

| type | 图 |
|---|---|
| `scatter` | 散点图 |
| `combo` | 双轴组合图 |
| `gauge` | 仪表盘 |
| `mindmap` | 思维导图 |
| `archmap` | 架构图 |

---

# 每种图型都好看

```draw
type=bar&t=xcmd&labels=Jan,Feb,Mar,Apr&values=12,19,14,23&w=560&h=300&title=月度活跃
```

--

## 折线图

```draw
type=line&t=evil&labels=1月,2月,3月,4月,5月&values=120,180,150,210,240&w=560&h=300&title=周下载量
```

--

## 饼图

```draw
type=pie&t=xcmd&labels=bar,line,pie,radar&values=40,25,20,15&w=520&h=340&title=图型占比
```

--

## 雷达图

```draw
type=radar&t=xcmd&labels=易用,清晰,快速,可嵌入&values=90,85,88,95&w=520&h=380&title=评估
```

--

## 桑基图

```draw
type=sankey&t=pipeline&labels=feat,fix,docs,merged,closed&links=feat>merged:38;feat>closed:12;fix>merged:33;fix>closed:6;docs>merged:16&w=600&h=320&title=PR 生命周期
```

---

# 十几套风格

`t=` 选风格 —— 配色、字体、网格一起换:

```text
/draw?type=bar&t=evil&labels=A,B&values=1,2
/draw?type=bar&t=opendata&labels=A,B&values=1,2
/draw?type=bar&t=market-mono&labels=A,B&values=1,2
```

`xcmd` · `evil` · `opendata` · `market-mono` · `pipeline` · `rank` · `shadcn` · `reliability` · `revenue` · `progress` …

--

## 也能直接贴链接

[![各模块行数](https://x-cmd.com/draw?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327)

套一层链接 → **点图跳到别处**(explore 里悬停看数、改参数)。

---

# 图能直接进幻灯片

ppt 的 markdown 里写围栏或图片链接,服务端就把它展开成**内联 SVG**:

```draw
type=bar&t=xcmd&labels=Jan,Feb&values=3,5&w=560&h=300
```

浏览器原生渲染 —— 矢量、可缩放、能跟主题融合。

---

# 下一个图,从这里开始

**https://x-cmd.com/draw**
