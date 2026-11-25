---
title: 五分钟,学会写 deck
look: terminal
---

<!-- .slide: data-layout="t-status" -->

# 一 · 五分钟能写什么

你会 markdown —— 剩下的新东西只有三样:**分页**、**声明**、**备注**。这一份就是它们的速查表,照着写,五分钟能交一份 deck。

<div class="row"><span class="ok">✓</span><span class="k">分页</span><span class="v">--- 换章 · -- 换页</span></div>
<div class="row"><span class="ok">✓</span><span class="k">声明</span><span class="v">frontmatter 写元数据</span></div>
<div class="row"><span class="ok">✓</span><span class="k">备注</span><span class="v">Note: 只给自己看</span></div>
<div class="row"><span class="dim">·</span><span class="k">标题列表表格代码</span><span class="v">照常写,不用学</span></div>

<span class="t-ref">quickstart · v1 · 2026-11-25</span>

<span class="t-foot">look: terminal · 共 3 章 15 页</span>

--

<!-- .slide: data-layout="t-log" -->

# 分页:两种分隔符,两种方向

`---` 横向分页是**另起一个系列**(左右方向键);`--` 纵向分页是**同一系列的下一页**(上下方向键)。

```text
# 一 · 开场        ← --- 另起一个系列

## 破题            ← -- 同系列的下一页

--

## 展开

---

# 二 · 收尾
```

<span class="t-ref">键盘:← → 换系列 · ↑ ↓ 换页 · ESC 缩略图 · S 备注</span>

<span class="t-foot">分隔符单独占一行,前后各留一个空行</span>

--

<!-- .slide: data-layout="t-args" -->

# 分页的规矩:三句话

写多了会踩的坑,基本就这三条。

<div class="usage"><span class="p">$</span> x ppt quickstart <span class="q">--check</span></div>

<div class="arg"><span class="k">---</span><span class="v">另起一个系列,章与章之间</span><span class="n">横向</span></div>
<div class="arg"><span class="k">--</span><span class="v">同一系列的下一页</span><span class="n">纵向</span></div>
<div class="arg"><span class="k">空行</span><span class="v">分隔符前后各留一行,不然会被当成 setext 下划线</span><span class="n req">required</span></div>
<div class="arg"><span class="k">围栏内</span><span class="v">代码块里的 --- 与 -- 是字面量,不分页</span><span class="n">字面量</span></div>

<div class="row"><span class="warn">●</span><span class="k">少了空行</span><span class="v">讲台与封面图页数对不上</span></div>

<span class="t-ref">分隔符前后各一个空行</span>

<span class="t-foot">usage 错误 → exit <span class="err">2</span></span>

--

<!-- .slide: data-layout="t-args" -->

# 版式表:页首一条注释换一页性格

版式写在页首的 `<!-- .slide: -->` 注释里,写什么这一页就长什么样。

<div class="usage"><span class="p">$</span> x ppt quickstart <span class="q">--layout t-status</span></div>

<div class="arg"><span class="k">t-status</span><span class="v">作业表:一行一条状态,符号 + 名字 + 状态 + 耗时</span><span class="n">一览</span></div>
<div class="arg"><span class="k">t-log</span><span class="v">命令与输出:一段 ```text 终端回显</span><span class="n">过程</span></div>
<div class="arg"><span class="k">t-args</span><span class="v">参数表:名字 / 说明 / 默认值 三列对齐</span><span class="n">规格</span></div>
<div class="arg"><span class="k">t-tree</span><span class="v">文件树:目录、文件、右侧注解</span><span class="n">结构</span></div>
<div class="arg"><span class="k">t-env</span><span class="v">环境与版本:一行一个变量</span><span class="n">环境</span></div>
<div class="arg"><span class="k">t-exit</span><span class="v">收尾:退出码 + 一句结论 + 链接</span><span class="n">结尾</span></div>

<span class="t-ref">looks/terminal.json · 页型表</span>

<span class="t-foot">这一份 deck 全用的这一套版式</span>

---

<!-- .slide: data-layout="t-log" -->

# 二 · 写内容

新东西只有三样,剩下的照常 markdown 写。这一章讲的是那三样怎么落到文件里。

```text
---
look: terminal          ← 一行换掉整套长相
---

