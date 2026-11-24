---
theme: black
transition: fade
style: |
  /* ── DECK AS CODE · 蓝图工程风 ─────────────────────────────
     深海军蓝图纸底 + 青色注记线 + 等宽标注。每个元素都有"图号":
     角标、刻度、REV 戳 —— 信息图(infographic)的语言,不是幻灯片。 */

  :root {
    --r-background: #060b14;
    --r-background-color: #0a1524;
    --r-main-color: #d7e6ff;
    --r-heading-color: #eaf3ff;
    --r-heading-gradient: linear-gradient(90deg, #eaf3ff 0%, #eaf3ff 100%);
    --r-link-color: #6fc3ff;

    /* 海报工具箱:装饰用青,几何细线 */
    --ppt-decor-accent: 111, 195, 255;
    --ppt-decor-ink: 111, 195, 255;
    --ppt-ghost-stroke: rgba(111, 195, 255, .12);

    /* 图:蓝图底上的图,网格线细一档 */
    --ppt-chart-ink: #eaf3ff;
    --ppt-chart-text: #a9c2e2;
    --ppt-chart-muted: #6d84a8;
    --ppt-chart-grid: rgba(111, 195, 255, .16);
    --ppt-chart-accent: #6fc3ff;
    --ppt-chart-accent-2: #4f9de0;
    --ppt-chart-accent-3: #8ec6ff;
    --ppt-chart-on-accent: #061020;
    --ppt-chart-font: 'PptSpace', 'PingFang SC', monospace;
  }

  /* ── 全页骨架:图纸 + 图框 + 图签行 ───────────────────────
     网格跟着幻灯片缩放(background-size 用 px,画布恒 960×700)。 */
  .reveal .slides section[data-layout^="tc-"] {
    height: 100%;
    display: flex !important;
    flex-direction: column;
    justify-content: center;
    box-sizing: border-box;
    text-align: left;
    background-color: #0a1524;
    background-image:
      linear-gradient(rgba(111, 195, 255, .05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(111, 195, 255, .05) 1px, transparent 1px),
      linear-gradient(rgba(111, 195, 255, .10) 1px, transparent 1px),
      linear-gradient(90deg, rgba(111, 195, 255, .10) 1px, transparent 1px);
    background-size: 40px 40px, 40px 40px, 200px 200px, 200px 200px;
  }
  /* 图框:内框 + 四角角标(蓝图注册标记) */
  .reveal .slides section[data-layout^="tc-"]::before {
    content: '';
    position: absolute;
    inset: 14px;
    pointer-events: none;
    z-index: 0;
    border: 1px solid rgba(111, 195, 255, .30);
    background:
      linear-gradient(to right, #6fc3ff 0 14px, transparent 14px) top left / 14px 2px,
      linear-gradient(to bottom, #6fc3ff 0 14px, transparent 14px) top left / 2px 14px,
      linear-gradient(to left, #6fc3ff 0 14px, transparent 14px) top right / 14px 2px,
      linear-gradient(to bottom, #6fc3ff 0 14px, transparent 14px) top right / 2px 14px,
      linear-gradient(to right, #6fc3ff 0 14px, transparent 14px) bottom left / 14px 2px,
      linear-gradient(to top, #6fc3ff 0 14px, transparent 14px) bottom left / 2px 14px,
      linear-gradient(to left, #6fc3ff 0 14px, transparent 14px) bottom right / 14px 2px,
      linear-gradient(to top, #6fc3ff 0 14px, transparent 14px) bottom right / 2px 14px;
    background-repeat: no-repeat;
  }
  /* 图签行:每页顶部一行等宽小字(DOC 号 / REV / 比例) */
  .reveal .slides section[data-layout^="tc-"] .sheet-head {
    position: absolute;
    top: 5.5%;
    left: 8%;
    right: 8%;
    display: flex;
    justify-content: space-between;
    font-family: var(--ppt-tech-font);
    font-size: 11px;
    letter-spacing: .2em;
    color: #6d84a8;
    z-index: 1;
  }
  .reveal .slides section[data-layout^="tc-"] h1 {
    font-family: var(--ppt-tech-font);
    font-weight: 500;
    letter-spacing: .06em;
    background-image: none;
    color: #eaf3ff;
    -webkit-text-stroke: 0;
  }
  .reveal .slides section[data-layout^="tc-"] h1 b { font-weight: 700; color: #6fc3ff; }
  /* 左缘的青色标注尺:每页一根,像图纸的索引线 */
  .reveal .slides section[data-layout^="tc-"] .ruler {
    position: absolute;
    top: 18%;
    bottom: 18%;
    left: 8%;
    width: 1px;
    background: linear-gradient(180deg, transparent, rgba(111, 195, 255, .45) 12%, rgba(111, 195, 255, .45) 88%, transparent);
  }
  .reveal .slides section[data-layout^="tc-"] .ruler::before {
    content: '';
    position: absolute;
    top: 0; left: -3px;
    width: 7px; height: 7px;
    border-radius: 50%;
    background: #6fc3ff;
    box-shadow: 0 0 8px 1px rgba(111, 195, 255, .6);
  }

  /* ── 封面:标题块 + REV 戳 ──────────────────────────────── */
  .reveal .slides section[data-layout="tc-title"] h1 {
    font-size: 116px;
    line-height: 1.02;
    letter-spacing: .02em;
    margin: 1.4em 0 .4em;
  }
  .reveal .slides section[data-layout="tc-title"] h2 {
    font-size: 22px;
    font-weight: 400;
    color: #9db4d4;
    letter-spacing: .08em;
    margin: 0;
  }
  .reveal .slides section[data-layout="tc-title"] .rev {
    position: absolute;
    bottom: 7%;
    left: 8%;
    font-family: var(--ppt-tech-font);
    font-size: 12px;
    letter-spacing: .22em;
    color: #6fc3ff;
  }

  /* ── 规格表:表头宽字距,行线青色减淡 ─────────────────────── */
  .reveal .slides section[data-layout="tc-spec"] h1 { font-size: 34px; margin: 0 0 .8em; }
  .reveal .slides section[data-layout="tc-spec"] table { width: 100%; font-size: 19px; }
  .reveal .slides section[data-layout="tc-spec"] th {
    font-family: var(--ppt-tech-font);
    font-weight: 500;
    letter-spacing: .2em;
    text-transform: uppercase;
    font-size: 12px;
    color: #6fc3ff;
    text-align: left;
  }
  .reveal .slides section[data-layout="tc-spec"] td,
  .reveal .slides section[data-layout="tc-spec"] th {
    border-bottom: 1px solid rgba(111, 195, 255, .22);
    padding: .72em .4em;
    vertical-align: top;
  }
  .reveal .slides section[data-layout="tc-spec"] td:first-child {
    font-family: var(--ppt-tech-font);
    color: #6fc3ff;
    width: 22%;
  }

  /* ── 图页:结构图居中,图号在左下 ────────────────────────── */
  .reveal .slides section[data-layout="tc-figure"] h1 { font-size: 30px; margin: 0 0 .9em; }
  .reveal .slides section[data-layout="tc-figure"] .ppt-chart { margin: 0; }
  .reveal .slides section[data-layout="tc-figure"] .ppt-chart svg { max-width: 100%; height: auto; }
  .reveal .slides section[data-layout="tc-figure"] .figcap {
    position: absolute;
    left: 8%;
    bottom: 7%;
    margin: 0;
    font-family: var(--ppt-tech-font);
    font-size: 12px;
    letter-spacing: .2em;
    color: #6fc3ff;
  }
  .reveal .slides section[data-layout="tc-figure"] .figcap b { color: #eaf3ff; font-weight: 500; }

  /* ── 键位页:键帽 chips ─────────────────────────────────── */
  .reveal .slides section[data-layout="tc-keys"] h1 { font-size: 34px; margin: 0 0 1em; }
  .reveal .slides section[data-layout="tc-keys"] .key {
    display: inline-block;
    min-width: 2.4em;
    text-align: center;
    border: 1px solid rgba(111, 195, 255, .55);
    border-bottom-width: 3px;
    border-radius: 6px;
    font-family: var(--ppt-tech-font);
    font-size: 17px;
    color: #eaf3ff;
    padding: .32em .55em;
    background: rgba(111, 195, 255, .08);
  }
  .reveal .slides section[data-layout="tc-keys"] table { font-size: 20px; }
  .reveal .slides section[data-layout="tc-keys"] td {
    border: 0;
    padding: .5em 1.4em .5em 0;
    color: #a9c2e2;
  }
  .reveal .slides section[data-layout="tc-keys"] td:first-child { width: 26%; }

  /* ── 约束页:编号 + 细线,像图纸的 NOTES 栏 ───────────────── */
  .reveal .slides section[data-layout="tc-notes"] h1 { font-size: 34px; margin: 0 0 1em; }
  .reveal .slides section[data-layout="tc-notes"] .note {
    display: flex;
    align-items: baseline;
    gap: 1.3em;
    border-bottom: 1px solid rgba(111, 195, 255, .22);
    padding: .7em 0;
    font-size: 21px;
    color: #cfe0f7;
  }
  .reveal .slides section[data-layout="tc-notes"] .note .no {
    font-family: var(--ppt-tech-font);
    color: #6fc3ff;
    font-size: 14px;
    letter-spacing: .12em;
    flex: none;
  }

  /* ── 结尾:EOF 戳 + 二维码 ──────────────────────────────── */
  .reveal .slides section[data-layout="tc-eof"] .endmark {
    font-family: var(--ppt-tech-font);
    font-weight: 700;
    font-size: 168px;
    letter-spacing: .04em;
    color: #eaf3ff;
    margin: 1em 0 .2em;
  }
  .reveal .slides section[data-layout="tc-eof"] .endmark::after {
    content: '■';
    color: #6fc3ff;
    font-size: .26em;
    vertical-align: .9em;
    margin-left: .24em;
  }
  .reveal .slides section[data-layout="tc-eof"] .sub {
    font-family: var(--ppt-tech-font);
    font-size: 13px;
    letter-spacing: .22em;
    color: #6d84a8;
  }
  .reveal .slides section[data-layout="tc-eof"] .ppt-chart {
    position: absolute;
    right: 8%;
    bottom: 9%;
    margin: 0;
  }
  .reveal .slides section[data-layout="tc-eof"] .ppt-chart svg {
    max-width: 150px;
    height: auto;
  }
---

<!-- .slide: data-layout="tc-title" -->

<span class="sheet-head"><span>X-CMD/PPT · SPEC SHEET</span><span>REV 2026-11</span></span>

# DECK<br><b>AS CODE</b>

## 把一份演示当成一个软件构件来管理

<span class="rev">DWG № 2026-1114 · SCALE 1:1 · SHEET 1/6</span>

---

<!-- .slide: data-layout="tc-spec" -->

<span class="sheet-head"><span>§1 · GENERAL</span><span>总体规格</span></span>

# 输入与输出

| 项 | 规格 |
|---|---|
| 输入 | 一个 URL(issue / PR / release / raw)或 `?content=` 全文 |
| 输出 | reveal.js 6 演示 + 封面 SVG + info 预览页 |
| 渲染 | 浏览器直读源站;CORS 受阻才回落服务端代取 |
| 图表 | x-cmd/draw 数据图与结构图,draw 围栏内联矢量 SVG |
| 体积 | 单 deck 无硬性上限;取图限 4MB |

---

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§2 · PIPELINE</span><span>渲染管线</span></span>

# 一次请求的旅程

```draw/seq
n=browser;fe;Browser;;r0c0&n=gh;ext;GitHub raw;;r0c1&n=draw;be;draw;;r0c2&e=browser;gh;GET markdown&e=browser;draw;GET /draw&e=draw;browser;SVG;dash&title=Render pipeline&w=840
```

<span class="figcap"><b>FIG.1</b> — RENDER PIPELINE · 常见路径零服务端参与</span>

---

<!-- .slide: data-layout="tc-keys" -->

<span class="sheet-head"><span>§3 · OPERATION</span><span>讲台操作面</span></span>

# 键位

| 键 | 功能 |
|---|---|
| <span class="key">←</span> <span class="key">→</span> | 换页 |
| <span class="key">S</span> | 演讲者备注(跨窗口同步)|
| <span class="key">W</span> | 标注:画笔 / 荧光 / 划词 |
| <span class="key">ESC</span> | 缩略图总览 |

---

<!-- .slide: data-layout="tc-notes" -->

<span class="sheet-head"><span>§4 · CONSTRAINTS</span><span>设计约束</span></span>

# NOTES

<span class="note"><span class="no">N-01</span>输入只能是 URL 或 markdown —— 不接受二进制附件</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-02</span>注释即停用;指令注释(`.slide` / `.element`)是语法</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-03</span>图表内联为矢量 SVG,缩放不糊</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-04</span>版式即海报:几何装饰由模板统一提供,deck 只写内容</span> <!-- .element: class="note fragment" -->

---

<!-- .slide: data-layout="tc-eof" -->

<span class="sheet-head"><span>END OF DOCUMENT</span><span>X-CMD/PPT</span></span>

<span class="endmark">EOF</span>

<span class="sub">SHEET 6/6 · 源文件在仓库里,链接永远指向最新版</span>

```draw
type=qr&d=https://x-cmd.com/ppt&fg=%230a1524&bg=%23ffffff&w=240&h=240
```
