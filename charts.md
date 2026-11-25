---
look: swiss
transition: fade
---

<!-- .slide: data-layout="sw-statement" -->

# 一行参数,<br>一张<em>矢量图</em>

markdown 里的一行 draw,讲台上展开成原生 SVG。

**数据图与结构图,两套语法,同一个讲台。**

---

<!-- .slide: data-layout="sw-index" -->

# 这场讲什么

<span class="item"><span class="no">01</span><span class="t">数据图</span><span class="lead"></span><span class="pg">03</span></span>
<span class="item"><span class="no">02</span><span class="t">结构图</span><span class="lead"></span><span class="pg">08</span></span>
<span class="item"><span class="no">03</span><span class="t">怎么配色与排版</span><span class="lead"></span><span class="pg">13</span></span>

---

<!-- .slide: data-layout="sw-statement" -->

# 写法一:<br>draw <em>围栏</em>

围栏语言标成 draw,内容就是图表参数 —— 跟写 URL 查询串一模一样。

--

<!-- .slide: data-layout="sw-figure" -->

# 一行围栏,一张图

```draw
type=bar&t=xcmd&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=380&title=月度活跃
```

<span class="sw-note"><b>FIG.1</b> — 服务端把它展开成内联 SVG:不是图片,是原生矢量,放大不糊,跟主题融在一张画布里。</span>

--

<!-- .slide: data-layout="sw-spec" -->

# 数据图的参数

<span class="row"><span class="k">type</span><span class="v">图种:bar · line · pie · radar · sankey · gauge</span></span>
<span class="row"><span class="k">labels</span><span class="v">类目名,逗号分隔</span></span>
<span class="row"><span class="k">values</span><span class="v">数值,与 labels 一一对应</span></span>
<span class="row"><span class="k">t</span><span class="v">风格:配色 + 字体 + 网格,一套皮</span></span>
<span class="row"><span class="k">w / h</span><span class="v">画布尺寸(像素)</span></span>
<span class="row"><span class="k">title</span><span class="v">图题,也是图的替代文本</span></span>
<span class="row"><span class="k">unit</span><span class="v">单位,标在坐标轴上</span></span>

--

<!-- .slide: data-layout="sw-spec" -->

# 常用图型,各说各的话

<span class="row"><span class="k">bar</span><span class="v">比大小 —— 类目之间横向一比</span></span>
<span class="row"><span class="k">line</span><span class="v">看趋势 —— 随时间往上还是往下</span></span>
<span class="row"><span class="k">pie</span><span class="v">看占比 —— 几块拼成一个整体</span></span>
<span class="row"><span class="k">radar</span><span class="v">看评估 —— 几个维度同时打分</span></span>
<span class="row"><span class="k">sankey</span><span class="v">看流动 —— 东西从哪儿流到哪儿</span></span>
<span class="row"><span class="k">gauge</span><span class="v">看单值 —— 一个进度式的结论</span></span>

--

<!-- .slide: data-layout="sw-figure" -->

# 趋势与占比

```draw
type=line&t=xcmd&labels=一季,二季,三季,四季,五季,六季&values=120,180,150,210,240,290&w=700&h=300&title=周下载量
```

<span class="sw-note"><b>FIG.2</b> — 折线看的是"随时间的走向"。要讲占比就换饼图,别把两种图挤在一页。</span>

--

<!-- .slide: data-layout="sw-spec" -->

# 风格:一个参数换一套皮

<span class="row"><span class="k">t=xcmd</span><span class="v">默认皮 —— 墨色底子,红线点睛</span></span>
<span class="row"><span class="k">t=opendata</span><span class="v">公开数据皮 —— 明亮底,适合截图外发</span></span>
<span class="row"><span class="k">t=pipeline</span><span class="v">流程皮 —— 适合画流转</span></span>
<span class="row"><span class="k">t=rank</span><span class="v">排行皮 —— 适合画榜单</span></span>
<span class="row"><span class="k">t=market</span><span class="v">等宽皮 market-mono —— 适合对齐密集标签</span></span>
<span class="row"><span class="k">十几套</span><span class="v">evil · opendata · market-mono · pipeline · rank …</span></span>

---

<!-- .slide: data-layout="sw-statement" -->

# 写法二:<br>贴 draw 的<em>链接</em>

图片地址指向图表服务,同样会被内联 —— 而且能点。

--

<!-- .slide: data-layout="sw-figure" -->