<!-- .slide: data-layout="t-log" -->
# 标题
正文照常写:列表、表格、代码、链接都认。
```

<div class="row"><span class="ok">✓</span><span class="k">look: terminal</span><span class="v">一行换掉整套长相</span></div>
<div class="row"><span class="ok">✓</span><span class="k">Note:</span><span class="v">演讲者备注,按 S 只给自己看</span></div>
<div class="row"><span class="dim">·</span><span class="k">标题列表表格代码</span><span class="v">照常写,不用学</span></div>

<span class="t-ref">写在文件最前面</span>

<span class="t-foot">frontmatter 结束线之后才算正文</span>

--

<!-- .slide: data-layout="t-env" -->

# 头上的声明(frontmatter)

写不写都行,写了更像"一份作品"。

<div class="row"><span class="dim">look</span><span class="k">terminal</span><span class="v">一整套美术方向</span></div>
<div class="row"><span class="dim">theme</span><span class="k">black</span><span class="v">配色,14 款内置</span></div>
<div class="row"><span class="dim">template</span><span class="k">deck</span><span class="v">deck 左对齐 / center 居中 / plain 原样</span></div>
<div class="row"><span class="dim">palette</span><span class="k">—</span><span class="v">微调 CSS 变量,浏览器与封面图同步</span></div>
<div class="row"><span class="dim">cover</span><span class="k">—</span><span class="v">生成一页标准封面</span></div>

<div class="row"><span class="ok">✓</span><span class="k">deck 没写的键</span><span class="v">用 look 自己的值</span></div>

<span class="t-ref">look 优先 · deck 覆盖</span>

<span class="t-foot">$ x ppt doctor → <span class="ok">all green</span></span>

--

<!-- .slide: data-layout="t-log" -->

# 指令注释:页首一行换一页

页首一条 `<!-- .slide: -->` 注释,这一页的版式就定了。注释里的 `data-layout` 是页型,其余是逐页属性。

```text
<!-- .slide: data-layout="t-log" -->
# 标题
正文照常写。
```

<div class="row"><span class="ok">✓</span><span class="k">data-layout</span><span class="v">这一页用哪个版式</span></div>
<div class="row"><span class="dim">◷</span><span class="k">data-background-color</span><span class="v">逐页底色</span></div>
<div class="row"><span class="dim">◷</span><span class="k">data-title</span><span class="v">给版式留的一行副标</span></div>

<span class="t-ref">逐页生效,两侧同源</span>

<span class="t-foot">$ x ppt check → <span class="ok">0 problems</span></span>

--

<!-- .slide: data-layout="t-tree" -->

# 页面骨架:一棵树

一份 deck 就是一棵文件树:frontmatter 是根,系列是目录,页是文件。

<div class="tree">
<div class="line"><span class="b">▸</span><span class="d">quickstart.md</span><span class="m">15 页 · 3 个系列</span></div>
<div class="line"><span class="b">├──</span><span class="d">frontmatter</span><span class="f">look: terminal</span><span class="m">1 行</span></div>
<div class="line"><span class="b">├──</span><span class="d">一 · 五分钟能写什么</span><span class="f">t-status</span><span class="m">4 页</span></div>
<div class="line"><span class="b">├──</span><span class="d">二 · 写内容</span><span class="f">t-log</span><span class="m">5 页</span></div>
<div class="line"><span class="b">└──</span><span class="d">三 · 发布与排错</span><span class="f">t-log</span><span class="m">6 页</span></div>
</div>

<p class="tree-sum">每个系列的第一页是钩子:标题 + 一句摘要;后面 2–4 页是详情</p>

<span class="t-ref">系列 = --- 切出来的段</span>

<span class="t-foot">exit <span class="ok">0</span> · 3 个系列 / 15 页</span>

--

<!-- .slide: data-layout="t-log" -->

# 图表围栏:一行参数,一张图

围栏语言写 `draw`,参数写成查询串。服务端展开成内联 SVG —— 矢量、可点、跟着 deck 的配色走。下面这张就是本 deck 自己画的:

```draw
type=hbar&t=evil&labels=听懂,上手,讲完&values=100,95,5&w=560&h=200&title=五分钟的效果
```

<div class="row"><span class="dim">◷</span><span class="k">type=</span><span class="v">bar / line / pie / radar / gauge …</span></div>
<div class="row"><span class="dim">◷</span><span class="k">draw/&lt;图种&gt;</span><span class="v">结构图:seq / erd / gitgraph / timeline …</span></div>
<div class="row"><span class="dim">◷</span><span class="k">w= h=</span><span class="v">尺寸;不写用默认值</span></div>

<span class="t-ref">玩法见「图表」那份 deck</span>

<span class="t-foot">SVG 内联 · 封面图里也在</span>

---

<!-- .slide: data-layout="t-log" -->

# 三 · 发布与排错

写完往哪儿放、怎么贴出去、出错了怎么办 —— 这一章三件事各一页。

```text
$ git push origin main
$ x ppt serve ./quickstart.md
ppt serving at http://localhost:8787/ppt

