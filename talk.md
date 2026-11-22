---
template: deck
theme: black
cover:
  title: 把 markdown 变成一场演讲
  subtitle: 一个长链接,就是入口
  author: x-cmd
  date: 2026-11-23
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#1c2a4a 0%, #0d1117 78%)" -->

# 一个链接,就是一场演讲

**贴进 README,别人点开就能讲。**

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 旧剧本

## AI 十分钟写完 deck,然后呢

- 装工具、导 PDF、调样式 —— 每台机器重来一遍 <!-- .element: class="fragment" -->
- 发出去的是**文件**:打不开、看不了、改不动 <!-- .element: class="fragment" -->
- 三个月后,版本已经对不上了 <!-- .element: class="fragment" -->

--

<!-- .slide: data-layout="quote" data-background-color="#101726" -->

> 分享出去的应该是**内容**,不是文件。

markdown 早就躺在仓库里了 —— 缺的只是一个**入口**。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 新剧本:只贴地址

```text
https://x-cmd.com/ppt?url=<markdown 的地址>
```

渲染搬到**浏览器**,输入缩成一个地址:

- **内容不动** <!-- .element: class="fragment" -->
- **仓库不动** <!-- .element: class="fragment" -->
- **工具不用装** <!-- .element: class="fragment" -->

--

## 内容直传也行

不想找托管?全文塞进参数:

```text
https://x-cmd.com/ppt?content=<URL 编码的 markdown>
```

一两个屏幕的短 deck,一条链接走天下。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#241a3d 0%, #0e0a18 75%)" -->

# 封面,也是一张链接

<a href="?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md"><img src="/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md" width="380" alt="本 deck 的封面"></a>

服务端把指定那一页排成 **SVG** —— 矢量、可缩放,`width` 控制大小。

点图 → 直接开讲。

--

## README 里的标准嵌法

```markdown
[![](https://x-cmd.com/ppt/cover.svg?url=<deck 地址>)](https://x-cmd.com/ppt?url=<deck 地址>)
```

封面永远与第一页**同源同款** —— deck 改了,封面跟着变。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 架构:浏览器直读

## 常见路径零服务端调用

<svg viewBox="0 0 780 300" width="640" xmlns="http://www.w3.org/2000/svg" font-family="ui-sans-serif, PingFang SC, sans-serif">
  <defs>
    <marker id="ar" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse">
      <path d="M0 0 L10 5 L0 10 z" fill="#7c9dff"/>
    </marker>
  </defs>
  <rect x="290" y="20" rx="10" width="200" height="52" fill="#16233d" stroke="#3d5a78"/>
  <text x="390" y="52" text-anchor="middle" font-size="17" fill="#e8f0ff">浏览器(讲台)</text>
  <rect x="40" y="200" rx="10" width="230" height="52" fill="#171b24" stroke="#3a4a63"/>
  <text x="155" y="226" text-anchor="middle" font-size="15" fill="#c8d0da">markdown 源站(GitHub raw)</text>
  <text x="155" y="244" text-anchor="middle" font-size="12" fill="#7f8ba0">自带 CORS 头 · 直读零调用</text>
  <rect x="510" y="200" rx="10" width="230" height="52" fill="#1b1430" stroke="#5a3d78"/>
  <text x="625" y="226" text-anchor="middle" font-size="15" fill="#dcd2f0">ppt Worker(回落 + SSR)</text>
  <text x="625" y="244" text-anchor="middle" font-size="12" fill="#9d8bb8">CORS 被挡才代取 · cover.svg 出图</text>
  <line x1="330" y1="72" x2="180" y2="196" stroke="#7c9dff" stroke-width="2" marker-end="url(#ar)"/>
  <text x="215" y="120" font-size="12.5" fill="#7c9dff">fetch 直读 markdown</text>
  <line x1="450" y1="72" x2="600" y2="196" stroke="#b48cff" stroke-width="2" stroke-dasharray="6 5" marker-end="url(#ar)"/>
  <text x="500" y="120" font-size="12.5" fill="#b48cff">被 CORS 挡住 → 同源代理</text>
</svg>

被 CORS 挡住才回落服务端代取:校验 Referer、限体积、限频率。

--

## 服务端只做一件难事

把**指定的那一页**排成 SVG:

- 画布 960×700,字号/行高/颜色取自主题 CSS
- 字体子集**内嵌**(`<img>` 里取不到外部字体)
- 测量的字,就是渲染的字

于是封面图和浏览器里那一页,看着一样。

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#241a3d 0%, #0e0a18 75%)" -->

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

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 三份案例,点开就讲

- **五分钟** —— 写 deck 的语法速查
- **图表** —— draw 图表与真实数据
- **datalink** —— 数据在链接里(理念篇)

都在首页的 gallery 里,也都在你的收藏栏里。

---

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#1c2a4a 0%, #0d1117 78%)" -->

# 现在就去讲一场

**https://x-cmd.com/ppt**
