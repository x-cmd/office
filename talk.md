# ppt

## 把 markdown 变成一场演讲

- 一个**长链接**就是入口
- 浏览器端 reveal.js 渲染
- 服务端只解决跨域

---

## 场景

> 用 AI 生成一份演讲 markdown,贴进 README,点开就能讲。

```text
[![](https://po6.sh/ppt/cover.svg?url=…)](https://po6.sh/ppt?url=…)
```

没有安装、没有构建、没有账号 —— 只是一个链接。

---

## 形态:webapp,不是 action

| | draw | ppt |
|---|---|---|
| 输入 | 结构化数据(扁平参数) | **一个数据链接** |
| 输出 | 一张 SVG 图 | **一个可交互的 webapp** |
| 渲染时机 | 服务端一次渲完 | **浏览器现场渲染** |

ppt 的主产物是**一场演讲**,不是一张图。图只是附属品。

---

## 原理一:datalink

输入不是数据本身,而是**数据的地址**。

markdown 通常已经躺在仓库里(git raw / gist / 任意静态托管),
用户只想把**它的地址**贴出来 —— 于是"输入"天然是一个链接。

```text
https://x-cmd.com/ppt?url=https://raw.githubusercontent.com/o/r/main/talk.md
```

---

## 原理二:渲染发生在浏览器

服务端**不预渲染幻灯片**,只出一个 HTML 壳:

1. 浏览器请求 `/ppt/raw?url=…`(同源)
2. 拿到 markdown
3. reveal.js 的 markdown 插件在浏览器里切页、渲染

所以幻灯片是活的:主题、翻页、演讲者备注、打印成 PDF,全是 reveal.js 原生能力。

---

## 原理三:跨域由服务端代取

那些放 markdown 的站点大多**不发 CORS 头**,浏览器直接取会被拦。

服务端 fetch 不受同源策略约束 —— 所以后台代取,再以**同源**身份交给浏览器。

代价是后台成了出口,所以必须守住边界:

- 只允许 `http/https`
- 拒绝内网 / 回环 / 云元数据地址
- 限体积、限跳数、限超时

---

## 原理四:SSR 只负责"指定页"

reveal.js **没有**服务端渲染能力(官方只支持浏览器打印成 PDF)。

所以后台只做一件小 事:把**指定的那一页**排成 SVG。

- 画布 960×700(reveal.js 默认尺寸)
- 字号、行高、块间距、颜色 —— 全部取自主题 CSS 的 `--r-*` 变量
- 行盒模型(半行距)照抄浏览器

于是封面图与浏览器里的那一页**看着一样**。

---

## 原理五:测量与渲染同源

折行点要跟浏览器一致,量宽就得用**同一份字体**。

- 内嵌 Source Sans Pro 子集(base64)进 SVG —— `<img>` 引用时无法联网取字体
- 同时导出这份字体的**字宽表**,排版测量与最终渲染零偏差
- 中文回落系统字体 —— 与浏览器里的回落行为一致

这与 draw 的 Inter 做法同源:**测量的字,就是渲染的字**。

---

## 动画模式

封面图也可以是一段动画:依次播几页,最后定格。

```text
/ppt/cover.svg?url=…&anim=0,2,5&freeze=5
```

手段是 SVG 内嵌的 **SMIL** 动画(HTML 标准在 `<img>` 上下文明确允许)。

降级也体面:不支持动画时,看到的就是**定格的那一页**。

---

## 用法

```text
https://x-cmd.com/ppt?url=<markdown 链接>
https://x-cmd.com/ppt?data=<markdown 原文>
https://x-cmd.com/ppt/cover.svg?url=<markdown 链接>&slide=2
```

分页:`---` 横向 · `--` 纵向 · `Note:` 演讲者备注

---

## 边界

- reveal.js 无 SSR → 只保证"指定页"够像,不追求整份一致
- 远端图片不进 SVG(体积 + SSRF 面),画占位框
- 主题字体只内嵌 Source Sans Pro,其余主题用系统字体栈
