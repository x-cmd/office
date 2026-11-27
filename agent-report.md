---
title: agent 的工作汇报
look: report
poster:
  title: 这一轮 ppt 做了什么
  subtitle: 版式即海报 —— 从内置版式扩到任意 deck
  tag: AGENT REPORT
  date: 2026-11-25
---

<!-- .slide: data-layout="rep-verdict" class="rep-ok" -->

<span class="rep-status">PASS</span>

# 这一轮 ppt 做了什么

把「版式即海报」从**内置版式**扩到任意 deck 自己写的版式:海报工具箱
(几何装饰 / ghost 巨字 / 注记栏 / 12 栏网格)与图表配色桥接都进了模板层。
三份旗舰 deck 已上线,讲台与封面图同源 —— 这一段讲**交付了什么**。

<span class="rep-ref">#41 · feat/design-system</span>

<span class="rep-foot">feat/design-system · 2026-11-25 · 12 files · +742 −96</span>

--

<!-- .slide: data-layout="rep-evidence" -->

# 233<span class="unit">tests</span>

全绿;新增 9 条回归(角标剥离 / 块标量 / 断行 / 表外边距 / 图表配色 / 页型回退)。

<span class="rep-ref">CI run 99812</span>

```draw
type=bar&labels=上一轮,这一轮&series=通过:224,233&w=720&h=300
```

<span class="rep-foot">vitest · 233 passed / 0 failed · 4.3s</span>

--

<!-- .slide: data-layout="rep-change" -->

# 改了 12 个文件

```
src/charts.ts               +23   −4
src/render/layouts.ts       +28   −6
src/render/look-data.ts     +64   −0
src/webapp.ts               +71  −12
templates/deck.css         +305   −0
looks/report.css           +241   −0
```

<span class="rep-ref">+742 −96</span>

<span class="rep-foot">6 commits · 2 repos · ppt + office</span>

--

<!-- .slide: data-layout="rep-change" -->

# 一半的改动是「搬」

```
templates/deck.css       ← poster.css + swiss.css + terminal.css
looks/report.css         ← 新 look(配色 + 9 个语义页型)
src/render/look-data.ts  ← gen-looks.mjs 生成,勿手改
```

搬出来的 CSS 一行没改 —— 原来的 look 与新的 look 长得一样,
只是从「写死的模板」变成「可声明的一套方向」。

<span class="rep-ref">3 commits: refactor: extract</span>

<span class="rep-foot">refs/heads/feat/design-system · 3 of 6 commits</span>

---

<!-- .slide: data-layout="rep-verify" -->

# 怎么自己跑一遍

```text
$ npm test
$ npm run serve
$ node scripts/shoot.mjs talk.md --out /tmp/shots
```

逐页截图走查已入库(`npm run shoot`):去分步、绕缓存,只看最终版面。

<span class="rep-ref">scripts/shoot.mjs</span>

<span class="rep-foot">本地 8787 · 无需外网 · Chrome headless</span>

--

<!-- .slide: data-layout="rep-evidence" -->

# 13<span class="unit">页</span>

新 deck `agent-report.md` 一次跑通:4 个系列 × 13 页,页眉 / 页脚 / 状态色全部对齐。

<span class="rep-ref">agent-report.md</span>

```draw
type=bar&labels=交付,验证,边界,下一步&series=页数:4,3,3,3&w=720&h=300
```

<span class="rep-foot">shoot.mjs · 13 shots · 0 layout warnings</span>

--

<!-- .slide: data-layout="rep-timeline" -->

# 这一轮的时间线

