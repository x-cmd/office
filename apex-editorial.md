---
theme: black
transition: fade
style: |
  /* ── 演示的尽头是链接 · 杂志编辑风 ─────────────────────────
     纸面 #f2ede3 / 油墨 #1b1712 / 国际红 #c8361b 只给签名处。
     衬线当家:中文宋体,拉丁与数字 Fraunces;齐头线、刊号、
     导语首字下沉、目录点线 —— 全是报刊排版语言。 */

  :root {
    --r-background: #ece7db;
    --r-background-color: #f3eee4;
    --r-main-color: #1b1712;
    --r-heading-color: #1b1712;
    --r-heading-font: 'Songti SC', 'Noto Serif SC', 'SimSun', serif;
    --r-heading-gradient: linear-gradient(90deg, #1b1712 0%, #1b1712 100%);
    --r-link-color: #c8361b;

    /* 海报工具箱:装饰改用油墨色,强调色是国际红 */
    --ppt-decor-accent: 200, 54, 27;
    --ppt-decor-ink: 27, 23, 18;
    --ppt-ghost-stroke: rgba(27, 23, 18, .10);
    --ppt-d-hair-y: calc(100% - 92px);

    /* 图:浅底图跟着纸面走 */
    --ppt-chart-ink: #1b1712;
    --ppt-chart-text: #453d31;
    --ppt-chart-muted: #8a8172;
    --ppt-chart-grid: rgba(27, 23, 18, .12);
    --ppt-chart-accent: #c8361b;
    --ppt-chart-accent-2: #a8571f;
    --ppt-chart-accent-3: #6b6255;
    --ppt-chart-accent-4: #d98a4a;
    --ppt-chart-on-accent: #ffffff;
    --ppt-chart-font: 'PptFraunces', 'Songti SC', serif;
  }

  /* ── 全页骨架 ──────────────────────────────────────────────
     纸面 + 刊头线(粗一根细一根,所有页共用)。 */
  .reveal .slides section[data-layout^="ed-"] {
    height: 100%;
    display: flex !important;
    flex-direction: column;
    justify-content: center;
    box-sizing: border-box;
    text-align: left;
    background: linear-gradient(180deg, #f5f0e6 0%, #ece6d9 100%);
  }
  .reveal .slides section[data-layout^="ed-"]::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 7px;
    background: #1b1712;
    z-index: 2;
  }
  .reveal .slides section[data-layout^="ed-"]::after {
    content: '';
    position: absolute;
    top: 15px; left: 0; right: 0;
    height: 1px;
    background: rgba(27, 23, 18, .45);
    z-index: 2;
  }
  /* 眉题:markdown 里孤零零的一个 span 会被 marked 包一层 <p> ——
     定位要认那层 p(靠 :has 找到),字号字色认 span 本身。 */
  .reveal .slides section[data-layout^="ed-"] p:has(> .kicker) {
    position: absolute;
    top: 7.5%;
    left: 8%;
    margin: 0;
  }
  .reveal .slides section[data-layout^="ed-"] .kicker {
    margin: 0;
    font-family: 'PptFraunces', serif;
    font-size: 12px;
    letter-spacing: .3em;
    text-transform: uppercase;
    color: #8a8172;
  }
  /* 页码(红色角标) */
  .reveal .slides section[data-layout^="ed-"] .folio {
    position: absolute;
    top: 7%;
    right: 8%;
    font-family: 'PptFraunces', serif;
    font-size: 15px;
    color: #c8361b;
    letter-spacing: .12em;
  }
  .reveal .slides section[data-layout^="ed-"] h1 {
    font-family: 'Songti SC', 'Noto Serif SC', serif;
    font-weight: 700;
    letter-spacing: .01em;
    background-image: none;
    color: #1b1712;
    -webkit-text-stroke: 0;
  }
  .reveal .slides section[data-layout^="ed-"] p,
  .reveal .slides section[data-layout^="ed-"] li { line-height: 1.85; }

  /* ── 刊头:刊名 + 期号,巨号标题,导语,署名 ─────────────────── */
  .reveal .slides section[data-layout="ed-masthead"] .mast {
    position: absolute;
    top: 7%;
    left: 8%;
    right: 8%;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    font-family: 'Songti SC', serif;
    font-size: 26px;
    letter-spacing: .3em;
  }
  .reveal .slides section[data-layout="ed-masthead"] .mast .vol {
    font-family: 'PptFraunces', serif;
    font-size: 12px;
    color: #6b6255;
    letter-spacing: .22em;
  }
  .reveal .slides section[data-layout="ed-masthead"] h1 {
    font-size: 126px;
    line-height: 1.1;
    margin: .5em 0 .34em;
    letter-spacing: .04em;
  }
  /* 导语:左边一道国际红,像报纸的提要 */
  .reveal .slides section[data-layout="ed-masthead"] .dek {
    max-width: 27em;
    font-size: 21px;
    color: #453d31;
    line-height: 1.85;
    border-left: 4px solid #c8361b;
    padding-left: 1.1em;
    margin: 0;
  }
  .reveal .slides section[data-layout="ed-masthead"] .byline {
    position: absolute;
    bottom: 8%;
    left: 8%;
    margin: 0;
    font-family: 'PptFraunces', serif;
    font-size: 14px;
    letter-spacing: .18em;
    color: #6b6255;
  }

  /* ── 内页:首字下沉 + 侧栏注 ──────────────────────────────── */
  .reveal .slides section[data-layout="ed-article"] h1 {
    font-size: 46px;
    margin: 0 0 .5em;
  }
  .reveal .slides section[data-layout="ed-article"] .body {
    max-width: 30em;
    font-size: 21px;
    color: #2a251e;
  }
  /* 侧栏:一道细竖线分栏,像杂志的边注 */
  .reveal .slides section[data-layout="ed-article"] .aside {
    position: absolute;
    top: 26%;
    right: 8%;
    width: 21%;
    padding-left: 1.6em;
    border-left: 1px solid rgba(27, 23, 18, .28);
    font-size: 14px;
    line-height: 1.9;
    color: #6b6255;
  }
  .reveal .slides section[data-layout="ed-article"] .aside b {
    display: block;
    margin-bottom: .6em;
    font-family: 'PptFraunces', serif;
    font-size: 12px;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: #c8361b;
  }

  /* ── 引语页:红色大引号 + 衬线大句 ────────────────────────── */
  .reveal .slides section[data-layout="ed-quote"] .qmark {
    font-family: 'PptFraunces', serif;
    font-size: 168px;
    line-height: .78;
    color: #c8361b;
    display: block;
    margin: 0 0 -.12em -.07em;
  }
  .reveal .slides section[data-layout="ed-quote"] h1 {
    font-size: 62px;
    line-height: 1.5;
    max-width: 15em;
    font-weight: 700;
    margin: .1em 0 0;
  }
  .reveal .slides section[data-layout="ed-quote"] .attr {
    margin-top: 2.4em;
    font-family: 'PptFraunces', serif;
    font-size: 14px;
    letter-spacing: .22em;
    color: #6b6255;
  }
  .reveal .slides section[data-layout="ed-quote"] .attr::before {
    content: '';
    display: inline-block;
    width: 3.4em;
    height: 1px;
    background: #1b1712;
    vertical-align: middle;
    margin-right: 1em;
  }

  /* ── 目录页:点线引到页码 ─────────────────────────────────── */
  .reveal .slides section[data-layout="ed-index"] h1 {
    font-size: 46px;
    margin: 0 0 .9em;
  }
  .reveal .slides section[data-layout="ed-index"] .toc {
    display: flex;
    align-items: baseline;
    max-width: 34em;
    padding: .5em 0;
    border-bottom: 1px solid rgba(27, 23, 18, .18);
    font-size: 24px;
  }
  .reveal .slides section[data-layout="ed-index"] .toc .no {
    font-family: 'PptFraunces', serif;
    color: #c8361b;
    font-size: 19px;
    margin-right: .9em;
  }
  /* 点线引:标题与页码之间那串点 */
  .reveal .slides section[data-layout="ed-index"] .toc .lead {
    flex: 1;
    margin: 0 .8em .28em;
    border-bottom: 1px dotted rgba(27, 23, 18, .45);
  }
  .reveal .slides section[data-layout="ed-index"] .toc .pg {
    font-family: 'PptFraunces', serif;
    color: #6b6255;
    font-size: 16px;
  }

  /* ── 数据页:编辑部的大数字 ──────────────────────────────── */
  .reveal .slides section[data-layout="ed-callout"] h1 {
    font-family: 'PptFraunces', serif;
    font-weight: 600;
    font-size: 210px;
    line-height: 1;
    letter-spacing: -.02em;
    margin: .1em 0 .34em;
  }
  /* 图注:span 要变块级,max-width 才吃得到 */
  .reveal .slides section[data-layout="ed-callout"] .cap {
    display: block;
    max-width: 26em;
    padding-top: 1.1em;
    border-top: 1px solid rgba(27, 23, 18, .28);
    font-size: 23px;
    color: #453d31;
    margin: 0;
  }
  .reveal .slides section[data-layout="ed-callout"] .src {
    position: absolute;
    right: 8%;
    bottom: 8%;
    font-family: 'PptFraunces', serif;
    font-size: 13px;
    color: #8a8172;
    letter-spacing: .14em;
  }

  /* ── 图版:杂志里的图 + 图注(左右分栏) ───────────────────── */
  .reveal .slides section[data-layout="ed-figure"] h1 {
    font-size: 40px;
    margin: 0 0 .7em;
  }
  .reveal .slides section[data-layout="ed-figure"] .ppt-chart { margin: 0; }
  .reveal .slides section[data-layout="ed-figure"] .ppt-chart svg {
    max-width: 100%;
    height: auto;
  }
  .reveal .slides section[data-layout="ed-figure"] .figcap {
    margin: 1em 0 0;
    font-family: 'PptFraunces', serif;
    font-size: 13px;
    letter-spacing: .1em;
    color: #6b6255;
  }
  .reveal .slides section[data-layout="ed-figure"] .figcap b {
    color: #c8361b;
    font-weight: 600;
  }

  /* ── 版权页:刊名 + 三栏小字 + 二维码 ─────────────────────── */
  .reveal .slides section[data-layout="ed-colophon"] p:has(> .wordmark) {
    position: absolute;
    top: 11%;
    left: 8%;
    margin: 0;
  }
  .reveal .slides section[data-layout="ed-colophon"] .wordmark {
    font-family: 'Songti SC', serif;
    font-size: 60px;
    letter-spacing: .32em;
    color: #1b1712;
  }
  .reveal .slides section[data-layout="ed-colophon"] .col {
    position: absolute;
    top: 34%;
    width: 21%;
    line-height: 2.1;
    font-size: 15px;
    color: #453d31;
  }
  .reveal .slides section[data-layout="ed-colophon"] .c1 { left: 8%; }
  .reveal .slides section[data-layout="ed-colophon"] .c2 { left: 34%; }
  .reveal .slides section[data-layout="ed-colophon"] .c3 { left: 60%; }
  .reveal .slides section[data-layout="ed-colophon"] .col b {
    display: block;
    font-family: 'PptFraunces', serif;
    font-size: 11px;
    letter-spacing: .24em;
    text-transform: uppercase;
    color: #8a8172;
    margin-bottom: .9em;
  }
  .reveal .slides section[data-layout="ed-colophon"] .eof {
    position: absolute;
    bottom: 8%;
    left: 8%;
    margin: 0;
    font-family: 'PptFraunces', serif;
    font-size: 15px;
    letter-spacing: .34em;
    color: #c8361b;
  }
  .reveal .slides section[data-layout="ed-colophon"] .ppt-chart {
    position: absolute;
    right: 8%;
    bottom: 8%;
    margin: 0;
  }
  .reveal .slides section[data-layout="ed-colophon"] .ppt-chart svg {
    max-width: 132px;
    height: auto;
  }
---

<!-- .slide: data-layout="ed-masthead" -->

<span class="mast">链接<span class="vol">VOL.07 / 2026.11</span></span>

# 演示的尽头<br>是链接

<span class="dek">为什么 deck 应该像网页一样活着:一个地址,永远最新,点开就讲 —— 而不是又一个传来传去的附件。</span>

<span class="byline">文 / X-CMD 研究室 · 2026 年 11 月</span>

---

<!-- .slide: data-layout="ed-article" -->

<span class="folio">07</span>
<span class="kicker">Editorial · 本刊特稿</span>

# 文件的死法

<p class="ppt-lead body">过去十年,我们交换想法的方式是把文件丢来丢去。PPT、PDF、截图 —— 每传一次,就死掉一点:版本对不上,链接过期,字体丢失。</p>

<p class="body">发出去的是<strong>文件</strong>,收到的人看到的却是<strong>过去某一帧的你</strong>。</p>

<div class="aside">
  <b>Sidebar</b>
  一份 PPT 的平均寿命:从写完到被转发,大约 11 天。<br>一份链接的寿命:只要它还能打开。
</div>

---

<!-- .slide: data-layout="ed-quote" -->

<span class="qmark">“</span>

# 内容住在仓库里,<br>链接只是它的门。

<span class="attr">X-CMD 研究室</span>

---

<!-- .slide: data-layout="ed-index" -->

<span class="folio">09</span>
<span class="kicker">Index · 本期目录</span>

# 七个页面,一个观点

<span class="toc"><span class="no">01</span><span>文件的死法</span><span class="lead"></span><span class="pg">07</span></span> <!-- .element: class="toc fragment" -->
<span class="toc"><span class="no">02</span><span>链接的活法</span><span class="lead"></span><span class="pg">11</span></span> <!-- .element: class="toc fragment" -->
<span class="toc"><span class="no">03</span><span>封面的复兴</span><span class="lead"></span><span class="pg">19</span></span> <!-- .element: class="toc fragment" -->
<span class="toc"><span class="no">04</span><span>讲台上见</span><span class="lead"></span><span class="pg">27</span></span> <!-- .element: class="toc fragment" -->

---

<!-- .slide: data-layout="ed-callout" -->

<span class="kicker">By the numbers</span>

# 10 min

<span class="cap">从「写完 markdown」到「开场演讲」的平均距离 —— 不用装软件,不用导出,不用发附件。</span>

<span class="src">本刊编辑部实测 · 2026.11</span>

---

<!-- .slide: data-layout="ed-figure" -->

<span class="folio">19</span>
<span class="kicker">Figure · 一张图</span>

# 打开就讲

```draw
type=line&labels=Sep,Oct,Nov&series=打开即讲:62,71,84&w=820&h=360
```

<span class="figcap"><b>FIG.1</b> —— 拿到链接后 30 秒内真的开始讲的比例(%)。数据为示例。</span>

---

<!-- .slide: data-layout="ed-colophon" -->

<span class="wordmark">链接</span>

<span class="col c1"><b>出品</b>X-CMD 研究室<br>上海 / 远程</span> <!-- .element: class="col c1 fragment" -->
<span class="col c2"><b>排版</b>reveal.js<br>markdown 直出</span> <!-- .element: class="col c2 fragment" -->
<span class="col c3"><b>字体</b>得意黑 / Fraunces<br>Songti SC / Space Grotesk</span> <!-- .element: class="col c3 fragment" -->

<span class="eof">— EOF —</span>

```draw
type=qr&d=https://x-cmd.com/ppt&fg=%231b1712&bg=%23ffffff&w=240&h=240
```
