# overseas-collection-monitor

海外长账龄监控的静态网页发布仓库。GitHub Pages负责展示已生成的报表；取数、加工和每日结论由维护机上的Codex任务执行。

本文统一记录仓库文件、墨西哥定版、每日17点更新、观远接入和维护操作。印尼、菲律宾、泰国的取数口径由各自维护者管理，本文不替它们定义业务规则。

## 1. 网页入口与仓库文件

| 文件 | 作用 | 网页入口 |
| --- | --- | --- |
| `Id.html` | 印尼监控完整HTML | [打开印尼监控](https://maxyu-0302.github.io/overseas-collection-monitor/Id.html) |
| `Ph.html` | 菲律宾监控完整HTML | [打开菲律宾监控](https://maxyu-0302.github.io/overseas-collection-monitor/Ph.html) |
| `Th.html` | 泰国监控完整HTML | [打开泰国监控](https://maxyu-0302.github.io/overseas-collection-monitor/Th.html) |
| `Mx.html` | 墨西哥页面结构、内嵌业务数据、真实楷体字体、样式、筛选和图表代码；另含新版检查脚本 | [打开墨西哥监控](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html) |
| `Mx.version.json` | 墨西哥版本标记，供页面检查是否出现新版；不负责取数或执行任务 | [查看版本标记](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.version.json) |
| `README.md` | 本说明：文件用途、时间设置、复刻、发布、观远接入和故障处理 | 当前文档 |

文件名区分大小写。墨西哥入口是 `Mx.html`，维护时保持名称不变。观远应填写上表的 `github.io` 网页地址。

仓库及Pages网页目前公开。2026-11-17已确认墨西哥完整监控可公开，保留催员姓名、个人业绩和每日历史。网页直接访问不继承观远权限；数据库凭据、Cookie、查询回执和独立核对资料不提交到这里。

## 2. 墨西哥定版基线

2026-11-17用户确认截图中的回款归组修订版定版，业务版本标记为 `BUSINESS_RECEIPT_EVENT_QUEUE_V1`。

- 业务现金按每笔回款发生时的承接队列归组，保持已确认的账龄、资格、本金、补充现金及目标规则。
- 个人统计沿用 `PERSONAL_DPD_GT30_VERIFIED_NONACTUAL_V3`；个人范围和业务组范围分别核验。
- 11月M2个人目标为每日 **3,477 MXN**、全月 **104,310 MXN**；不能恢复旧个人目标。
- 基线数据截至 **2026-11-14**。定版日期、网页生成时间与数据截止日分别记录，后续更新以真实完整数据日为准。
- 定版原网页的源码提交记录为 `abb05bc8eb9a03e3768a60ed2df5e31c4ca5cb83`；本地完整主HTML基线SHA256为 `16e917265f721cf8cd7166b938a92208551bd89a5c3a5d4aa8fda0d4b17e4374`。
- GitHub初次墨西哥网页提交为 `54ff99754eccfcacb4482ea26b6c7d44b76c9dca`，其数据已与上述基线核对一致。它不是本次README提交号，也不是以后每天固定不变的版本号。

本地 `release_approval.json` 登记本次定版；以后改口径或换验收分支，要先验证并重新确认版本。允许数据公开和确认版本验收是两个独立条件。

## 3. 这些文件在哪里运行

**GitHub仓库现在只保存展示文件和本README。下表是维护机上的文件，不会随克隆本仓库自动下载。**

当前维护机项目根目录：

```text
C:\Users\user\Documents\ChatGPT\海外5过长账龄
```

以下路径均相对该根目录：

| 本机文件或目录 | 作用 |
| --- | --- |
| `outputs/墨西哥长账龄监控_20261115/墨西哥长账龄监控.html` | 取数与核验后生成的完整主HTML，是Pages打包的输入 |
| `work/mx_monitor_20261115/revision/data.json` | 本地业务、个人、目标及历史数据；网页本身不连接数仓 |
| 同目录 `daily_conclusions.json`、`daily_collector_revisions.json`、`daily_business_revisions.json` | 持续保留每日结论、个人修订和业务修订；不能覆盖原历史 |
| 同目录 `event_attribution.py`、`make_queries.py` | 按定版规则生成取数SQL；后续刷新不得复制旧运行目录的末队列现金归组SQL |
| 同目录 `analyze_update.py`、`build.py` 及模板、样式、核验脚本 | 生成结论和主HTML，并核对金额、目标、历史与交互 |
| 同目录 `DAILY_UPDATE.md` | 维护规则、确认口径、过程记录及本轮最新状态；历史条目按日期阅读 |
| `work/mx_git_deploy/prepare_pages_candidate.py` | 从主HTML生成同一批 `Mx.html`、`Mx.version.json`，保留业务JSON，加入新版检查 |
| `work/mx_git_deploy/pages_refresh.js` | 新版检查的源代码；打包时内联到 `Mx.html`，不需要另在观远或README里执行 |
| `work/mx_git_deploy/publish_pages.py` | 读取定版门控，生成发布包，使用已有Git认证提交两个墨西哥文件；不取新数、不强推、不覆盖其他国家文件 |
| `work/mx_git_deploy/verify_pages.py` | 读取已发布版本和HTML，核对业务日期与实际Git文件摘要；只推送成功不算完成 |
| `work/mx_git_deploy/release_approval.json` | 定版与自动发布门控，记录已确认源码引用和版本；未批准时在联网、推送前拦截 |
| `work/mx_git_deploy/github_pages_authorization.json` | 记录完整数据公开的授权范围；它不是定版审批，也不存凭据 |
| `work/mx_git_deploy/pages_latest.json`、`pages_publication.json`、`pages_runs/` | 最新执行状态、最近成功线上核验及逐次发布记录；用于判断成功阶段和回退 |
| `work/mx_git_deploy/automation_pages_configuration.json` | 定时配置的本地记录副本；修改它不会更改真实定时器 |
| `outputs/墨西哥GitHubPages待发布包_20261117/` | 本地生成包及操作手册；只提交其中两个网站文件，不整包上传 |
| `work/mx_guanyuan_native/`、`outputs/墨西哥监控自助更新/` | 旧自定义图表三栏转换及复刻工具；使用Pages外链后不再作为日常观远更新方式 |

真实定时任务在 **Codex的“墨西哥长账龄每日结论”任务**，ID为 `automation`。本机配置文件为：

```text
C:\Users\user\.codex\automations\automation\automation.toml
```

这不是GitHub Actions定时配置。不要通过修改 `Mx.version.json`、README或配置副本来尝试改变取数时间。

## 4. 每日17点如何更新

```text
本机Codex每日17:00启动（Asia/Shanghai）
  → 读取定版规则，查询最新完整数据日
  → 检查业务/个人范围、金额守恒、目标、历史与字体
  → 追加新数据日结论，修订另行留档
  → 生成本地主HTML
  → 打包Mx.html与Mx.version.json
  → Git提交main，仅更新这两个文件
  → GitHub Pages构建发布
  → 读取线上文件并核验
  → 观远固定外链显示新版
```

| 时间点 | 当前含义 | 在哪里调整 |
| --- | --- | --- |
| 北京时间17:00 | **开始取数**，不是承诺已完成发布 | 修改原有Codex任务，保留 `Asia/Shanghai` 时区 |
| 取数与核验完成后 | 自动推送，等待Pages发布，再做线上核验 | 本机发布流程 |
| 页面可见时每5分钟、重新切回可见时 | 检查版本标记；新版本才刷新 | `pages_refresh.js`，打包到 `Mx.html` |

修改时间可直接在Codex要求：“将现有‘墨西哥长账龄每日结论’任务改为北京时间每天XX:XX，不另建重复任务。”如果要求17点前已经可见，需要按实测耗时提前取数，并给Pages发布和缓存预留时间。

运行条件：本机开机联网、Codex运行、公司查询认证和Git认证有效。命令行推送不要求Chrome前台；查询认证过期而需要本人验证时，任务会受阻。**电脑关机后旧网页仍可访问，但本机不能产生新数据。**目前没有配置独立服务器取数服务，也没有在此公开仓库配置每日17点的取数工作流。

没有新的完整数据时，不伪造数据日或新增当天结论；已有同日目标/范围修订可以重新发布。失败保留上一成功网页。当前月为2026年11月，跨月先确认新目标和配置。

## 5. 观远一次性接入

1. 先打开 [墨西哥网页](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html)，确认能直接显示报表。
2. 打开已有观远监控仪表板，点击右上角“编辑”。
3. 点击“新建卡片”→“外链”，填写卡片名称。
4. 外链填写：`https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html`。
5. 保存卡片，拉宽到整行，调整高度；然后点击父仪表板“发布”。
6. 从观远正式页面检查数据日、金额、筛选和三个页签，与独立网页一致后验收。
7. 先保留旧自定义图表作为回退；新外链正常后再决定将旧卡片移入卡片池。

后续网址保持固定，不用每天替换HTML/CSS/JavaScript或重新发布仪表板。新版检查只刷新展示，不执行SQL。浏览器后台标签页可能被限频；切回页面会再检查，也可手动刷新。

观远接入由用户自行操作，本文不把“网页已发布”写成“观远已接入成功”。观远筛选和权限不会自动传给外部HTML，HTML内部筛选继续由页面自己处理。

## 6. 自己复刻和手工补发

### 6.1 只复刻网页展示

1. 取得同一批 `Mx.html` 和 `Mx.version.json`，保持相对目录和文件名一致。
2. 放入有权维护、且允许相同公开范围的仓库发布目录，启用GitHub Pages。
3. 等待Pages部署成功，打开对应的 `github.io/仓库名/Mx.html` 地址。
4. 按上一节把这个网址填入观远外链卡片。

无需安装Python即可展示已有快照。仅克隆本仓库可以复刻展示，不能自动获得数仓权限或完整取数环境。

### 6.2 在当前维护机手工补发已有主HTML

前提：主HTML已用真实数据刷新并核验，定版门控已批准。下面命令只负责打包、发布和核验，**不会重新查询数据**。

在PowerShell中执行；使用当前维护机已验证的Python路径：

```powershell
Set-Location 'C:\Users\user\Documents\ChatGPT\海外5过长账龄'
$mxPython = 'C:\Program Files\WindowsApps\OpenAI.CodexPrimaryRuntime.v26-1112-611-0_26.1112.611.0_x64__3k8sg7r9htsxt\dependencies\python\python.exe'
& $mxPython '.\work\mx_git_deploy\publish_pages.py' --publish
# 上一条成功后，等待同一次Pages部署，再核验：
& $mxPython '.\work\mx_git_deploy\verify_pages.py'
```

若核验返回尚未发布，查看本次Pages构建并稍后重试**核验命令**，不要为了等待重复推送。应用升级后Python路径可能变化，应换为已安装并验证的Python；Git路径可通过进程环境变量 `MX_MONITOR_GIT` 指定。

也可以在Codex要求：“按本README把当前已核墨西哥主HTML推送到GitHub Pages，并完成线上读回核验。”

### 6.3 复刻自动取数到另一台机器

需要从维护机取得受控的完整 `work/mx_monitor_20261115/`、`work/mx_git_deploy/`、相关模板、目标配置、历史记录、字体与核验依赖；只复制某一个Python脚本不够。本机打包文档还使用 `work/mx_guanyuan_native/.deps` 中的字体处理依赖。

在目标机配置Python、Git、必要的Node/页面核验工具、真实KaiTi字体和公司查询工具，重新完成公司只读认证与Git授权。当前打包字体依赖为 `fonttools==4.68.0`、`brotli==1.2.1`；核验脚本仍须按实际环境适配。不要复制个人Cookie或把凭据写入仓库。

先手动跑通真实取数→守恒与历史检查→主HTML→Git推送→线上核验，再建立一个17点任务。迁移到服务器还需调整Windows路径、字体和无人值守认证，不能把本机脚本原样上传就当作服务器服务。验收后保留一个生产发布者，避免新旧机器同时写历史或发布。

## 7. JSON、成功判断与回退

`Mx.version.json` 的字段含义：

| 字段 | 含义 |
| --- | --- |
| `version` | 输入完整主HTML的SHA256指纹；不是Token或数据库连接信息 |
| `data_through` | 本次业务数据真实截止日 |
| `generated_at_shanghai` | 打包时间，带时区；不等于数据截止日或取数完成时间 |
| `report` | 对应网页文件名，当前为 `Mx.html` |

HTML里的脚本读取JSON并比较版本，版本变化才刷新网页。JSON本身不执行任何任务。**不要只改JSON里的日期或版本号冒充刷新；两个文件必须来自同一次打包并一起提交。**

一次更新完成的判断：真实取数和业务核验通过；Git只改预期文件；Pages部署成功；线上JSON的版本和数据日匹配；线上HTML与**实际Git blob**摘要一致。Windows可能将工作文件CRLF规范为Git中的LF，因此核验以提交对象为准，不通过放宽金额或数据检查来处理换行。

| 问题 | 处理 |
| --- | --- |
| 显示“未定版，发布已拦截” | 先确认最终版本并登记审批，再启用发布；公开授权不能代替定版确认 |
| Git推送成功，但网页仍旧 | 查本次Pages部署；稍后重试 `verify_pages.py`，核对版本而非只看生成时间 |
| 网页已新，观远仍旧 | 确认外链是 `github.io/.../Mx.html`；切回页面或刷新，检查是否仍显示旧自定义图表 |
| 出现OpenAI登录页 | 核对是否误用了旧 `chatgpt.site` 地址；本方案使用GitHub Pages外链 |
| 查询或Git认证过期 | 在批准工具中完成正常登录，再恢复原任务；不在聊天中提供Token或Cookie |
| Git出现他人新提交 | 重新获取main并保留他人文件后提交；不强推、不回退整个仓库 |
| 无新数据或校验失败 | 保留旧网页及其真实数据日，报告失败阶段，不以改日期替代刷新 |

回退时定位最近一次成功的墨西哥发布记录，恢复**同一批** `Mx.html` 和 `Mx.version.json`，提交新的恢复版本并重新核验。只处理墨西哥文件，不撤销同事其他国家的提交。自动发布脚本拒绝用更早数据覆盖线上；紧急历史回退应作为单独维护操作明确确认并记录。

## 8. 定版、文档与维护纪律

- 改业务口径、目标或模板：先在候选/验收分支检查，确认版本后再改发布基线；日常数据刷新沿用批准流程。
- 每日结论逐日追加，源修订单独记录；昨日跟进有连续性，历史原记录不被刷新覆盖。
- 监控HTML嵌入真实KaiTi，标题、正文、数字、表格、控件统一楷体。GitHub自身的README字体由平台控制。
- 发布机制、路径、时间或观远入口变更后同步更新本README；业务核对明细继续留在独立说明和维护记录里。
- 当前已验证网页发布、完整文件读回及页面展示；新流程的首次完整17点定时取数运行、用户侧观远外链接入仍需实际运行/操作验收。

参考：[GitHub Pages创建与发布](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)、[Codex本地定时任务](https://learn.chatgpt.com/docs/automations)、[观远外链卡片](https://docs.guandata.com/?a=index&aid=656371261059891200&id=1&m=Article)。
