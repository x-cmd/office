---
theme: black
transition: fade
cover:
  title: 一屏一图
  subtitle: 把数字讲成故事 · draw 数据图全家桶
  author: x-cmd
  date: 2026-11-24
  tag: x-cmd · insight
  qr: https://github.com/x-cmd/office/issues/new
  background: aurora-ocean
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

**数字不会说话,图替它说。**

---

<!-- .slide: data-layout="two-col" -->

# 三个月,发生了什么

<span class="kicker">Chapter 01 · 增长</span>

- MAU 从 1 万涨到 2.4 万 <!-- .element: class="fragment" -->
- 增长不是广告砸出来的:自然流量占七成 <!-- .element: class="fragment" -->
- 口碑曲线开始抬头 <!-- .element: class="fragment" -->

```draw
type=line&labels=Sep,Oct,Nov&series=MAU:10000,16000,24000&t=evil-glow&w=340&h=360&num=peak
```

--

<!-- .slide: data-layout="fact" data-title="2.4×" data-background-gradient="radial-gradient(#1d4e5f 0%, #14323e 52%, #0a161c 100%)" -->

# 2.4×

三个月的增长倍数 · MAU(示例数据)

---

<!-- .slide: data-layout="two-col" -->

# 谁带来了增长

<span class="kicker">Chapter 02 · 获客</span>

- 搜索与社区是基本盘 <!-- .element: class="fragment" -->
- 口碑占两成,还在涨 <!-- .element: class="fragment" -->
- 广告只占一成(示例数据)<!-- .element: class="fragment" -->

```draw
type=pie&labels=搜索,社区,口碑,广告&values=42,26,21,11&w=340&h=340&title=获客来源
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

# 流量从哪来,到哪去

--

<!-- .slide: data-layout="statement" -->

```draw
type=sankey&labels=搜索,社区,口碑,广告,注册,试用,付费&links=搜索>注册:420;社区>注册:260;口碑>注册:210;广告>注册:110;注册>试用:620;试用>付费:180&w=800&h=380
```

**一屏一图:** 桑基图把"获客 → 付费"画成一条河(示例数据)

---

<!-- .slide: data-layout="two-col" -->

# 跟友商比,长短板

<span class="kicker">Chapter 03 · 对标</span>

- 速度与价格是我们赢的地方 <!-- .element: class="fragment" -->
- 生态是下一课(示例数据)<!-- .element: class="fragment" -->

```draw
type=radar&t=evil&labels=速度,稳定,生态,价格&series=我们:9,8,6,9&series=友商A:7,7,8,6&w=340&h=360
```

--

<!-- .slide: data-layout="fact" data-title="70%" data-background-gradient="radial-gradient(#2c4630 0%, #1c2c20 52%, #0e1610 100%)" -->

# 70%

自然流量占比 · 获客来源(示例数据)

---

<!-- .slide: data-layout="two-col" -->

# 把这张图贴进你的 deck

<span class="kicker">Copy & Paste</span>

一页 markdown,一个围栏,图就是你的(换行只为好看,写一行也行):

````text
```draw
type=line&labels=Sep,Oct,Nov
&series=MAU:10000,16000,24000
```
````

数据在链接里,改数字就改图。

--

<!-- .slide: data-layout="end" data-title="Q&A" data-background-gradient="radial-gradient(#24406e 0%, #16233d 48%, #0b1120 100%)" -->

# 把数字讲成故事

```draw
type=qr&d=https://x-cmd.com/ppt&w=240&title=x-cmd.com/ppt
```