<div class="rep-timeline">
<div class="rep-tl-item rep-ok"><span class="rep-tl-time">11-24 09:12</span><span class="rep-tl-text">抽出海报工具箱,四个几何装饰收进 <code>ppt-decor--*</code></span></div>
<div class="rep-tl-item rep-ok"><span class="rep-tl-time">11-24 14:40</span><span class="rep-tl-text">图表配色桥接:deck 的 <code>palette:</code> 覆盖模板配色</span></div>
<div class="rep-tl-item rep-ok"><span class="rep-tl-time">11-24 19:05</span><span class="rep-tl-text">look 机制成型:<code>looks/*.css</code> + <code>looks/*.json</code> 两文件</span></div>
<div class="rep-tl-item rep-warn"><span class="rep-tl-time">11-25 02:33</span><span class="rep-tl-text">report look 第一版 —— 6 个页型,配色与几何抽出</span></div>
<div class="rep-tl-item rep-ok"><span class="rep-tl-time">11-25 08:15</span><span class="rep-tl-text">三份旗舰 deck 上线,讲台与封面图同源</span></div>
</div>

<span class="rep-ref">5 个工作日</span>

<span class="rep-foot">commits 6 · 2026-11-24 ~ 2026-11-25</span>

---

<!-- .slide: data-layout="rep-risk" -->

# 已知边界

- 服务端出图**看不见 deck 自带的 `style:`** —— 配色已搬进 `palette:`,但版式仍各写各的
- `look` 目前只有一套(report);其余三套气质还是手写 CSS,没收成 look
- 渐变标题在小尺寸下仍发虚(issue #9 的第三条根因,未解)

<span class="rep-ref">issue #9</span>

<span class="rep-foot">三项都不影响本轮交付 · 下轮跟进</span>

--

<!-- .slide: data-layout="rep-matrix" -->

# 影响面:两种用法

<div class="rep-matrix">
<div class="rep-mx-col">
<p class="rep-mx-h">改之前<span class="rep-mx-tag">手写</span></p>
<p class="rep-mx-row"><span class="rep-mx-k">配色</span>每个 deck 各写一份 <code>palette:</code></p>
<p class="rep-mx-row"><span class="rep-mx-k">版式</span>只能挑内置版式,不够用就手改 CSS</p>
<p class="rep-mx-row"><span class="rep-mx-k">成本</span>一个 deck ≈ 200 行 CSS</p>
</div>
<div class="rep-mx-col">
<p class="rep-mx-h">改之后<span class="rep-mx-tag rep-ok">声明</span></p>
<p class="rep-mx-row"><span class="rep-mx-k">配色</span>集中在 <code>looks/*.css</code> 的 <code>:root</code></p>
<p class="rep-mx-row"><span class="rep-mx-k">版式</span>deck 自带页型,写在 <code>data-layout</code> 上</p>
<p class="rep-mx-row"><span class="rep-mx-k">成本</span>一个 deck ≈ 1 行 <code>look:</code></p>
</div>
</div>

<span class="rep-ref">两份对照 · office/agent-report.md</span>

<span class="rep-foot">3 个仓库共用一套语义页型</span>

--

<!-- .slide: data-layout="rep-quote" -->

# 一个具体的反例

<div class="rep-quote rep-warn">
<p class="rep-q-text">「我写了 <code>look: report</code>,封面图还是老样子 —— 深色底、蓝渐变标题。」</p>
<p class="rep-q-src">来自 <code>office/insight.md</code> 的评论 · 2026-11-25 03:02</p>
</div>

根因:封面走服务端出图,服务端只认 <code>:root</code> 里的 <code>--r-*</code>;
那套 deck 的配色写在 <code>style:</code> 里,服务端抽不到。

<span class="rep-ref">issue #12 · 已复现</span>

<span class="rep-foot">修法:配色搬进 look 的 :root · 已在本轮做掉</span>

---

<!-- .slide: data-layout="rep-outro" -->

# 下一步做什么

- 把 `editorial` / `swiss` / `blueprint` 三套收成 look(各 ~1 天,机械活)
- 服务端出图支持 deck 自带页型(需要 SSR 侧认识 `rep-*` 这套 div 结构)
- issue #9 的第三条根因:小尺寸渐变字改用纯色 + 细描边

<span class="rep-ref">3 items · 2.5 人天</span>

<span class="rep-foot">排期在下个迭代 · owner: @lijunhao</span>

--

<!-- .slide: data-layout="rep-timeline" -->

# 后续计划

<div class="rep-timeline">
<div class="rep-tl-item rep-ok"><span class="rep-tl-time">W1 D1</span><span class="rep-tl-text">收 <code>swiss</code> 与 <code>blueprint</code> 两套 look</span></div>
<div class="rep-tl-item rep-warn"><span class="rep-tl-time">W1 D3</span><span class="rep-tl-text">SSR 侧认识语义页型 —— 先做 <code>rep-matrix</code> 一个试水</span></div>
<div class="rep-tl-item"><span class="rep-tl-time">W2 D1</span><span class="rep-tl-text">小尺寸渐变字改纯色,issue #9 收尾</span></div>
<div class="rep-tl-item"><span class="rep-tl-time">W2 D4</span><span class="rep-tl-text">发 <code>look</code> 的文档页:怎么写一套自己的方向</span></div>
</div>

<span class="rep-ref">2026-12-01 起</span>

<span class="rep-foot">4 项 · 无依赖 · 可并行</span>

--

<!-- .slide: data-layout="rep-outro" -->

# 合并前请看这两处

<div class="rep-links">
<a href="https://github.com/x-cmd/ppt/pull/41">PR #41</a>
<a href="https://github.com/x-cmd/ppt/issues/12">issue #12</a>
<a href="https://x-cmd.com/ppt">线上</a>
</div>

<span class="rep-foot">x-cmd/ppt · x-cmd/office · 2026-11-25</span>
