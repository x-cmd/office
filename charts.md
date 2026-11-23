---
template: deck
theme: black
cover:
  title: 图表
  subtitle: 把数据搬上讲台
  author: x-cmd
  date: 2026-11-23
  background: radial-gradient(#33245c 0%, #1d1436 55%, #0e0a18 100%)
---

<!-- .slide: data-layout="title" data-background-gradient="radial-gradient(#1c2a4a 0%, #0d1117 78%)" -->

# 图表

markdown 里的一行参数,讲台上的一张矢量图。

**两种写法:围栏,或链接。数据在图里,图在链接里。**

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 写法一:draw 围栏

## 围栏语言标成 draw,内容就是图表参数

````
```draw
type=bar&t=xcmd&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=380&title=月度活跃
```
````

服务端把它展开成**内联 SVG** —— 不是图片,是原生矢量,
放大不糊,跟主题融在一张画布里。

--

```draw
type=bar&t=xcmd&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=380&title=月度活跃
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 写法二:贴 draw 的链接

图片地址指向图表服务,同样会被内联:

[![各模块行数](https://x-cmd.com/draw?type=hbar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327&w=720&h=360&title=ppt%20各模块行数&unit=%E8%A1%8C)](https://x-cmd.com/draw/explore?type=hbar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327&w=720&h=360&title=ppt%20各模块行数&unit=%E8%A1%8C)

**外面套一层链接,图就能点** —— 跳进 draw 的 explore,
悬停看数、现场改参数。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#241a3d 0%, #0e0a18 75%)" -->

# 常用的几种型

## 折线 · 趋势

```draw
type=line&t=xcmd&labels=一季,二季,三季,四季,五季,六季&values=120,180,150,210,240,290&w=720&h=360&title=周下载量
```

--

## 饼图 · 占比

```draw
type=pie&t=xcmd&labels=bar,line,pie,radar&values=40,25,20,15&w=560&h=360&title=图型占比
```

--

## 雷达 · 评估

```draw
type=radar&t=xcmd&labels=易用,清晰,快速,可嵌入&values=90,85,88,95&w=560&h=400&title=方案评估
```

--

## 桑基 · 流动

```draw
type=sankey&t=pipeline&labels=feat,fix,docs,merged,closed&links=feat>merged:38;feat>closed:12;fix>merged:33;fix>closed:6;docs>merged:16&w=720&h=360&title=PR 生命周期
```

还有 `area` `scatter` `combo` `gauge` `mindmap` `archmap` …
图型速查见 draw 的 SKILL。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 风格:一个参数换一套皮

`t=` 同时换配色、字体、网格:

```draw
type=bar&t=opendata&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=340&title=t=opendata
```

`xcmd` · `evil` · `opendata` · `market-mono` · `pipeline` · `rank` … 十几套。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#241a3d 0%, #0e0a18 75%)" -->

# 封面图也带图表参数

任何一页都能排成 SVG 放进 README:

| 参数 | 作用 |
|---|---|
| `slide=3` | 第 3 页(展平页号) |
| `slide=4.1` | 第 4 主题的第 2 页 |
| `anim=0,2,5&freeze=5` | 依次播这三页,定格在第 5 页 |
| `dur=2` | 每页停留秒数 |

动画是 SVG 内嵌的 SMIL —— 不支持的浏览器看到定格页,永不白屏。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 真实数据:dbnomics

## 宏观数据,也是一条条链接

数字来自 [DBnomics](https://db.nomics.world),图是 draw 的 URL —— 公开、机器可读、五语界面。

**每张图都能点进 explore。**

--

## G20 · GDP 名义值(2025,USD bn)

[![G20 GDP](https://x-cmd.com/draw?type=hbar&t=opendata&labels=USA,China,Germany,Japan,India,UK,France,Italy,Canada,Brazil,Russia,Korea&values=30337.2,19534.9,4921.6,4389.3,4271.9,3730.3,3283.4,2459.6,2330.3,2307.2,2195.7,1947.1&w=780&h=440&title=G20+%C2%B7+GDP+2025&unit=USD+bn)](https://x-cmd.com/draw/explore?type=hbar&t=opendata&labels=USA,China,Germany,Japan,India,UK,France,Italy,Canada,Brazil,Russia,Korea&values=30337.2,19534.9,4921.6,4389.3,4271.9,3730.3,3283.4,2459.6,2330.3,2307.2,2195.7,1947.1&w=780&h=440&title=G20%20%C2%B7%20GDP%202025&unit=USD%20bn)

--

## 政策利率 · 三大央行

[![政策利率](https://x-cmd.com/draw/echarts?d=%7B%22title%22%3A%7B%22text%22%3A%22Policy%20rates%20%C2%B7%20year-end%20%25%22%7D%2C%22color%22%3A%5B%22%232563eb%22%2C%22%2316a34a%22%2C%22%23f59e0b%22%5D%2C%22xAxis%22%3A%7B%22data%22%3A%5B%222015%22%2C%222016%22%2C%222017%22%2C%222018%22%2C%222019%22%2C%222020%22%2C%222021%22%2C%222022%22%2C%222023%22%2C%222024%22%2C%222025%22%5D%7D%2C%22yAxis%22%3A%7B%22name%22%3A%22%25%22%7D%2C%22legend%22%3A%7B%7D%2C%22series%22%3A%5B%7B%22name%22%3A%22Fed%22%2C%22type%22%3A%22line%22%2C%22smooth%22%3Atrue%2C%22itemStyle%22%3A%7B%22color%22%3A%22%232563eb%22%7D%2C%22lineStyle%22%3A%7B%22color%22%3A%22%232563eb%22%7D%2C%22data%22%3A%5B0.38%2C0.62%2C1.38%2C2.38%1.62%2C0.12%2C0.12%2C4.38%2C5.38%2C4.38%2C4.38%5D%7D%2C%7B%22name%22%3A%22ECB%22%2C%22type%22%3A%22line%22%2C%22smooth%22%3Atrue%2C%22itemStyle%22%3A%7B%22color%22%3A%22%2316a34a%22%7D%2C%22lineStyle%22%3A%7B%22color%22%3A%22%2316a34a%22%7D%2C%22data%22%3A%5B0.05%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2C2.5%2C4.5%2C3.0%2C2.0%5D%7D%2C%7B%22name%22%3A%22BoJ%22%2C%22type%22%3A%22line%22%2C%22smooth%22%3Atrue%2C%22itemStyle%22%3A%7B%22color%22%3A%22%23f59e0b%22%7D%2C%22lineStyle%22%3A%7B%22color%22%3A%22%23f59e0b%22%7D%2C%22data%22%3A%5Bnull%2C-0.1%2C-0.1%2C-0.1%2C-0.1%2C-0.1%2C-0.1%2C-0.1%2C-0.1%2C0.25%2C0.5%5D%7D%5D%7D)](https://x-cmd.com/draw/explore/echarts?d=%7B%22title%22%3A%7B%22text%22%3A%22Policy%20rates%22%7D%7D)

--

## 命令行也能取

```text
x dbnomics data <series>      # 取一条序列
x dbnomics align <a> <b> <c>  # 把几个指标对齐
```

---

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#1c2a4a 0%, #0d1117 78%)" -->

# 下一张图,从这里开始

**https://x-cmd.com/draw**
