---
template: deck
theme: black
cover:
  title: ppt
  subtitle: 把 markdown 变成一场演讲
  author: x-cmd
  date: 2026-11-14
---

<!-- .slide: data-layout="gallery" -->

# 演示

一份 markdown = 一场演讲。每一张都是真 deck 的封面,**点一下就开讲**。

<div class="ppt-gallery">
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Ftalk.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Ftalk.md" alt="把 markdown 变成一场演讲"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fquickstart.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fquickstart.md" alt="五分钟:写 deck 的语法速查"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fcharts.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fcharts.md" alt="图表:把数据搬上讲台"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fdatalink.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fdatalink.md" alt="datalink:数据在链接里"></a>
</div>

---

# 这个项目在做什么

- **输入**:一个 markdown 链接(`?url=`),或一段原文(`?content=`)
- **输出**:一场 reveal.js 演讲,外加一页页的 SVG 封面图
- **浏览器直读**:常见路径零 Worker 调用,CORS 才回落服务端代取
- **图表内联**:` ```draw ` 围栏或 draw 链接,服务端展开成原生 SVG(可点)

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt/cover.svg?url=<markdown 链接>
```

---

# 怎么开始写

```markdown
---
cover:
  title: 我的演讲
  subtitle: 一句话说明
  author: 我
  date: 2026-11-14
---

# 第一页

正文。
```

`---` 横向分页 · `--` 纵向分页 · `Note:` 演讲者备注 · `<!-- .slide: data-layout="section" -->` 每页版式。
