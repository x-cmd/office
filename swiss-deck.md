---
look: swiss
---

<!-- .slide: data-layout="sw-statement" -->

# 一张纸,<br>只讲<em>一件事</em>

瑞士国际主义的规矩只有三条:一张纸、一套网格、一个想法。

讲台上的每一页,只讲一件事。

--

<!-- .slide: data-layout="sw-grid" -->

# 为什么是减法

<div class="sw-grid">
<span class="cell"><span class="no">01</span><span class="t">一页一义</span><span class="d">观众不需要记标题,标题就是这一页的结论。</span></span>
<span class="cell"><span class="no">02</span><span class="t">位置说话</span><span class="d">靠左缘、靠字号、靠间距讲清楚,不加装饰性元素。</span></span>
<span class="cell"><span class="no">03</span><span class="t">对齐说话</span><span class="d">所有元素咬在同一条左缘上,页面自己就整齐了。</span></span>
<span class="cell"><span class="no">04</span><span class="t">留白说话</span><span class="d">空白不是没内容,是让唯一的内容被看见。</span></span>
</div>

--

<!-- .slide: data-layout="sw-quote" -->

<span class="sw-qmark">“</span>

# 版面上每一个元素,<br>都应该<em>有存在的理由</em>。

<span class="sw-attr">Müller-Brockmann · Grid Systems</span>

---

<!-- .slide: data-layout="sw-statement" -->

# 一套网格,<br>一个<em>共同</em>的坐标系

十二栏就够了。栏数不是越多越灵活,越少越可控。

--

<!-- .slide: data-layout="sw-spec" -->

# 十二栏怎么用

<span class="row"><span class="k">Grid</span><span class="v">12 栏,栏间距 1.4em;左右版心各 72px</span></span>
<span class="row"><span class="k">Full</span><span class="v">12 栏通栏 —— 图、表、代码块</span></span>
<span class="row"><span class="k">Half</span><span class="v">6 + 6 —— 左文右图,或左右对照</span></span>
<span class="row"><span class="k">Third</span><span class="v">4 + 4 + 4 —— 三项并列、指标条</span></span>
<span class="row"><span class="k">Offset</span><span class="v">2 + 8 / 8 + 2 —— 侧栏注记</span></span>
<span class="row"><span class="k">Baseline</span><span class="v">正文行距 1.6em,跨栏时基线不断</span></span>

--

<!-- .slide: data-layout="sw-figure" -->

# 分栏与基线

```draw
type=hbar&t=base&labels=标题,一级正文,二级正文,图注,页码&values=88,40,26,17,11&w=820&h=300&title=字阶%20与%20基线
```

<span class="sw-note"><b>FIG.1</b> — 五个字号层级,行距统一 1.6em。跨栏的文字共用同一条基线,页就不会散。</span>

--

<!-- .slide: data-layout="sw-index" -->

# 一场演讲的目录

<span class="item"><span class="no">01</span><span class="t">一张纸</span><span class="lead"></span><span class="pg">01</span></span>
<span class="item"><span class="no">02</span><span class="t">一套网格</span><span class="lead"></span><span class="pg">04</span></span>
<span class="item"><span class="no">03</span><span class="t">一个想法</span><span class="lead"></span><span class="pg">08</span></span>
<span class="item"><span class="no">04</span><span class="t">落地</span><span class="lead"></span><span class="pg">12</span></span>

---

<!-- .slide: data-layout="sw-statement" -->

# 一个想法,<br>需要<em>对比</em>才立得住

同一句话,写在 26px 里是信息,写在 88px 里才是主张。

--

<!-- .slide: data-layout="sw-spec" -->

# 字号阶梯

<span class="row"><span class="k">Display</span><span class="v">88px / 3.4em —— 一页只有一个</span></span>
<span class="row"><span class="k">Headline</span><span class="v">40px / 1.55em —— 结论句</span></span>
<span class="row"><span class="k">Body</span><span class="v">26px / 1em —— 正文,每行不超过 34 个汉字</span></span>
<span class="row"><span class="k">Caption</span><span class="v">17px —— 图注与标签</span></span>
<span class="row"><span class="k">Folio</span><span class="v">13px —— 页码、眉题、署名</span></span>

--

<!-- .slide: data-layout="sw-figure" -->

# 留白也是内容

```draw
type=bar&labels=标题区,主体区,留白区&values=22,46,32&w=760&h=280&title=一页纸的面积分配
```

<span class="sw-note"><b>FIG.2</b> — 主体区只占四成半,剩下的是标题与留白。留白被挤到一成,这一页就挤了。</span>

--

<!-- .slide: data-layout="sw-quote" -->

<span class="sw-qmark">“</span>

# 空白不是没装东西,<br>是<em>给装进去的东西</em>让路。

<span class="sw-attr">Swiss Design · 1950s</span>

---

<!-- .slide: data-layout="sw-statement" -->

# 落地:<br>一页到底<em>装什么</em>

先定这一页的结论,再决定版面 —— 而不是反过来。

--

<!-- .slide: data-layout="sw-grid" -->

# 一页的标准结构

<div class="sw-grid">
<span class="cell"><span class="no">01</span><span class="t">标题</span><span class="d">这一页的结论,不是话题。写在左缘,1.55em。</span></span>
<span class="cell"><span class="no">02</span><span class="t">主体</span><span class="d">一张图,或一段不超过六行的文字。二选一当主角。</span></span>
<span class="cell"><span class="no">03</span><span class="t">注解</span><span class="d">图注、口径、出处。17px,贴着一根发丝线。</span></span>
<span class="cell"><span class="no">04</span><span class="t">签名</span><span class="d">页码与栏目的小字,钉在右上或左下。</span></span>
</div>

--

<!-- .slide: data-layout="sw-spec" -->

# 常见的六个毛病

<span class="row"><span class="k">01</span><span class="v">一页两个观点 —— 拆成两页</span></span>
<span class="row"><span class="k">02</span><span class="v">居中排版 —— 瑞士式没有居中</span></span>
<span class="row"><span class="k">03</span><span class="v">标题写成话题 —— 换成结论句</span></span>
<span class="row"><span class="k">04</span><span class="v">字号比太近 —— 拉大到 2 倍以上</span></span>
<span class="row"><span class="k">05</span><span class="v">左缘不齐 —— 全部咬死一条线</span></span>
<span class="row"><span class="k">06</span><span class="v">留白不够 —— 删一半元素再试</span></span>

--

<!-- .slide: data-layout="sw-timeline" -->

# 排完之后的四道检查

<div class="sw-tl">
<span class="node"><span class="yr">01</span><span class="stage">一句话</span><span class="note">这页讲什么?一句话讲不清,就是还没想清楚。</span></span>
<span class="node"><span class="yr">02</span><span class="stage">两条线</span><span class="note">所有元素是不是咬在同一条左缘上?</span></span>
<span class="node"><span class="yr">03</span><span class="stage">三个数</span><span class="note">字阶拉开了吗?最大的和最小的差三倍了吗?</span></span>
<span class="node"><span class="yr">04</span><span class="stage">四成半</span><span class="note">主体区还剩四成半的面积吗?</span></span>
</div>

--

<!-- .slide: data-layout="sw-end" -->

# 一张纸,<br>一套网格,<br><em>一个想法</em>

<span class="sw-foot">x-cmd.com/ppt · 2026</span>