# 外面套一层链接,图就能点

[![月度活跃](https://x-cmd.com/draw?type=bar&t=xcmd&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=380&title=月度活跃)](https://x-cmd.com/draw/explore?type=bar&t=xcmd&labels=一月,二月,三月,四月&values=12,19,14,23&w=720&h=380&title=月度活跃)

<span class="sw-note"><b>FIG.3</b> — 讲台上点一下跳进 draw 的 explore:悬停看数、现场改参数,当场讲清楚这张图怎么来的。</span>

---

<!-- .slide: data-layout="sw-statement" -->

# 结构图:<br>draw/<em>图种</em>

数据图有 type=,结构图没有 —— 它走自己的端点。

--

<!-- .slide: data-layout="sw-spec" -->

# 围栏标成 draw/图种

<span class="row"><span class="k">n=</span><span class="v">节点:id;type;label[;sub][;pos]</span></span>
<span class="row"><span class="k">e=</span><span class="v">连线:from;to[;label][;variant]</span></span>
<span class="row"><span class="k">b=</span><span class="v">分组/边界:label;id id …</span></span>
<span class="row"><span class="k">pos</span><span class="v">r0c1 格子 · r0c1w2 跨格 · p40,80 像素</span></span>
<span class="row"><span class="k">换行</span><span class="v">用 %0A —— 标签里不能有 ; 和 :</span></span>
<span class="row"><span class="k">画布</span><span class="v">同样是 w= h= title=</span></span>

--

<!-- .slide: data-layout="sw-figure" -->

# 时序图:一次请求

```draw/seq
n=u;fe;浏览器;;r0c0&n=app;be;ppt webapp;;r0c1&n=gh;ext;GitHub;;r0c2&n=dr;svc;draw;;r0c3&e=u;app;打开 ?url=&e=app;gh;直读正文与评论&e=app;dr;展开图表&title=一次打开&w=720&h=320
```

<span class="sw-note"><b>FIG.4</b> — 参与方按 n= 出现的顺序从左到右排;e= 按时间先后写,回信在 label 尾段加 ;dash。</span>

--

<!-- .slide: data-layout="sw-figure" -->

# 架构图:谁跟谁说话

```draw/arch2
n=gw;cloud;API Gateway;REST 入口;r0c0&n=fn;be;Lambda;业务逻辑;r1c0&n=ddb;db;DynamoDB;数据表;r2c0&n=iam;sec;IAM;最小权限;r0c1&n=cog;be;CloudWatch;指标与告警;r3c0&e=gw;fn;同步调用&e=gw;fn;异步入队&e=fn;ddb;读写&e=iam;fn;授权&b=Edge;gw iam&b=Data;fn ddb&title=无服务器 API&w=820&h=380
```

<span class="sw-note"><b>FIG.5</b> — 架构图词汇:fe 前端 · be 后端 · db 数据库 · cloud 云服务 · sec 安全 · bus 消息 · svc 服务 · ext 外部。</span>

--

<!-- .slide: data-layout="sw-grid" -->

# 常用的几种结构图

<div class="sw-grid">
<span class="cell"><span class="no">01</span><span class="t">seq</span><span class="d">时序 —— 谁先找谁,一条消息一个来回。</span></span>
<span class="cell"><span class="no">02</span><span class="t">arch2 / archmap</span><span class="d">架构 —— 系统怎么摆,边界在哪儿。</span></span>
<span class="cell"><span class="no">03</span><span class="t">erd / class</span><span class="d">数据与类型 —— 表与类,字段写进 sub。</span></span>
<span class="cell"><span class="no">04</span><span class="t">lifecycle</span><span class="d">状态机 —— 状态怎么流转,哪条路通向失败。</span></span>
<span class="cell"><span class="no">05</span><span class="t">journey / kanban</span><span class="d">旅程与看板 —— 用户经历了什么,任务卡在哪。</span></span>
<span class="cell"><span class="no">06</span><span class="t">gantt / mindmap</span><span class="d">排期与脑图 —— 时间条与树的两种排布。</span></span>
</div>

--

<!-- .slide: data-layout="sw-figure" -->

# 状态机:每条流水线都是

```draw/lifecycle
n=commit;terminal;提交;push / PR;r0c0&n=lint;state;静态检查;eslint + tsc;r1c0&n=lintok;decision;通过?;;r2c0&n=unit;state;单元测试;vitest;r2c1&n=unitok;decision;通过?;;r3c1&n=build;state;构建镜像;docker buildx;r3c2&n=staging;state;部署 staging;r4c2&n=gate;decision;冒烟通过?;;r5c2&n=prod;state;全量发布;canary;r6c2&n=done;terminal;上线;;r7c2&n=fail;terminal;失败;通知作者&e=commit;lint&e=lint;lintok&e=lintok;unit;是&e=lintok;fail;否&e=unit;unitok;是&e=unitok;fail;否&e=build;staging&e=staging;gate&e=gate;prod;是&e=gate;fail;否&e=prod;done&title=CI 流水线&w=780&h=430
```

<span class="sw-note"><b>FIG.6</b> — 状态图词汇:state 状态 · decision 判定 · terminal 起止。决策节点永远两条出路:是 / 否。</span>

---

<!-- .slide: data-layout="sw-statement" -->

# 图与字,<br>各占<em>一半</em>

一页的主角只有一个:图,或者字。挤在一起,两个都不成立。

--

<!-- .slide: data-layout="sw-figure" -->

# 图注小到几乎没有

```draw
type=bar&labels=标题区,主体区,留白区&values=22,46,32&w=700&h=280&title=一页纸的面积分配
```

<span class="sw-note"><b>FIG.7</b> — 主体区只占四成半,剩下的是标题与留白。图注只说口径,不复述图里已经有的东西。</span>

--

<!-- .slide: data-layout="sw-spec" -->

# 图与字的比例

<span class="row"><span class="k">标题</span><span class="v">1.55em —— 结论句,不是话题</span></span>
<span class="row"><span class="k">图</span><span class="v">吃掉剩余空间,左缘与标题对齐</span></span>
<span class="row"><span class="k">图注</span><span class="v">13px —— 口径、出处、一句点评</span></span>
<span class="row"><span class="k">正文</span><span class="v">19px —— 最多六行,超过就换页</span></span>
<span class="row"><span class="k">留白</span><span class="v">至少三成 —— 挤满的一页等于没有重点</span></span>
<span class="row"><span class="k">一页一图</span><span class="v">两张图 = 两页,除非你就是要对比</span></span>

--

<!-- .slide: data-layout="sw-quote" -->

<span class="sw-qmark">“</span>

# 图是<em>证据</em>,<br>字是<em>结论</em>。

<span class="sw-attr">Swiss Design · 1950s</span>

---

<!-- .slide: data-layout="sw-spec" -->

# 配色:图跟着 deck 走

<span class="row"><span class="k">chart-ink</span><span class="v">线的颜色 —— 瑞士式是纯墨 #111111</span></span>
<span class="row"><span class="k">chart-text</span><span class="v">字的颜色 —— 别用纯黑,留一点暖</span></span>
<span class="row"><span class="k">chart-muted</span><span class="v">次要信息 —— 轴线、浅色标签</span></span>
<span class="row"><span class="k">chart-grid</span><span class="v">网格线 —— 一根发丝就够</span></span>
<span class="row"><span class="k">chart-accent</span><span class="v">强调色 —— 一根红 #e63312 打重点</span></span>
<span class="row"><span class="k">chart-font</span><span class="v">图里的字体 —— 无衬线,跟正文同一套</span></span>

<span class="sw-note">变量名全称是 `--ppt-chart-*` —— 在 deck 的 `style:` 里改,图立刻换色。</span>

--

<!-- .slide: data-layout="sw-timeline" -->

# 一张图的四个决定

<div class="sw-tl">
<span class="node"><span class="yr">01</span><span class="stage">图型</span><span class="note">比大小用柱,看走向用线,看占比用饼。选错图型,数据就白给了。</span></span>
<span class="node"><span class="yr">02</span><span class="stage">颜色</span><span class="note">一套皮只留两个颜色:墨与红。其余交给网格和留白。</span></span>
<span class="node"><span class="yr">03</span><span class="stage">尺寸</span><span class="note">w h 决定画布。长宽比按内容挑,别让标签挤成一列字。</span></span>
<span class="node"><span class="yr">04</span><span class="stage">图注</span><span class="note">一句话说明口径与出处。没有来源的数字不该上台。</span></span>
</div>

---

<!-- .slide: data-layout="sw-end" -->

# 下一张图,<br>从<em>这里</em>开始

<span class="sw-foot">x-cmd.com/draw · 2026</span>
