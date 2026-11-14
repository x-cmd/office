---
template: deck
theme: black
cover:
  title: 把 markdown 变成一场演讲
  subtitle: 一个长链接,就是入口
  author: x-cmd
  date: 2026-11-14
---

<!-- .slide: data-layout="statement" -->

# 一个链接,就是一场演讲

**贴进 README,别人点开就能讲。**

---

# 旧剧本

<!-- .slide: data-layout="section" data-background-color="#101722" -->

## AI 十分钟写完 deck,然后呢

- 装工具、导 PDF、调样式 —— 每台机器重来一遍
- 发出去的是**文件**:打不开、看不了、改不动
- 三个月后,版本已经对不上了

--

> 分享出去的应该是**内容**,不是文件。

markdown 早就躺在仓库里了 —— 缺的只是一个**入口**。

---

# 新剧本:只贴地址

```text
https://x-cmd.com/ppt?url=<markdown 的地址>
```

渲染搬到**浏览器**,输入缩成**一个地址**。

内容不动、仓库不动、工具不用装。

--

## 内容直传也行

不想找托管?全文塞进参数:

```text
https://x-cmd.com/ppt?content=<URL 编码的 markdown>
```

一两个屏幕的短 deck,一条链接走天下。

---

# 封面,也是一张链接

[![本 deck 的封面](/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md)](?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md)

服务端把指定那一页排成 **SVG** —— 矢量、可缩放,README 里 `width="420"` 控制大小。

点图 → 直接开讲。

--

## README 里的标准嵌法

```markdown
[![](https://x-cmd.com/ppt/cover.svg?url=<deck 地址>)](https://x-cmd.com/ppt?url=<deck 地址>)
```

封面永远与第一页**同源同款** —— deck 改了,封面跟着变。

---

# 架构:浏览器直读

<!-- .slide: data-layout="section" data-background-color="#0f1a17" -->

## 常见路径零服务端调用

GitHub 的 raw 有 CORS 头 —— **浏览器直接取 markdown**,
worker 只出一个页面壳。

被 CORS 挡住才回落服务端代取:校验 Referer、限体积、限频率。

--

## 服务端只做一件难事

把**指定的那一页**排成 SVG:

- 画布 960×700,字号/行高/颜色取自主题 CSS
- 字体子集**内嵌**(`<img>` 里取不到外部字体)
- 测量的字,就是渲染的字

于是封面图和浏览器里那一页,看着一样。

---

# 讲台上有什么

| 键 | 能做什么 |
|---|---|
| `← → ↑ ↓` | 换主题 / 换主题内的页 |
| `S` | 演讲者备注(跨窗口同步) |
| `W` | **标注**:画笔 / 荧光笔 / 划词高亮 |
| `Z` / `Y` | 标注撤销 / 重做 |
| `ESC` | 缩略图总览 |

标注钉在**页**上,翻回来还在;观众屏只见内容,不见工具。

--

## 手机是另一套

竖屏画布、上下滑翻页、二维小地图 —— 不是"缩小的桌面版",
是照视频软件的用法重做的。

---

# 三份案例,点开就讲

- **五分钟** —— 写 deck 的语法速查
- **图表** —— draw 图表与真实数据
- **datalink** —— 数据在链接里(理念篇)

都在首页的 gallery 里,也都在你的收藏栏里。

---

<!-- .slide: data-layout="end" -->

# 现在就去讲一场

**https://x-cmd.com/ppt**
