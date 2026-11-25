---
theme: black
look: blueprint
transition: fade
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
