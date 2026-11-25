---
look: terminal
---

<!-- .slide: data-layout="t-status" -->

# 三个作业,两个绿

<div class="row"><span class="ok">✓</span><span class="k">build</span><span class="v">passed</span><span class="n">1m 12s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">test</span><span class="v">passed</span><span class="n">4m 03s</span></div>
<div class="row"><span class="ok">✓</span><span class="k">lint</span><span class="v">passed</span><span class="n">0m 21s</span></div>
<div class="row"><span class="warn">●</span><span class="k">release</span><span class="v">pending</span><span class="n">—</span></div>

<span class="t-ref">run 99812 · 2026-11-25 03:12</span>

<span class="t-foot">$ echo $? → <span class="ok">0</span></span>

---

<!-- .slide: data-layout="t-log" -->

# 竞态的现场

```text
$ npm test -- race
  ✓ 40 passing
  ✗ 12 failing   lost frame
```

十二个用例挂在同一处:读-改-写没有串行化。
日志里那行 `lost frame` 就是全部线索。

<span class="t-ref">test/race.test.ts</span>

<span class="t-foot">exit <span class="err">1</span> · 3 retries</span>

---

<!-- .slide: data-layout="t-diff" -->

# 改了 9 个文件

<div class="row"><span class="dim">M</span><span class="k">src/core/queue.ts</span><span class="v">+120 −12</span></div>
<div class="row"><span class="dim">M</span><span class="k">src/core/frame.ts</span><span class="v">+64 −18</span></div>
<div class="row"><span class="dim">A</span><span class="k">test/race.test.ts</span><span class="v">+88 −0</span></div>
<div class="row"><span class="dim">M</span><span class="k">src/core/worker.ts</span><span class="v">+31 −7</span></div>

<span class="t-ref">9 files changed, 303 insertions(+), 37 deletions(−)</span>

<span class="t-foot">branch fix/race · base main · 3 commits</span>

---

<!-- .slide: data-layout="t-env" -->

# 环境

<div class="row"><span class="dim">node</span><span class="k">v22.21.1</span><span class="v">darwin-arm64</span></div>
<div class="row"><span class="dim">worker</span><span class="k">wrangler 4.155</span><span class="v">compat 2026-09-01</span></div>
<div class="row"><span class="dim">base</span><span class="k">x-cmd.com/ppt</span><span class="v">d776129c</span></div>
<div class="row"><span class="dim">deps</span><span class="k">reveal 6.0.2</span><span class="v">marked 16.4.1</span></div>

<span class="t-ref">env · 无外网 · 无代理</span>

<span class="t-foot">$ x-cmd doctor → <span class="ok">all green</span></span>

---

<!-- .slide: data-layout="t-exit" -->

<span class="code">exit 0</span>

# 合并前看这两处

<div class="links">
<a href="https://github.com/x-cmd/ppt/pull/41">PR #41</a>
<a href="https://github.com/x-cmd/office/issues/1">issue #1</a>
<a href="https://x-cmd.com/ppt">线上</a>
</div>

<span class="t-ref">x-cmd/ppt · x-cmd/office</span>

<span class="t-foot">look: terminal · agent 的工作痕迹</span>
