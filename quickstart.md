---
template: deck
theme: league
cover:
  title: 五分钟
  subtitle: 写一场演讲要多久
  author: x-cmd
  date: 2026-11-14
---

<!-- .slide: data-layout="title" -->

# 五分钟

一份 markdown,一场演讲。

**你只需要记住三件事:`#` 是主题,`---` 翻页,剩下全是 markdown。**

---

# 骨架

<!-- .slide: data-layout="section" data-background-color="#1c2430" -->

## 两级标题,两级页面

```markdown
# 一 · 原理          ← 主题(左右翻)

## 开场              ← 主题内的一页(上下翻)

--
                   ← 主题内换页

---

# 二 · 用法          ← 换主题
```

--

## 头上的 frontmatter

```yaml
---
template: deck        # deck(默认)/ center / plain
theme: black          # 14 款内置
cover:                # 写了就生成一页标准封面
  title: 我的演讲
  subtitle: 一句话说明
  author: 我
  date: 2026-11-14
---
```

都有合理默认,只写要用的。

---

# 排版就是 markdown

| 写法 | 效果 |
|---|---|
| `**粗**` | **粗体** |
| `*斜*` | *斜体* |
| `` `代码` `` | 行内代码 |
| `[文字](链接)` | 链接 |
| `> 引用` | 引用块 |
| `- 项` / `1. 项` | 列表 |

表格、代码块、图片照常写 —— 渲染交给 reveal.js。

--

## 图片

```markdown
![说明](https://example.com/a.png)
```

浏览器里正常显示;封面图(SVG)里画占位框 —— 配图建议用
draw 链接或内联 SVG,两侧都是矢量。

---

# 版式:一页一个性格

每页开头放一条注释,版式就换:

```markdown
<!-- .slide: data-layout="section" data-background-color="#101722" -->
```

| 版式 | 用在 |
|---|---|
| `title` / `cover` | 开场 |
| `section` | 章节分隔(配背景色) |
| `statement` | 一句话砸场 |
| `quote` | 引用 |
| `end` | 收尾 |
| `gallery` | 封面卡片墙(见首页) |

--

## 演讲者备注

```markdown
## 这一页

正文。

Note:
只有你自己能看到的话,写在 S 键打开的备注窗口里。
```

代码块里的 `---` / `--` / `Note:` 不会被当分页 —— 放心写示例。

---

# 发布:贴出去就行

deck 放在任何取得到 raw 的地方(git / gist / 静态托管):

```text
https://x-cmd.com/ppt?url=<deck 的地址>
```

URL 参数可以盖过 deck 声明:`?theme=league`、`?template=center`。

--

## 顺手做张封面

```markdown
[![封面](https://x-cmd.com/ppt/cover.svg?url=<deck 地址>)](https://x-cmd.com/ppt?url=<deck 地址>)
```

嵌进 README —— 封面与第一页永远同源同款,点图开讲。

---

<!-- .slide: data-layout="end" -->

# 五分钟到了

**去写第一页:`# 我的演讲`**
