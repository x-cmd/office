---
template: center
theme: black
---

# 图表

封面图与内联图表的玩法。

---

# 封面图

```text
https://x-cmd.com/ppt/cover.svg?url=<deck 的地址>
```

服务端把**指定的那一页**排成 SVG —— 矢量、可缩放、能放进 README。

--

## 换主题、换页

| 参数 | 作用 |
|---|---|
| `theme=dark` | 换主题(14 款内置) |
| `slide=3` | 第 3 页(展平页号) |
| `slide=1.2` | 第 1 个主题里的第 2 页 |

--

## 动画

| 参数 | 作用 |
|---|---|
| `anim=0,2,5` | 依次播这几页 |
| `freeze=5` | 最后定格在第 5 页 |
| `dur=2` | 每页停留秒数 |

```text
/ppt/cover.svg?url=…&slide=4.1
/ppt/cover.svg?url=…&anim=0,1,2,3&freeze=3&dur=2
```

--

## 不支持动画也不怕

SVG 内嵌的是 **SMIL** 动画(HTML 标准在 `<img>` 上下文明确允许)。

不支持的浏览器看到的就是**定格的那一页** —— 永远不会白屏。

---

# 内联图表

服务端把围栏展开成**内联 SVG**,浏览器原生渲染 —— 矢量、可缩放,不是图片:

```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```

--

## 写法就一句

围栏的语言标成 `draw`,内容是图表服务的参数:

````markdown
```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```
````

--

## 或者直接贴 draw 的链接

[![各模块行数](https://x-cmd.com/draw?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&t=xcmd&labels=排版,取数,路由,页面&values=615,272,263,327)

指向图表服务的图片,同样会被内联成原生 SVG。

外面套一层链接 → **点图跳到别处**(这里是 draw 的 explore:悬停看数、改参数)。

--

## 还能是表格

表格、引用、列表、代码块 —— 都是标准 markdown,排版由服务端照着主题 CSS 复刻。

---

# 三个案例

- **本 deck** —— 图表与封面图的玩法
- **五分钟** —— 写 deck 的语法速查
- **draw** —— 把数据变成一张图

---

# 你的下一个 deck

**https://x-cmd.com/ppt**
