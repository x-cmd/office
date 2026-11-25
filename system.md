---
title: 一个请求的一生
theme: black
look: blueprint
transition: fade
---

<!-- .slide: data-layout="tc-title" -->

<span class="sheet-head"><span>X-CMD/PPT · SYSTEM SHEET</span><span>REV 2026-11</span></span>

# 一个请求的<br><b>一生</b>

## 架构与流程图 · 从一次打开到一张图

<span class="rev">DWG № 2026-1125 · SCALE 1:1 · SHEET 1/13</span>

--

<!-- .slide: data-layout="tc-spec" -->

<span class="sheet-head"><span>§1 · OVERVIEW</span><span>总览</span></span>

# 一次请求穿过哪些部件

<p class="ppt-lead">渲染在浏览器,服务端只做一件难事:把 CORS 挡住的那次代取完成。</p>

| 层 | 部件 | 职责 |
|---|---|---|
| 源站 | GitHub / issue / raw | 存放 markdown 源文件 |
| 浏览器 | fetch + marked | 直读源站、切页、渲染 |
| 服务端 | Worker / Node | CORS 受阻时代取;出封面图 |
| 绘图 | x-cmd/draw | 把 `draw` 围栏展开成内联矢量 SVG |
| 讲台 | reveal.js | 放映、标注、备注、缩略图 |

--

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§1 · PIPELINE</span><span>打开一份 deck</span></span>

# 打开一份 deck 时

```draw/seq
n=u;fe;浏览器;;r0c0&n=app;fe;讲台;;r0c1&n=gh;ext;GitHub;;r0c2&n=dr;svc;draw;;r0c3&e=u;app;打开 ?url&e=app;gh;直读正文与评论&e=app;dr;展开图表&title=一次打开&w=760&h=300
```

<span class="figcap"><b>FIG.1</b> — OPEN PIPELINE · 浏览器直读源站,CORS 受阻才回落服务端</span>

--

<!-- .slide: data-layout="tc-flow" -->

<span class="sheet-head"><span>§1 · PIPELINE</span><span>四道工序</span></span>

# 从链接到讲台

| STEP 01 | STEP 02 | STEP 03 | STEP 04 |
|---|---|---|---|
| <span class="fl-name">取源</span><span class="fl-note">issue / PR / raw 归一成一个 URL</span> | <span class="fl-name">切页</span><span class="fl-note">`---` 与 `--` 分出主题与子页</span> | <span class="fl-name">展开图</span><span class="fl-note">draw 围栏换成内联矢量 SVG</span> | <span class="fl-name">渲染</span><span class="fl-note">讲台与封面图同源同版</span> |

--

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§1 · DEPLOY</span><span>部署形态</span></span>

# 部署形态:无服务器

```draw/arch2
n=gw;cloud;API Gateway;REST 入口;r0c0;aws:apigw&n=fn;be;Lambda;业务逻辑;r1c0;aws:lambda&n=ddb;db;DynamoDB;数据表;r2c0;aws:dynamodb&n=sqs;bus;SQS;异步队列;r2c1;aws:sqs&n=iam;sec;IAM;最小权限;r0c1;aws:iam&n=cog;be;CloudWatch;指标与告警;r3c0;aws:cloudwatch&e=gw;fn;同步调用&e=gw;sqs;异步入队&e=fn;ddb;读写&e=sqs;fn;消费&e=iam;fn;授权&e=fn;cog;埋点&b=Edge;gw iam&b=Compute;fn sqs&b=Data;ddb&title=无服务器 API&w=860&h=460
```

<span class="figcap"><b>FIG.2</b> — SERVERLESS API · 入口、计算、存储三条线各司其职</span>

---

<!-- .slide: data-layout="tc-spec" -->

<span class="sheet-head"><span>§2 · DATA</span><span>数据怎么走</span></span>

# markdown → 页面 → 图表

<p class="ppt-lead">三段流水线:每一段只认上一段的产物,页与图都从同一份 markdown 里长出来。</p>

| 阶段 | 输入 | 处理 | 产物 |
|---|---|---|---|
| 源 | markdown 源文件 | 按 `---` / `--` 切页,摘掉 frontmatter | 一组页 |
| 页 | 一页 markdown | marked 解析;`draw` 围栏换成内联 SVG | 一段 HTML |
| 图 | draw 查询参数 | 代理到 x-cmd/draw,剥掉角标 | 一张自包含 SVG |

--

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§2 · PIPELINE</span><span>流水线是状态机</span></span>

# 每条流水线都是状态机

```draw/lifecycle
n=commit;terminal;提交;push / PR;r0c0&n=lint;state;静态检查;eslint + tsc;r1c0&n=lintok;decision;通过?;;r2c0&n=unit;state;单元测试;vitest;r2c1&n=unitok;decision;通过?;;r3c1&n=build;state;构建镜像;docker buildx;r3c2&n=staging;state;部署 staging;k8s;r4c2&n=gate;decision;冒烟通过?;;r5c2&n=prod;state;全量发布;canary;r6c2&n=done;terminal;上线;;r7c2&n=fail;terminal;失败;通知作者;r3c0&e=commit;lint&e=lint;lintok&e=lintok;unit;是&e=lintok;fail;否&e=unit;unitok;是&e=unitok;fail;否&e=build;staging&e=staging;gate&e=gate;prod;是&e=gate;fail;否&e=prod;done&title=CI 流水线&w=780&h=520
```

