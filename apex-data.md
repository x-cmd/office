---
theme: black
transition: fade
style: |
  /* ── 增长账本 · 发布会数字风 ────────────────────────────────
     近黑底 / 白字 / 唯一渐变只给数字。字阶对比拉满:300px 的巨号数字
     配 11px 的小注;发丝线做结构,不要装饰纹样。

     字体分工(全 deck 只有这三支):
       数字与拉丁  Space Grotesk —— 几何、等宽数字,像仪表读数
       中文大字   得意黑        —— 招牌斜体,海报的那股劲
       中文正文   苹方(系统)    —— 中性,不抢戏
     图里的颜色跟着 deck 走(draw 的 --d-* 变量被模板桥接过)。 */

  :root {
    --r-background: #030306;
    --r-background-color: #050507;
    --r-main-color: #e9ebf1;
    --r-heading-color: #ffffff;
    --r-link-color: #8ea6ff;
    --r-heading-gradient: linear-gradient(100deg, #6e8bff 0%, #9a7bff 52%, #c06bff 100%);

    /* 海报工具箱:装饰的强调色 = deck 的蓝紫 */
    --ppt-decor-accent: 110, 139, 255;
    --ppt-decor-ink: 157, 180, 232;
    --ppt-ghost-stroke: rgba(150, 170, 240, .10);
    /* 底部发丝线抬高一档,让开钉在左下的页脚 */
    --ppt-d-hair-y: calc(100% - 96px);

    /* 图:跟着 deck 的底色与配色走,不看系统明暗 */
    --ppt-chart-ink: #f4f6fa;
    --ppt-chart-text: #c6ccdb;
    --ppt-chart-muted: #79808f;
    --ppt-chart-grid: rgba(255, 255, 255, .085);
    --ppt-chart-accent: #6e8bff;
    --ppt-chart-accent-2: #9a7bff;
    --ppt-chart-accent-3: #c06bff;
    --ppt-chart-accent-4: #4f7fe0;
    --ppt-chart-accent-5: #8ec6ff;
    --ppt-chart-on-accent: #06060c;
    --ppt-chart-font: 'PptSpace', 'PingFang SC', sans-serif;
  }

  /* ── 全页骨架 ──────────────────────────────────────────────
     整页高 + 居中(绝对定位的参照系才是整页);眉题钉左上、页脚钉左下,
     主体占左侧两栏,右侧留一条注记栏。 */
  .reveal .slides section[data-layout^="ad-"] {
    height: 100%;
    display: flex !important;
    flex-direction: column;
    justify-content: center;
    box-sizing: border-box;
    text-align: left;
  }
  /* 眉题:markdown 里孤零零的一个 span 会被 marked 包一层 <p> ——
     定位要认那层 p(靠 :has 找到),字号字色认 span 本身。 */
  .reveal .slides section[data-layout^="ad-"] p:has(> .kicker) {
    position: absolute;
    top: 7%;
    left: 8%;
    margin: 0;
  }
  .reveal .slides section[data-layout^="ad-"] .kicker {
    margin: 0;
    font-family: var(--ppt-tech-font);
    font-size: 11px;
    letter-spacing: .34em;
    color: #6b7180;
  }
  .reveal .slides section[data-layout^="ad-"] h1 {
    font-family: var(--ppt-tech-font);
    font-weight: 600;
    letter-spacing: -.05em;
    line-height: .92;
    margin: 0;
  }
  /* 数字后缀(×、%、min):小一号并抬起,挂在字身的中腰 */
  .reveal .slides section[data-layout^="ad-"] h1 .unit {
    font-size: .38em;
    letter-spacing: 0;
    margin-left: .05em;
    position: relative;
    top: -.55em;
  }
  /* 钉在左下的页脚:小字、宽字距,跟巨号数字拉开两档 */
  .reveal .slides section[data-layout^="ad-"] .ppt-bl {
    margin: 0;
    font-family: var(--ppt-tech-font);
    font-size: 12px;
    letter-spacing: .22em;
    color: #6b7180;
  }
  /* 图注:markdown 里是一个 span,marked 会包一层 <p> —— 那层 p 得零边距,
     否则会在版心里占出空当(整页 flex 居中会被顶偏)。 */
  .reveal .slides section[data-layout^="ad-"] p:has(> .figcap) { margin: 0; }
  .reveal .slides section[data-layout^="ad-"] .figcap {
    font-family: var(--ppt-tech-font);
    font-size: 11px;
    letter-spacing: .2em;
    color: #6b7180;
  }
  .reveal .slides section[data-layout^="ad-"] .figcap b { color: #8ea6ff; font-weight: 500; }

  /* ── 封面:巨号倍数 + 一行小注,右栏是这一期的注脚 ─────────── */
  .reveal .slides section[data-layout="ad-hero"] h1 {
    font-size: 296px;
    margin: 0 0 .16em;
  }
  .reveal .slides section[data-layout="ad-hero"] h2 {
    font-family: 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', sans-serif;
    font-size: 32px;
    font-weight: 400;
    color: #b9bfce;
    letter-spacing: .01em;
    margin: 0;
  }

  /* ── 大数字页:数字与说明,右栏放口径与环比 ───────────────── */
  .reveal .slides section[data-layout="ad-stat"] h1 {
    font-size: 268px;
    margin: 0 0 .1em;
  }
  .reveal .slides section[data-layout="ad-stat"] .cap {
    display: block;
    font-size: 24px;
    color: #cfd4e0;
    margin: 0;
  }
  /* 右栏里的两根小条:环比的粗略对比(手搓,不用图) */
  .reveal .slides section .cmp { margin: 1.1em 0 0; }
  .reveal .slides section .cmp .row {
    display: flex; align-items: center; gap: .8em; margin: .45em 0;
    font-family: var(--ppt-tech-font); font-size: 12px; letter-spacing: .1em;
    color: #6b7180;
  }
  .reveal .slides section .cmp .track {
    flex: 1; height: 3px; background: rgba(255, 255, 255, .10); border-radius: 2px;
  }
  .reveal .slides section .cmp .fill { display: block; height: 100%; border-radius: 2px; }
  .reveal .slides section .cmp .now .fill { background: linear-gradient(90deg, #6e8bff, #c06bff); }
  .reveal .slides section .cmp .was .fill { background: #454b5c; }

  /* ── 图表页:一张大图撑满版心,图注钉左下 ─────────────────── */
  .reveal .slides section[data-layout="ad-chart"] .ppt-chart { margin: 0; }
  .reveal .slides section[data-layout="ad-chart"] .ppt-chart svg {
    max-width: 100%;
    height: auto;
  }
  .reveal .slides section[data-layout="ad-chart"] .figcap {
    position: absolute;
    left: 8%;
    bottom: 9%;
    margin: 0;
  }
  /* 图表页的图压到版心的中带,上下留白匀 */
  .reveal .slides section[data-layout="ad-chart"] .ppt-chart {
    margin-top: 1.6em;
  }

  /* ── 构成页:饼图在左,注记栏在右 ─────────────────────────── */
  .reveal .slides section[data-layout="ad-mix"] .ppt-chart {
    margin: 0;
    align-self: start;
  }
  .reveal .slides section[data-layout="ad-mix"] .ppt-chart svg {
    max-width: 600px;
    height: auto;
  }
  /* 饼图自己带图例,右栏只放结论,不重复图例 */
  .reveal .slides section[data-layout="ad-mix"] .ppt-rail { top: 30%; }

  /* ── 三连指标:三栏横贯,每栏一根发丝线打头 ───────────────── */
  .reveal .slides section[data-layout="ad-trio"] .ppt-grid { width: 100%; }
  .reveal .slides section[data-layout="ad-trio"] .cell {
    border-top: 1px solid rgba(157, 180, 232, .22);
    padding-top: 1.1em;
  }
  .reveal .slides section[data-layout="ad-trio"] .cell .num {
    display: block;
    font-family: var(--ppt-tech-font);
    font-weight: 600;
    font-size: 82px;
    letter-spacing: -.04em;
    line-height: 1;
    color: #fff;
  }
  .reveal .slides section[data-layout="ad-trio"] .cell .lab {
    display: block;
    margin-top: 1.1em;
    font-size: 14px;
    color: #8a90a2;
    letter-spacing: .12em;
  }

  /* ── 宣言页:一句话两行,第二行刷渐变,巨字在背后当回声 ─────── */
  .reveal .slides section[data-layout="ad-manifesto"] {
    align-items: flex-start;
    --ppt-ghost-stroke: rgba(150, 170, 240, .07);
  }
  .reveal .slides section[data-layout="ad-manifesto"] h1 {
    font-family: var(--ppt-display-font);
    font-size: 92px;
    font-weight: 400;
    line-height: 1.28;
    letter-spacing: .01em;
    color: #eef0f6;
    background-image: none;
    -webkit-text-stroke: 0;
    z-index: 1;
  }
  .reveal .slides section[data-layout="ad-manifesto"] h1 .grad {
    background-image: var(--r-heading-gradient);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
  }
  .reveal .slides section[data-layout="ad-manifesto"] .sign {
    margin-top: 2.4em;
    font-family: var(--ppt-tech-font);
    font-size: 12px;
    letter-spacing: .28em;
    color: #6b7180;
  }

  /* ── 结尾:URL 巨字 + 二维码卡钉右下 ─────────────────────── */
  .reveal .slides section[data-layout="ad-end"] h1 {
    font-size: 132px;
    margin: .5em 0 0;
  }
  .reveal .slides section[data-layout="ad-end"] .bye {
    font-family: var(--ppt-tech-font);
    font-size: 12px;
    letter-spacing: .3em;
    color: #6b7180;
    margin: 0;
  }
  .reveal .slides section[data-layout="ad-end"] .ppt-chart {
    position: absolute;
    right: 8%;
    bottom: 10%;
    margin: 0;
  }
  .reveal .slides section[data-layout="ad-end"] .ppt-chart svg {
    max-width: 168px;
    height: auto;
  }
---

<!-- .slide: data-layout="ad-hero" data-title="INSIGHT" class="ppt-decor ppt-decor--glow ppt-decor--rings ppt-decor--hairline ppt-ghost ppt-ghost--br" -->

<span class="kicker">X-CMD INSIGHT · VOL.03</span>

# 2.4<span class="unit">×</span>

## MAU 月度增长倍数 · 自然流量占七成

<div class="ppt-rail">
  <span class="ppt-label">ISSUE 03</span>
  <b>增长账本</b>
  <p>三个月,月活从 1 万到 2.4 万。增长不是广告砸出来的 —— 自然流量占七成,广告预算同比降 18%。</p>
</div>

x-cmd.com/insight <!-- .element: class="ppt-abs ppt-bl" -->

---

<!-- .slide: data-layout="ad-stat" data-title="73%" -->

<span class="kicker">ACQUISITION · 获客</span>

# 73<span class="unit">%</span>

<span class="cap">自然流量带来的新用户占比</span>

<div class="ppt-rail">
  <span class="ppt-label">环比</span>
  <div class="cmp">
    <div class="row now"><span>本月</span><span class="track"><i class="fill" style="width:73%"></i></span><span>73%</span></div>
    <div class="row was"><span>上月</span><span class="track"><i class="fill" style="width:58%"></i></span><span>58%</span></div>
  </div>
  <b>口碑在替我们打广告</b>
  <p>连续四个月,自然流量占比都在涨。</p>
</div>

---

<!-- .slide: data-layout="ad-chart" data-title="MAU" -->

<span class="kicker">MAU · 近 90 天</span>

```draw
type=line&labels=Sep,Oct,Nov&series=MAU:10000,16000,24000&t=evil-glow&w=880&h=360&num=peak
```

<span class="figcap"><b>FIG.01</b> — MAU 月度活跃(千)· 10 月 24 日社区帖破圈后曲线抬头</span> <!-- .element: class="figcap ppt-abs ppt-bl" -->

---

<!-- .slide: data-layout="ad-trio" data-title="SIDE BY SIDE" -->

<span class="kicker">SIDE BY SIDE · 三个侧面</span>

<div class="ppt-grid">
  <div class="cell ppt-col-4"><span class="num">1.2M</span><span class="lab">容器镜像拉取 / 月</span></div>
  <div class="cell ppt-col-4"><span class="num">+1,844</span><span class="lab">新增 Star / 月</span></div>
  <div class="cell ppt-col-4"><span class="num">38<span class="unit" style="font-size:.5em">min</span></span><span class="lab">Issue 首次响应中位</span></div>
</div>

<span class="figcap">示例数据 · 2026 年 11 月</span> <!-- .element: class="figcap ppt-abs ppt-br" -->

---

<!-- .slide: data-layout="ad-manifesto" data-title="口碑" class="ppt-ghost ppt-ghost--center" -->

<h1>广告买得来曝光,<br><span class="grad">买不来口碑。</span></h1>

<span class="sign">增长账本 · 第 03 期 · 完</span>

---

<!-- .slide: data-layout="ad-mix" data-title="MIX" -->

<span class="kicker">MIX · 获客构成</span>

```draw
type=pie&labels=搜索,社区,口碑,广告&values=42,26,21,11&w=640&h=420
```

<div class="ppt-rail">
  <span class="ppt-label">结论</span>
  <b>口碑是最贵的一块</b>
  <p>占比只有两成,却贡献了四成的复购 —— 它不花钱,是别人替我们说的。</p>
</div>

---

<!-- .slide: data-layout="ad-end" data-title="THANKS" -->

<span class="bye">THANKS · 提问请扫码</span>

# x-cmd.com

```draw
type=qr&d=https://github.com/x-cmd/ppt/issues/new&fg=%2310131c&bg=%23ffffff&w=240&h=240
```
