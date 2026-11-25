---
look: report
---

<!-- .slide: data-layout="rep-verdict" class="rep-ok" -->

<span class="rep-status">PASS</span>

# 海报系统上线 —— 三种美术方向,deck 只写内容

这一轮把「版式即海报」从**内置版式**扩到任意 deck 自己写的版式:海报工具箱
(几何装饰 / ghost 巨字 / 注记栏 / 12 栏网格)与图表配色桥接都进了模板层。
三份旗舰 deck(发布会数字风 / 杂志编辑风 / 蓝图工程风)已上线,讲台与封面图同源。

<span class="rep-ref">#41 · feat/design-system</span>

<span class="rep-foot">feat/design-system · 2026-11-25 · 12 files · +742 −96</span>

---

<!-- .slide: data-layout="rep-evidence" -->

# 233<span class="unit">tests</span>

全绿;新增 6 条回归(角标剥离 / 块标量 / 断行 / 表外边距 / 图表配色)。

<span class="rep-ref">CI run 99812</span>

```draw
type=bar&labels=前,后&series=通过:226,233&w=720&h=300
```

<span class="rep-foot">vitest · 233 passed / 0 failed · 4.3s</span>

---

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

---

<!-- .slide: data-layout="rep-verify" -->

# 自己跑一遍

```text
$ npm test
$ npm run serve
$ node scripts/shoot.mjs talk.md --out /tmp/shots
```

逐页截图走查已入库(`npm run shoot`):去分步、绕缓存,只看最终版面。

<span class="rep-ref">scripts/shoot.mjs</span>

<span class="rep-foot">本地 8787 · 无需外网 · Chrome headless</span>

---

<!-- .slide: data-layout="rep-risk" -->

# 已知边界

- 服务端出图**看不见 deck 自带的 `style:`** —— 配色已搬进 `palette:`,但版式仍各写各的
- `look` 目前只有一套(report);其余三套气质还是手写 CSS,没收成 look
- 渐变标题在小尺寸下仍发虚(issue #9 的第三条根因,未解)

<span class="rep-ref">issue #9</span>

<span class="rep-foot">三项都不影响本轮交付 · 下轮跟进</span>

---

<!-- .slide: data-layout="rep-outro" -->

# 合并前请看这两处

<div class="rep-links">
<a href="https://github.com/x-cmd/ppt/pull/41">PR #41</a>
<a href="https://github.com/x-cmd/office/issues/1">demo issue</a>
<a href="https://x-cmd.com/ppt">线上</a>
</div>

<span class="rep-foot">x-cmd/ppt · x-cmd/office</span>
