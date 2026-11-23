---
theme: black
cover:
  title: 一屏一图
  subtitle: 把数字讲成故事 · draw 数据图全家桶
  author: x-cmd
  date: 2026-11-23
  tag: x-cmd · insight
  qr: https://github.com/x-cmd/office/blob/main/insight.md
  background: aurora-ocean
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

**数字不会说话,图替它说。**

---

<!-- .slide: data-layout="two-col" -->

# 三个月,发生了什么

- MAU 从 1 万涨到 2.4 万 <!-- .element: class="fragment" -->
- 增长不是广告砸出来的:自然流量占七成 <!-- .element: class="fragment" -->
- 口碑曲线开始抬头 <!-- .element: class="fragment" -->

```draw
type=line&labels=Sep,Oct,Nov&series=MAU:10000,16000,24000&t=evil-glow&w=520&h=340&num=peak
```

--

<!-- .slide: data-layout="fact" data-background-gradient="radial-gradient(#1c3050 0%, #122036 55%, #0b1120 100%)" -->

# 2.4×

三个月的增长倍数 · MAU(示例数据)

---

<!-- .slide: data-layout="two-col" -->

# 谁带来了增长

广告只占一成;真正的工作是社区与口碑(示例数据)

```draw
type=pie&labels=搜索,社区,口碑,广告&values=42,26,21,11&w=480&h=360&title=获客来源
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

# 流量从哪来,到哪去

--

```draw
type=sankey&labels=搜索,社区,口碑,广告,注册,试用,付费&links=搜索>注册:420;社区>注册:260;口碑>注册:210;广告>注册:110;注册>试用:620;试用>付费:180&title=获客漏斗(示例数据)&w=880&h=420
```

---

<!-- .slide: data-layout="two-col" -->

# 跟友商比,长短板

我们赢在社区与价格;生态是下一课(示例数据)

```draw
type=radar&t=evil&labels=速度,稳定,生态,价格&series=我们:9,8,6,9&series=友商A:7,7,8,6&w=520&h=380
```

--

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#24406e 0%, #16233d 48%, #0b1120 100%)" -->

# 把数字贴进你的 deck

```draw
type=qr&d=https://x-cmd.com/ppt&w=240&title=x-cmd.com/ppt
```
