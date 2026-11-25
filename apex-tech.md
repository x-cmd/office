---
theme: black
look: blueprint
transition: fade
---

<!-- .slide: data-layout="tc-title" -->

<span class="sheet-head"><span>X-CMD/PPT · SPEC SHEET</span><span>REV 2026-11</span></span>

# DECK<br><b>AS CODE</b>

## 把一份演示当成一个软件构件来管理

<span class="rev">DWG № 2026-1114 · SCALE 1:1 · SHEET 1/12</span>

--

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

--

<!-- .slide: data-layout="tc-spec" -->

<span class="sheet-head"><span>§1 · GENERAL</span><span>为什么是链接</span></span>

# 一条 URL,一份永远最新的演示

<p class="ppt-lead">演示最常见的死法不是「讲得不好」,而是「版本对不上」:发出去的 PDF 是三周前的,同事看的是旧数据。</p>

| 载体 | 传阅方式 | 过期风险 |
|---|---|---|
| PDF / PPTX | 邮件附件,来回转发 | 高 —— 每次转发都是一个副本 |
| 在线文档 | 链接 | 低 —— 但只能读,不能讲 |
| 本仓库的 deck | 链接 | 无 —— 源文件改了就跟着变 |

---

<!-- .slide: data-layout="tc-matrix" -->

<span class="sheet-head"><span>§2 · PARAMETERS</span><span>参数矩阵</span></span>

# URL 参数一览

| 参数 | 取值 | 说明 |
|---|---|---|
| `url` | 任意 markdown 链接 | 内容源;GitHub blob 自动转 raw |
| `content` | URL 编码的全文 | 短 deck 直传,绕开回源 |
| `template` | deck / center / plain | 版面模板,默认 deck |
| `theme` | 14 款内置主题 | 默认 black(自研) |
| `slide` | 展平页号或 1.2 | 服务端出图定位到某一页 |
| `anim` / `freeze` | 页号列表 | 播几页后定格,用于静帧 |
| `w` / `h` | 960 × 700 | 画布尺寸,封面图按它出 |
| `present` | 1 | 打开即收起信息栏 |

--

<!-- .slide: data-layout="tc-keys" -->

<span class="sheet-head"><span>§2 · OPERATION</span><span>讲台操作面</span></span>

# 键位

| 键 | 功能 |
|---|---|
| <span class="key">←</span> <span class="key">→</span> | 换页 |
| <span class="key">S</span> | 演讲者备注(跨窗口同步)|
| <span class="key">W</span> | 标注:画笔 / 荧光 / 划词 |
| <span class="key">ESC</span> | 缩略图总览 |

--

<!-- .slide: data-layout="tc-spec" -->

<span class="sheet-head"><span>§2 · OPERATION</span><span>讲台细节</span></span>

# 放映时能做什么

| 场景 | 动作 | 结果 |
|---|---|---|
| 投影接不上 | `?present=1` | 收起信息栏,全屏只留字 |
| 要留档 | 浏览器直接打印 | `?print-pdf` 得到一份矢量 PDF |
| 想引用某一页 | `?slide=3` | 服务端出图只画那一页 |
| 分享给别人 | 复制当前地址 | 对方看到的是同一份源 |

---

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§3 · PIPELINE</span><span>渲染管线</span></span>

# 一次请求的旅程

```draw/seq
n=browser;fe;Browser;;r0c0&n=gh;ext;GitHub raw;;r0c1&n=draw;be;draw;;r0c2&e=browser;gh;GET markdown&e=browser;draw;GET /draw&e=draw;browser;SVG;dash&title=Render pipeline&w=840
```

<span class="figcap"><b>FIG.1</b> — RENDER PIPELINE · 常见路径零服务端参与</span>

--

<!-- .slide: data-layout="tc-flow" -->

<span class="sheet-head"><span>§3 · PIPELINE</span><span>四道工序</span></span>

# 从链接到讲台

| STEP 01 | STEP 02 | STEP 03 | STEP 04 |
|---|---|---|---|
| <span class="fl-name">取源</span><span class="fl-note">issue / PR / raw 归一成一个 URL</span> | <span class="fl-name">切页</span><span class="fl-note">— 与 --- 分出主题与子页</span> | <span class="fl-name">展开图</span><span class="fl-note">draw 围栏换成内联矢量 SVG</span> | <span class="fl-name">渲染</span><span class="fl-note">讲台与封面图同源同版</span> |

--

<!-- .slide: data-layout="tc-rev" -->

<span class="sheet-head"><span>§3 · REVISION</span><span>修订记录</span></span>

# REV

- <span class="rev-id">REV C</span><span class="rev-date">2026-11-24</span><span class="rev-text"><code>look: blueprint</code> 落到九种语义页型,新增矩阵 / 流程 / 修订三张图纸</span>
- <span class="rev-id">REV B</span><span class="rev-date">2026-11-18</span><span class="rev-text">版式即海报:几何装饰由模板统一提供,deck 只写内容</span>
- <span class="rev-id">REV A</span><span class="rev-date">2026-11-11</span><span class="rev-text">首版 —— 链接即演示,封面图与讲台第一页永远一致</span>

---

<!-- .slide: data-layout="tc-keys" -->

<span class="sheet-head"><span>§4 · OPERATION</span><span>操作与约束</span></span>

# 讲台上的六个动作

| 键 | 功能 |
|---|---|
| <span class="key">←</span> <span class="key">→</span> | 换页(含纵向子页) |
| <span class="key">S</span> | 演讲者备注 |
| <span class="key">W</span> | 标注:画笔 / 荧光 / 划词 |
| <span class="key">ESC</span> | 缩略图总览 |
| <span class="key">F</span> | 全屏 |
| <span class="key">?</span> | 快捷键速查 |

--

<!-- .slide: data-layout="tc-notes" -->

<span class="sheet-head"><span>§4 · CONSTRAINTS</span><span>设计约束</span></span>

# NOTES

<span class="note"><span class="no">N-01</span>输入只能是 URL 或 markdown —— 不接受二进制附件</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-02</span>注释即停用;指令注释(`.slide` / `.element`)是语法</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-03</span>图表内联为矢量 SVG,缩放不糊</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-04</span>版式即海报:几何装饰由模板统一提供,deck 只写内容</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-05</span>deck 上限 512KB;内容直传的总 URL 约 6KB</span> <!-- .element: class="note fragment" -->

--

<!-- .slide: data-layout="tc-eof" -->

<span class="sheet-head"><span>END OF DOCUMENT</span><span>X-CMD/PPT</span></span>

<span class="endmark">EOF</span>

<span class="sub">SHEET 12/12 · 源文件在仓库里,链接永远指向最新版</span>

```draw
type=qr&d=https://x-cmd.com/ppt&fg=%230a1524&bg=%23ffffff&w=240&h=240
```
