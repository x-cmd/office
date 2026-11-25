---
look: editorial
transition: fade
---

<!-- .slide: data-layout="ed-masthead" -->

<span class="mast">演讲<span class="vol">VOL.01 / 2026.11</span></span>

# 把 markdown<br>变成一场演讲

<span class="dek">一个长链接,就是入口。贴进 README,别人点开就能讲 —— 不装工具、不导 PDF、不发附件。</span>

<span class="byline">文 / X-CMD 研究室 · 2026 年 11 月</span>

--

<!-- .slide: data-layout="ed-article" -->

<span class="folio">03</span>

<span class="kicker">What · 这是什么</span>

# 文件的老毛病

<p class="ppt-lead body">过去十年,我们交换想法的方式是把文件丢来丢去。PPT、PDF、截图 —— 每传一次,就死掉一点:版本对不上,链接过期,字体丢失。</p>

<p class="body">发出去的是<strong>文件</strong>,收到的人看到的却是<strong>过去某一帧的你</strong>。</p>

<div class="aside">
  <b>Sidebar</b>
  装工具、导 PDF、调样式 —— 每台机器重来一遍。<br>
  三个月后,版本已经对不上了。
</div>

--

<!-- .slide: data-layout="ed-figure" -->

<span class="folio">04</span>

<span class="kicker">Figure · 旧剧本</span>

# 三步,变成三箱附件

```draw/seq
n=ai;be;AI 十分钟写完 deck;;r0c0&n=tool;ext;装工具 / 导 PDF;;r0c1&n=mail;be;发附件;;r0c2&e=ai;tool;每台机器重来一遍&e=tool;mail;对方打不开&e=mail;ai;版本对不上&title=旧剧本&w=840
```

<span class="figcap"><b>FIG.1</b> —— 从"写完"到"发出去"要跨过的三道工序。每一道都在文件上,不在内容上。</span>

--

<!-- .slide: data-layout="ed-callout" -->

<span class="kicker">By the numbers</span>

# 1

<span class="cap">一个链接,就是一场演讲。不用装软件,不用导出,不用发附件 —— 别人点开,就是一场已经准备好的演讲。</span>

<span class="src">X-CMD 研究室 ·《把 markdown 变成一场演讲》</span>

---

<!-- .slide: data-layout="ed-article" -->

<span class="folio">07</span>

<span class="kicker">How · 怎么做到</span>

# 新剧本:只贴地址

<p class="ppt-lead body">渲染搬到<strong>浏览器</strong>,输入缩成一个地址。markdown 本来就躺在仓库里 —— 缺的只是一个<strong>入口</strong>。</p>

<p class="body">内容不动,仓库不动,工具不用装。</p>

<div class="aside">
  <b>Sidebar</b>
  不想找托管?全文塞进参数也行:<br>
  <code>?content=</code> 传 URL 编码的 markdown,<br>
  一两个屏幕的短 deck,一条链接走天下。
</div>

--

<!-- .slide: data-layout="ed-figure" -->

<span class="folio">08</span>

<span class="kicker">Figure · 架构</span>

# 浏览器直读,常见路径零服务端调用

```draw/seq
n=b;fe;浏览器(讲台);;r0c0&n=gh;ext;markdown 源站;;r0c1&n=w;be;ppt Worker;;r0c2&e=b;gh;fetch 直读&e=b;w;被 CORS 挡住才回落&title=取源的两条路&w=840
```

<span class="figcap"><b>FIG.2</b> —— 源站自带 CORS 头,浏览器直读零调用;CORS 被挡才回落服务端代取(校验 Referer、限体积、限频率)。</span>

--

<!-- .slide: data-layout="ed-columns" -->

<span class="folio">09</span>

<span class="kicker">Lectern · 讲台备忘</span>

# 三件事,各占一页

