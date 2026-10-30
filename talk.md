# ppt

## 把 markdown 变成一场演讲

长链接即入口 · 浏览器端 reveal.js 渲染

[![本项目各模块行数](https://x-cmd.com/draw?type=bar&labels=排版,取数,路由,页面,其它&values=615,272,263,327,431&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&labels=排版,取数,路由,页面,其它&values=615,272,263,327,431)

---

# 一 · 它是什么

## webapp,不是 action

| | draw | ppt |
|---|---|---|
| 输入 | 数据(参数) | **链接** |
| 输出 | 一张图 | **一场演讲** |
| 渲染 | 服务端 | **浏览器** |

--

## 一个链接,一场演讲

```text
https://x-cmd.com/ppt?url=<markdown 链接>
```

贴进 README,别人点开就能讲。

--

## 封面就是一个 SVG

[![本 deck 的封面](https://po6.sh/ppt/cover.svg?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md)](https://po6.sh/ppt?url=https://raw.githubusercontent.com/x-cmd/office/main/talk.md)

上面这张图**就是这份 deck 的封面** —— 服务端把封面那页排成了 SVG(矢量、可缩放)。

点它 → 打开这份演示。

---

# 二 · 原理

## datalink

输入是**地址**,不是内容。

markdown 一般已经躺在仓库里,用户只想贴它的地址。

--

## 渲染在浏览器

服务端只出 HTML 壳:

1. 浏览器取 markdown(经同源代理)
2. reveal.js 切页、渲染

幻灯片是活的 —— 主题、翻页、备注、打印 PDF,全是原生能力。

--

## 同源代理

源站大多**不发 CORS 头**,浏览器直接取会被拦。

服务端 fetch 不受同源策略约束 → 代取 → 以**同源**身份交给浏览器。

后台成了出口,所以要守边界:

- 只允许 `http/https`
- 拒绝内网 / 回环 / 云元数据
- 限体积、跳数、超时、频率

--

## 取过一次就够了

备注窗口(S)会再开一个接收端页面,它本会**再取一次** markdown。

所以前端把取到的内容存进 `localStorage`(同源共享),之后一律用缓存 —— 不再回源。

---

# 三 · 封面图

## SSR 只做一页

reveal.js **没有**服务端渲染能力。

所以后台只把**指定的那一页**排成 SVG:

- 画布 960×700
- 字号 / 行高 / 间距 / 颜色 —— 取自主题 CSS
- 行盒模型照抄浏览器

于是封面图与浏览器里那一页**看着一样**。

--

## 测量与渲染同源

折行点要跟浏览器一致,量宽就得用**同一份字体**。

- 内嵌字体子集进 SVG(`<img>` 引用时取不到字体)
- 同一份字体的**字宽表**用于排版

测量的字,就是渲染的字。

--

## 也能是一段动画

依次播几页,最后定格:

```text
/ppt/cover.svg?url=…&anim=0,2,5&freeze=5
```

SVG 内嵌 **SMIL** 动画(HTML 标准在 `<img>` 上下文明确允许)。

不支持动画时,看到的就是**定格的那一页**。

---

# 四 · 图表

## 围栏里写参数

服务端展开成**内联 SVG**,浏览器原生渲染 —— 矢量、可缩放,不是图片:

```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```

写法就一句:

````markdown
```draw
type=bar&labels=Jan,Feb,Mar&values=3,5,4&w=560&h=300
```
````

--

## 或者直接贴 draw 的链接

[![各模块行数](https://x-cmd.com/draw?type=bar&labels=排版,取数,路由,页面&values=615,272,263,327&w=560&h=300)](https://x-cmd.com/draw/explore?type=bar&labels=排版,取数,路由,页面&values=615,272,263,327)

指向图表服务的图片,同样会被内联成原生 SVG。

外面套一层链接 → **点图跳到别处**(这里是 draw 的 explore:悬停看数、改参数)。

---

# 五 · 用法

## 怎么翻

- `← →` 换主题 · `↑ ↓` 换主题内的页
- `ESC` 看全部幻灯片 · `S` 演讲者备注
- `?print-pdf` 直接打印成 PDF

--

## 三条链接

```text
/ppt?url=<markdown 链接>            # 演讲
/ppt?data=<markdown 原文>            # 演讲(内联)
/ppt/cover.svg?url=<链接>&slide=1.2  # 指定页
```

分页:`---` 横向 · `--` 纵向 · `Note:` 备注

--

## 边界

- reveal.js 无 SSR → 只保证"指定页"够像
- 远端图片不进 SVG,画占位框
- 主题字体只内嵌 Source Sans Pro
- 私有仓库的 deck 需另加 token 支持
