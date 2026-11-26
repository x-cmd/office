---
title: 五分钟,学会写 deck
look: terminal
---

<!-- .slide: data-layout="t-status" -->

# 一 · 五分钟能写什么

你会 markdown —— 剩下的新东西只有三样:**分页**、**声明**、**备注**。这一份就是它们的速查表,照着写,五分钟能交一份 deck。

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | 分页 | --- 换章 · -- 换页 |
| <span class="ok">✓</span> | 声明 | frontmatter 写元数据 |
| <span class="ok">✓</span> | 备注 | Note: 只给自己看 |
| <span class="dim">·</span> | 标题列表表格代码 | 照常写,不用学 |

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

```text
$ x ppt quickstart --check
```

|  |  |  |
|---|---|---|
| --- | 另起一个系列,章与章之间 | 横向 |
| -- | 同一系列的下一页 | 纵向 |
| 空行 | 分隔符前后各留一行,不然会被当成 setext 下划线 | <span class="req">required</span> |
| 围栏内 | 代码块里的 --- 与 -- 是字面量,不分页 | 字面量 |

|  |  |  |
|---|---|---|
| <span class="warn">●</span> | 少了空行 | 讲台与封面图页数对不上 |

<span class="t-ref">分隔符前后各一个空行</span>

<span class="t-foot">usage 错误 → exit <span class="err">2</span></span>

--

<!-- .slide: data-layout="t-args" -->

# 版式表:页首一条注释换一页性格

版式写在页首的 `<!-- .slide: -->` 注释里,写什么这一页就长什么样。

```text
$ x ppt quickstart --layout t-status
```

|  |  |  |
|---|---|---|
| t-status | 作业表:一行一条状态,符号 + 名字 + 状态 + 耗时 | 一览 |
| t-log | 命令与输出:一段 ```text 终端回显 | 过程 |
| t-args | 参数表:名字 / 说明 / 默认值 三列对齐 | 规格 |
| t-tree | 文件树:目录、文件、右侧注解 | 结构 |
| t-env | 环境与版本:一行一个变量 | 环境 |
| t-exit | 收尾:退出码 + 一句结论 + 链接 | 结尾 |

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

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | look: terminal | 一行换掉整套长相 |
| <span class="ok">✓</span> | Note: | 演讲者备注,按 S 只给自己看 |
| <span class="dim">·</span> | 标题列表表格代码 | 照常写,不用学 |

<span class="t-ref">写在文件最前面</span>

<span class="t-foot">frontmatter 结束线之后才算正文</span>

--

<!-- .slide: data-layout="t-env" -->

# 头上的声明(frontmatter)

写不写都行,写了更像"一份作品"。

|  |  |  |
|---|---|---|
| <span class="dim">look</span> | terminal | 一整套美术方向 |
| <span class="dim">theme</span> | black | 配色,14 款内置 |
| <span class="dim">template</span> | deck | deck 左对齐 / center 居中 / plain 原样 |
| <span class="dim">palette</span> | — | 微调 CSS 变量,浏览器与封面图同步 |
| <span class="dim">cover</span> | — | 生成一页标准封面 |

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | deck 没写的键 | 用 look 自己的值 |

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

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | data-layout | 这一页用哪个版式 |
| <span class="dim">◷</span> | data-background-color | 逐页底色 |
| <span class="dim">◷</span> | data-title | 给版式留的一行副标 |

<span class="t-ref">逐页生效,两侧同源</span>

<span class="t-foot">$ x ppt check → <span class="ok">0 problems</span></span>

--

<!-- .slide: data-layout="t-tree" -->

# 页面骨架:一棵树

一份 deck 就是一棵文件树:frontmatter 是根,系列是目录,页是文件。

```text
▸ quickstart.md                    15 页 · 3 个系列
├── frontmatter       look: terminal        1 行
├── 一 · 五分钟能写什么        t-status        4 页
├── 二 · 写内容              t-log          5 页
└── 三 · 发布与排错            t-log          6 页
```

每个系列的第一页是钩子:标题 + 一句摘要;后面 2–4 页是详情

<span class="t-ref">系列 = --- 切出来的段</span>

<span class="t-foot">exit <span class="ok">0</span> · 3 个系列 / 15 页</span>

--

<!-- .slide: data-layout="t-log" -->

# 图表围栏:一行参数,一张图

围栏语言写 `draw`,参数写成查询串。服务端展开成内联 SVG —— 矢量、可点、跟着 deck 的配色走。下面这张就是本 deck 自己画的:

```draw
type=hbar&t=evil&labels=听懂,上手,讲完&values=100,95,5&w=560&h=200&title=五分钟的效果
```

|  |  |  |
|---|---|---|
| <span class="dim">◷</span> | type= | bar / line / pie / radar / gauge … |
| <span class="dim">◷</span> | draw/&lt;图种&gt; | 结构图:seq / erd / gitgraph / timeline … |
| <span class="dim">◷</span> | w= h= | 尺寸;不写用默认值 |

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

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | 本地先看一遍 | x ppt serve |
| <span class="ok">✓</span> | 写完自检 | node scripts/check-deck.mjs |
| <span class="warn">●</span> | 再贴出去 | 见下一页 |

<span class="t-ref">发布 · URL 参数 · 常见错</span>

<span class="t-foot">exit <span class="ok">0</span></span>

--

<!-- .slide: data-layout="t-args" -->

# 发布:三个住法,一行贴出去

deck 放在任何取得到 raw 的地方,然后给一条长链接。

```text
$ x ppt publish https://x-cmd.com/ppt?url=<deck 的地址>
```

|  |  |  |
|---|---|---|
| 仓库 | 放 GitHub / GitLab,给 raw 地址 | raw |
| 对象存储 | 任何能公开读的文件地址都行 | https |
| 本机 | 先 serve,自己看看够不够 | localhost |
| url | deck 的地址,唯一必填项 | <span class="req">required</span> |
| present | 讲台模式 | 1 |
| controls | 右下角控制条 | 1 |

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

|  |  |  |
|---|---|---|
| <span class="ok">✓</span> | cover.svg | 封面图,跟讲台同一套配色 |
| <span class="dim">◷</span> | 参数 | 与 ?url= 一样,url 必填 |
| <span class="dim">◷</span> | 空格 | 链接里的空格要 %20 编码 |

<span class="t-ref">封面图 = 第一页的静态版</span>

<span class="t-foot">$ curl -sI cover.svg → <span class="ok">200</span></span>

--

<!-- .slide: data-layout="t-stack" -->

# 常见错:页数对不上

最常踩的一个:分隔符前面少了空行 —— markdown 把它当成 setext 下划线,讲台切页,封面图不切。

```text
quickstart.md:18      ## 展开
quickstart.md:20      ---                 ← 被当成下划线
quickstart.md:21      # 二 · 收尾
```

> 分隔符前后各留一个空行 —— 少了它,**讲台与封面图页数对不上**。

<span class="t-ref">check-deck 第 5 项</span>

<span class="t-foot">exit <span class="err">1</span> · 1 problem</span>

--

<!-- .slide: data-layout="t-stack" -->

# 常见错:其余四条

```text
页型名写错          data-layout="t-stats"      ← 不在页型表里
没写 data-layout    回落成普通页                 ←
围栏没闭合          后面全是代码块                ←
url 取不到          返回 404,deck 是空的          ←
```

> 写完跑一遍 **node scripts/check-deck.mjs quickstart.md** —— 页数、系列切分、页型名、分隔符格式都查。

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