<span class="cols">
  <span class="col"><b>一 · 二维分页</b><code>---</code> 横向分页是换主题,<code>--</code> 纵向分页是同一主题的下一页。系列的首屏是钩子,后面才是详情。</span>
  <span class="col"><b>二 · 图表内联</b><code>draw</code> 围栏在服务端被换成<strong>内联 SVG</strong> —— 矢量、可缩放,跟着 deck 的配色走,放大不糊。</span>
  <span class="col"><b>三 · 封面同源</b>服务端把指定那一页排成 SVG:画布 960×700,字号行高颜色取自主题 CSS,字体子集内嵌 —— 于是封面图和讲台里那一页,看着一样。</span>
</span>

--

<!-- .slide: data-layout="ed-note" -->

<span class="folio">10</span>

<span class="kicker">Margin · 一条边注</span>

# 封面不是封面

<p class="body">杂志的封面每天都要抢读者一眼。演示的封面也一样:它不是"这次讲什么"的说明,是<strong>这次讲什么</strong>本身的一句话。</p>

<div class="note">
  <b>Note</b>
  README 里的标准嵌法:<br>
  <code>[![](cover.svg)](?url=…)</code><br>
  封面永远与第一页同源同款 —— deck 改了,封面跟着变。
</div>

<span class="src">出处:X-CMD 研究室 ·《新剧本:只贴地址》</span>

---

<!-- .slide: data-layout="ed-timeline" -->

<span class="folio">13</span>

<span class="kicker">Boundary · 边界与现状</span>

# 已知限制,摆在前台

<p class="body">链接把文件的麻烦换掉了,但没有把现实换掉 —— 体积、限流、缓存,还有讲台上那些已经能用的东西,一并交代清楚。</p>

<span class="tl">
  <span class="entry"><span class="year">512K</span><span class="what">deck 体积上限</span><span class="note">一份 deck 最大 512KB,超了会被截断。</span></span>
  <span class="entry"><span class="year">6K</span><span class="what">直传 URL 上限</span><span class="note">内容直传总 URL 约 6KB 原文,长 deck 仍需托管。</span></span>
  <span class="entry"><span class="year">60/分</span><span class="what">取源限流</span><span class="note">每 IP 每分钟 60 次,共享出口容易触顶(403)。</span></span>
  <span class="entry"><span class="year">24h</span><span class="what">浏览器缓存兜底</span><span class="note">源改了放映跟着变,最长的旧版本寿命 24 小时。</span></span>
</span>

--

<!-- .slide: data-layout="ed-callout" -->

<span class="kicker">By the numbers</span>

# 0

<span class="cap">常见路径下服务端参与次数:浏览器自带 CORS 头,markdown 直接读回来 —— 零回源。只有 CORS 被挡时,才回落 Worker 代取。</span>

<span class="src">X-CMD 研究室 ·《浏览器直读》</span>

--

<!-- .slide: data-layout="ed-columns" -->

<span class="folio">15</span>

<span class="kicker">Lectern · 讲台备忘</span>

# 现状:讲台上有什么

<span class="cols">
  <span class="col"><b>键位</b><code>← →</code> 换主题,换主题内的页。<code>S</code> 演讲者备注,跨窗口同步。<code>W</code> 标注:画笔 / 荧光笔 / 划词高亮,<code>Z</code> <code>Y</code> 撤销重做,<code>ESC</code> 缩略图总览。</span>
  <span class="col"><b>标注</b>钉在<strong>页</strong>上,翻回来还在。观众屏只见内容,不见工具 —— 标注是讲者的,不是观众的。</span>
  <span class="col"><b>手机</b>另一套:竖屏画布、上下滑翻页、二维小地图。不是"缩小的桌面版",是照视频软件的用法重做的。</span>
</span>

--

<!-- .slide: data-layout="ed-colophon" -->

<span class="wordmark">演讲</span>

<span class="col c1"><b>入口</b>x-cmd.com/ppt<br>?url= 传地址<br>?content= 传原文</span>
<span class="col c2"><b>素材</b>markdown 直出<br>draw 图内联<br>reveal.js 讲台</span>
<span class="col c3"><b>案例</b>五分钟 · 图表<br>datalink · 能力全景<br>都在 gallery 里</span>

<span class="eof">— 现在就去讲一场 —</span>

```draw
type=qr&d=https://x-cmd.com/ppt&fg=%231b1712&bg=%23ffffff&w=240&h=240
```
