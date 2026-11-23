---
theme: black
cover:
  title: 从想法到上线
  subtitle: 交付流程一张图 · 时间轴/看板/分支/旅程
  author: x-cmd
  date: 2026-11-23
  background: aurora-forest
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

**一个版本的距离:三次演示,两次返工,一堆图。**

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#2c4630 0%, #1c2c20 52%, #0e1610 100%)" -->

# 大事记,一条时间轴

--

```draw/timeline
title=x-cmd/ppt 大事记&section=2026-09&event=2026-09|第一版|markdown 变演讲&section=2026-10&event=2026-10|issue 源|deck 住进 issue&section=2026-11&event=2026-11|预览图系统|五种海报样式&w=900&h=420
```

---

<!-- .slide: data-layout="two-col" -->

# 这一迭代,看板说了算

进行中的只有一件:预览图样式系统

```draw/kanban
title=v0.9 迭代看板&column=待办&column=进行中&column=已完成&task=待办|暗色主题打磨|&task=待办|手机小地图|&task=进行中|预览图样式系统|&task=已完成|issue 源|&task=已完成|draw 图表展开|&task=已完成|转场调柔|&w=620&h=400
```

--

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

# 分支怎么长

--

```draw/gitgraph
title=发布分支&branch=main&branch=develop&commit=one|main|v0.8 发布|&commit=two|develop|draw 图族|one&commit=three|develop|预览图|two&commit=four|main|v0.9|two&w=860&h=360
```

---

<!-- .slide: data-layout="two-col" -->

# 观众的一天

从点链接到举手,分数是心情(5 = 最好)

```draw/journey
title=从链接到掌声&section=打开&task=打开|点链接|5|观众&task=打开|扫一眼大纲|4|观众&section=放映&task=放映|跟着翻页|5|观众&task=放映|举手提问|3|观众&w=640&h=400
```

--

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#24406e 0%, #16233d 48%, #0b1120 100%)" -->

# 下一个版本,从一行 markdown 开始

**https://x-cmd.com/ppt**