<span class="figcap"><b>FIG.3</b> — CI LIFECYCLE · 每个节点都是一次判定,每条边都是一次转移</span>

--

<!-- .slide: data-layout="tc-figure" -->

<span class="sheet-head"><span>§2 · SCHEMA</span><span>表结构</span></span>

# ERD:租户挂在最上面

```draw/erd
n=tenants;table;tenants;id:uuid (pk)%0Aslug:text (uk)%0Aplan:text&n=users;table;users;id:uuid (pk)%0Aemail:text (uk)&n=memberships;table;memberships;tenant_id:uuid%0Auser_id:uuid%0Arole:text&n=projects;table;projects;id:uuid (pk)%0Atenant_id:uuid%0Aname:text&n=tasks;table;tasks;id:uuid (pk)%0Aproject_id:uuid%0Aassignee_id:uuid%0Astatus:text&n=comments;table;comments;id:uuid (pk)%0Atask_id:uuid%0Abody:text&n=api_keys;table;api_keys;id:uuid (pk)%0Atenant_id:uuid%0Aprefix:text (uk)&n=audit_log;table;audit_log;id:uuid (pk)%0Atenant_id:uuid%0Aaction:text&e=tenants;memberships;1:N&e=users;memberships;1:N&e=tenants;projects;1:N&e=projects;tasks;1:N&e=users;tasks;1:N&e=tasks;comments;1:N&e=tenants;api_keys;1:N&e=tenants;audit_log;1:N&title=Multi-tenant SaaS&w=900&h=540
```

<span class="figcap"><b>FIG.4</b> — MULTI-TENANT SCHEMA · 租户 → 成员 → 项目 → 任务 → 评论</span>

--

<!-- .slide: data-layout="tc-rev" -->

<span class="sheet-head"><span>§2 · REVISION</span><span>修订记录</span></span>

# REV

- <span class="rev-id">REV C</span><span class="rev-date">2026-11-25</span><span class="rev-text"><code>look: blueprint</code> 落到九种语义页型,老版式手写页全部换掉</span>
- <span class="rev-id">REV B</span><span class="rev-date">2026-11-23</span><span class="rev-text">图种分流:<code>draw/&lt;kind&gt;</code> 走结构图端点,<code>draw</code> 走数据图端点</span>
- <span class="rev-id">REV A</span><span class="rev-date">2026-11-18</span><span class="rev-text">首版 —— 链接即演示,封面图与讲台第一页永远一致</span>

---

<!-- .slide: data-layout="tc-keys" -->

<span class="sheet-head"><span>§3 · OPERATION</span><span>讲台操作面</span></span>

# 键位

<p class="ppt-lead">讲台上的六个动作:换页、备注、标注、总览、全屏、速查。</p>

| 键 | 功能 |
|---|---|
| <span class="key">←</span> <span class="key">→</span> | 换页(含纵向子页) |
| <span class="key">S</span> | 演讲者备注(跨窗口同步) |
| <span class="key">W</span> | 标注:画笔 / 荧光 / 划词 |
| <span class="key">ESC</span> | 缩略图总览 |
| <span class="key">F</span> | 全屏 |
| <span class="key">?</span> | 快捷键速查 |

--

<!-- .slide: data-layout="tc-matrix" -->

<span class="sheet-head"><span>§3 · BOUNDARY</span><span>缓存与限流</span></span>

# 边界:体积、限流、缓存

| 项 | 数值 | 说明 |
|---|---|---|
| deck 体积 | 512KB | 一份 deck 的上限,超了会被截断 |
| 直传 URL | 约 6KB | 内容直传的总长度,长 deck 仍需托管 |
| 取源限流 | 60/分 | 每 IP 每分钟,共享出口容易触顶(403) |
| 浏览器缓存 | 24h | 源改了放映跟着变,旧版本最长活 24 小时 |
| 取图上限 | 4MB | 单张图的大小上限 |

--

<!-- .slide: data-layout="tc-notes" -->

<span class="sheet-head"><span>§3 · CONSTRAINTS</span><span>设计约束</span></span>

# NOTES

<span class="note"><span class="no">N-01</span>常见路径服务端零参与:浏览器自带 CORS 头,markdown 直接读回来</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-02</span>CORS 被挡才回落 Worker 代取 —— 服务端只做这一件难事</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-03</span>图表内联为矢量 SVG,缩放不糊</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-04</span>版式即海报:几何装饰由模板统一提供,deck 只写内容</span> <!-- .element: class="note fragment" -->
<span class="note"><span class="no">N-05</span>输入只能是 URL 或 markdown —— 不接受二进制附件</span> <!-- .element: class="note fragment" -->

--

<!-- .slide: data-layout="tc-eof" -->

<span class="sheet-head"><span>END OF DOCUMENT</span><span>X-CMD/PPT</span></span>

<span class="endmark">EOF</span>

<span class="sub">SHEET 13/13 · 架构即 URL:https://x-cmd.com/ppt</span>

```draw
type=qr&d=https://x-cmd.com/ppt&fg=%230a1524&bg=%23ffffff&w=240&h=240
```
