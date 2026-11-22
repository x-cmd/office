---
template: deck
theme: league
cover:
  title: 五分钟,学会写 deck
  subtitle: 因为 markdown 你已经会了
  author: x-cmd
  date: 2026-11-23
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#414958 0%, #202329 78%)" -->

# 你已经会写 deck 了

**你会 markdown —— 剩下的新东西,五分钟讲完。**

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#3d4657 0%, #20242c 75%)" -->

# 新东西只有三样

## 分页 · 声明 · 备注

- `---` —— 换一章(左右方向键) <!-- .element: class="fragment" -->
- `--` —— 章内换一页(上下方向键) <!-- .element: class="fragment" -->
- `Note:` —— 演讲者备注,按 `S` 只给自己看 <!-- .element: class="fragment" -->

标题、列表、表格、代码、链接 —— 照常写,不用学。

--

## 骨架长这样

```markdown
# 一 · 开场        ← 一章

## 破题            ← 章内一页

--

## 展开

---

# 二 · 收尾
```

---

<!-- .slide: data-layout="section" data-background-color="#2c3444" -->

# 头上的声明(frontmatter)

写不写都行,写了更像"一份作品":

| 键 | 作用 |
|---|---|
| `cover:` | 生成一页标准封面(title / subtitle / author / date) |
| `theme:` | 配色,14 款内置(本页是 league) |
| `template:` | `deck` 左对齐 / `center` 居中 / `plain` 原样 |
| `palette:` | 微调 CSS 变量,浏览器与封面图同步 |

--

## 每页还能换底色

```markdown
<!-- .slide: data-background-gradient="radial-gradient(#3d4657, #20242c)" -->
```

`data-background-color` / `data-background-gradient` 逐页生效,
浏览器与 cover.svg 两侧同源。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#3d4657 0%, #20242c 75%)" -->

# 每页一个性格

页首一条注释,版式就换:

| 版式 | 用在 |
|---|---|
| `section` | 章节分隔(居中、可配底色) |
| `statement` | 一句话砸场 |
| `quote` | 引用 |
| `end` | 收尾 |
| `gallery` | 封面卡片墙(见首页) |

本 deck 里那些深色大页,就是 `section` 配渐变底色。

--

## 内容逐步出现

列表项后缀一条注释,讲台上逐条浮现:

```markdown
- 第一条 <!-- .element: class="fragment" -->
- 第二条 <!-- .element: class="fragment" -->
```

封面图里它们一次全显 —— 两侧都不丢字。

---

<!-- .slide: data-layout="section" data-background-color="#2c3444" -->

# 图表,一行参数

围栏语言写 `draw`:

```draw
type=bar&t=evil&labels=听懂,上手,讲完&values=100,95,5&w=680&h=340&title=五分钟的效果
```

服务端展开成内联 SVG —— 矢量、可点,玩法见「图表」那份 deck。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#3d4657 0%, #20242c 75%)" -->

# 发布:贴出去就行

deck 放在任何取得到 raw 的地方,然后:

```text
https://x-cmd.com/ppt?url=<deck 的地址>
```

想嵌 README,再加一行封面 —— 点图开讲:

```markdown
[![封面](https://x-cmd.com/ppt/cover.svg?url=<deck 地址>)]
(https://x-cmd.com/ppt?url=<deck 地址>)
```

---

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#414958 0%, #202329 78%)" -->

# 五分钟到了

**去写第一页:`# 我的演讲`**