$ curl -sI "http://localhost:8787/ppt?url=…"
HTTP/1.1 200 OK
```

<div class="row"><span class="ok">✓</span><span class="k">本地先看一遍</span><span class="v">x ppt serve</span></div>
<div class="row"><span class="ok">✓</span><span class="k">写完自检</span><span class="v">node scripts/check-deck.mjs</span></div>
<div class="row"><span class="warn">●</span><span class="k">再贴出去</span><span class="v">见下一页</span></div>

<span class="t-ref">发布 · URL 参数 · 常见错</span>

<span class="t-foot">exit <span class="ok">0</span></span>

--

<!-- .slide: data-layout="t-args" -->

# 发布:三个住法,一行贴出去

deck 放在任何取得到 raw 的地方,然后给一条长链接。

<div class="usage"><span class="p">$</span> x ppt publish <span class="q">https://x-cmd.com/ppt?url=&lt;deck 的地址&gt;</span></div>

<div class="arg"><span class="k">仓库</span><span class="v">放 GitHub / GitLab,给 raw 地址</span><span class="n">raw</span></div>
<div class="arg"><span class="k">对象存储</span><span class="v">任何能公开读的文件地址都行</span><span class="n">https</span></div>
<div class="arg"><span class="k">本机</span><span class="v">先 serve,自己看看够不够</span><span class="n">localhost</span></div>
<div class="arg"><span class="k">url</span><span class="v">deck 的地址,唯一必填项</span><span class="n req">required</span></div>
<div class="arg"><span class="k">present</span><span class="v">讲台模式</span><span class="n">1</span></div>
<div class="arg"><span class="k">controls</span><span class="v">右下角控制条</span><span class="n">1</span></div>

<span class="t-ref">x-cmd.com/ppt?url=…</span>

<span class="t-foot">参数写错 → exit <span class="err">2</span></span>

--

<!-- .slide: data-layout="t-log" -->

# 嵌进 README:加一行封面

想嵌 README,再加一行封面图 —— 点图开讲。

````text
```markdown
[![封面](https://x-cmd.com/ppt/cover.svg?url=<deck 地址>)]
(https://x-cmd.com/ppt?url=<deck 地址>)
```
````

<div class="row"><span class="ok">✓</span><span class="k">cover.svg</span><span class="v">封面图,跟讲台同一套配色</span></div>
<div class="row"><span class="dim">◷</span><span class="k">参数</span><span class="v">与 ?url= 一样,url 必填</span></div>
<div class="row"><span class="dim">◷</span><span class="k">空格</span><span class="v">链接里的空格要 %20 编码</span></div>

<span class="t-ref">封面图 = 第一页的静态版</span>

<span class="t-foot">$ curl -sI cover.svg → <span class="ok">200</span></span>

--

<!-- .slide: data-layout="t-stack" -->

# 常见错:页数对不上

最常踩的一个:分隔符前面少了空行 —— markdown 把它当成 setext 下划线,讲台切页,封面图不切。

<div class="stack">
<div class="frame"><span class="n">quickstart.md:18</span><span class="m">## 展开</span></div>
<div class="frame err"><span class="n">quickstart.md:20</span><span class="m">---</span><span class="at">← 被当成下划线</span></div>
<div class="frame"><span class="n">quickstart.md:21</span><span class="m"># 二 · 收尾</span></div>
</div>

<p class="why">分隔符前后各留一个空行 —— 少了它,<b>讲台与封面图页数对不上</b>。</p>

<span class="t-ref">check-deck 第 5 项</span>

<span class="t-foot">exit <span class="err">1</span> · 1 problem</span>

--

<!-- .slide: data-layout="t-stack" -->

# 常见错:其余四条

<div class="stack">
<div class="frame"><span class="n">页型名写错</span><span class="m">data-layout="t-stats"</span><span class="at">← 不在页型表里</span></div>
<div class="frame"><span class="n">没写 data-layout</span><span class="m">回落成普通页</span><span class="at">←</span></div>
<div class="frame"><span class="n">围栏没闭合</span><span class="m">后面全是代码块</span><span class="at">←</span></div>
<div class="frame"><span class="n">url 取不到</span><span class="m">返回 404,deck 是空的</span><span class="at">←</span></div>
</div>

<p class="why">写完跑一遍 <b>node scripts/check-deck.mjs quickstart.md</b> —— 页数、系列切分、页型名、分隔符格式都查。</p>

<span class="t-ref">四个最常撞的</span>

<span class="t-foot">$ node scripts/check-deck.mjs → <span class="ok">✓</span></span>

--

<!-- .slide: data-layout="t-exit" -->

<span class="code">exit 0</span>

# 五分钟到了:去写第一页

从 `look: terminal` 一行开始,剩下的照常 markdown 写。标题、列表、表格、代码、链接 —— 你已经会了。

<div class="links">
<a href="https://x-cmd.com/ppt">线上讲台</a>
<a href="https://x-cmd.com/ppt/cover.svg">封面图</a>
<a href="https://github.com/x-cmd/office">deck 仓库</a>
</div>

<span class="t-ref">quickstart · look: terminal</span>

<span class="t-foot">$ echo '# 我的演讲' → <span class="ok">第一页</span></span>
