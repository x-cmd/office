---
theme: black
cover:
  title: 一个请求的一生
  subtitle: ppt 的架构 · 结构图速览
  author: x-cmd
  date: 2026-11-23
  background: aurora-blue
---

<!-- .slide: data-layout="statement" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

**渲染在浏览器,服务端只做一件难事。**

---

<!-- .slide: data-layout="two-col" -->

# 打开一份 deck 时

浏览器直读源站;被 CORS 挡住才回落服务端代取

```draw/seq
n=u;fe;浏览器;;r0c0&n=app;be;ppt webapp;;r0c1&n=gh;ext;GitHub;;r0c2&n=dr;svc;draw;;r0c3&e=u;app;打开 ?url=&e=app;gh;直读正文与评论&e=app;dr;展开图表&title=一次打开&w=720&h=320
```

--

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#2a1f4d 0%, #181130 55%, #0e0a18 100%)" -->

# 部署形态:无服务器

--

```draw/arch2
n=gw;cloud;API Gateway;REST 入口;r0c0;aws:apigw&n=fn;be;Lambda;业务逻辑;r1c0;aws:lambda&n=ddb;db;DynamoDB;数据表;r2c0;aws:dynamodb&n=sqs;bus;SQS;异步队列;r2c1;aws:sqs&n=iam;sec;IAM;最小权限;r0c1;aws:iam&n=cog;be;CloudWatch;指标与告警;r3c0;aws:cloudwatch&e=gw;fn;同步调用&e=gw;sqs;异步入队&e=fn;ddb;读写&e=sqs;fn;消费&e=iam;fn;授权&e=fn;cog;埋点&b=Edge;gw iam&b=Compute;fn sqs&b=Data;ddb&title=无服务器 API&w=860&h=460
```

---

<!-- .slide: data-layout="section" data-background-gradient="radial-gradient(#1c3050 0%, #122036 55%, #0b1120 100%)" -->

# 每条流水线都是状态机

--

```draw/lifecycle
n=commit;terminal;提交;push / PR;r0c0&n=lint;state;静态检查;eslint + tsc;r1c0&n=lintok;decision;通过?;;r2c0&n=unit;state;单元测试;vitest;r2c1&n=unitok;decision;通过?;;r3c1&n=build;state;构建镜像;docker buildx;r3c2&n=staging;state;部署 staging;k8s;r4c2&n=gate;decision;冒烟通过?;;r5c2&n=prod;state;全量发布;canary;r6c2&n=done;terminal;上线;;r7c2&n=fail;terminal;失败;通知作者;r3c0&e=commit;lint&e=lint;lintok&e=lintok;unit;是&e=lintok;fail;否&e=unit;unitok;是&e=unitok;fail;否&e=build;staging&e=staging;gate&e=gate;prod;是&e=gate;fail;否&e=prod;done&title=CI 流水线&w=780&h=520
```

---

<!-- .slide: data-layout="two-col" -->

# 数据住在库里,长这样

多租户 SaaS 的表结构(draw 案例册 #10)

```draw/erd
n=tenants;table;tenants;id:uuid (pk)%0Aslug:text (uk)%0Aplan:text&n=users;table;users;id:uuid (pk)%0Aemail:text (uk)&n=memberships;table;memberships;tenant_id:uuid%0Auser_id:uuid%0Arole:text&n=projects;table;projects;id:uuid (pk)%0Atenant_id:uuid%0Aname:text&n=tasks;table;tasks;id:uuid (pk)%0Aproject_id:uuid%0Aassignee_id:uuid%0Astatus:text&n=comments;table;comments;id:uuid (pk)%0Atask_id:uuid%0Abody:text&n=api_keys;table;api_keys;id:uuid (pk)%0Atenant_id:uuid%0Aprefix:text (uk)&n=audit_log;table;audit_log;id:uuid (pk)%0Atenant_id:uuid%0Aaction:text&e=tenants;memberships;1:N&e=users;memberships;1:N&e=tenants;projects;1:N&e=projects;tasks;1:N&e=users;tasks;1:N&e=tasks;comments;1:N&e=tenants;api_keys;1:N&e=tenants;audit_log;1:N&title=Multi-tenant SaaS&w=900&h=540
```

--

<!-- .slide: data-layout="end" data-background-gradient="radial-gradient(#24406e 0%, #16233d 48%, #0b1120 100%)" -->

# 架构即 URL

**https://x-cmd.com/ppt**
