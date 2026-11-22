---
template: deck
theme: black
cover:
  title: ppt
  subtitle: 把 markdown 变成一场演讲
  author: x-cmd
  date: 2026-11-23
---

<!-- .slide: data-layout="gallery" data-columns="2" -->

# 四份演示,点开就讲

<div class="ppt-gallery">
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Ftalk.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Ftalk.md" alt="把 markdown 变成一场演讲"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fquickstart.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fquickstart.md" alt="五分钟:写 deck 的语法速查"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fcharts.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fcharts.md" alt="图表:把数据搬上讲台"></a>
<a href="?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fdatalink.md"><img src="/ppt/cover.svg?url=https%3A%2F%2Fraw.githubusercontent.com%2Fx-cmd%2Foffice%2Fmain%2Fdatalink.md" alt="datalink:数据在链接里"></a>
</div>

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1a2740 0%, #0b1120 75%)" -->

# 这个项目在做什么

- **输入**:一个 markdown 链接(`?url=`),或一段原文(`?content=`) <!-- .element: class="fragment" -->
- **输出**:一场 reveal.js 演讲,外加一页页的 SVG 封面图 <!-- .element: class="fragment" -->
- **浏览器直读**:常见路径零 Worker 调用,CORS 才回落服务端代取 <!-- .element: class="fragment" -->
- **图表内联**:` ```draw ` 围栏或 draw 链接,服务端展开成原生 SVG(可点) <!-- .element: class="fragment" -->

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt/cover.svg?url=<markdown 链接>
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#241a3d 0%, #0e0a18 75%)" -->

# 怎么开始写

```markdown
---
cover:
  title: 我的演讲
  subtitle: 一句话说明
  author: 我
  date: 2026-11-23
---

# 第一页

正文。
```

`---` 横向分页 · `--` 纵向分页 · `Note:` 演讲者备注 · `<!-- .slide: data-layout="section" -->` 每页版式与底色。
