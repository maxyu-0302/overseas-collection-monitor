# 墨西哥长账龄监控：复刻与维护说明

本文件为墨西哥专用维护说明，统一保存在 `README-MX.md`；仓库原 `README.md` 保持原样。

海外长账龄监控静态网页仓库。**取数和加工在维护机执行 → 将生成的HTML推送到GitHub → GitHub Pages发布 → 观远用固定外链展示。**

本文统一记录文件用途、墨西哥最终版本、每日17点流程、复刻步骤和观远接入。其他国家的取数口径由各自维护者管理。

## 1. 先看当前状态

- 用户2026-11-17最后确认的定版为 **`MX_EVENT_QUEUE_LS_MERGED_V12`**，完整包名为 `墨西哥监控_展示定稿_p3代码同步_完整包_20261117.zip`。
- 定版主数据截至 **2026-11-15**；与保存的观远数据比较仅到 **2026-11-14**。两种日期不能混用。
- **2026-11-17已手动发布用户确认的V12到正式Pages网址，主数据截至11月15日，正式HTML及版本JSON已读回核验一致。** 报表提交为 `f17a342d071a66b328eaad23e484eea85b46152f`。仓库原README.md保持原文，墨西哥说明单独维护于README-MX.md。
- 原有每天17:00的Codex本机任务已改为引用V12。**V12首次“真实新日取数→发布→线上核验”的定时完整运行尚未验收。**有定时任务不代表服务器已部署。
- 观远外链由用户自行配置；尚未记录用户侧正式验收。不要把“Git已推送”写成“网页和观远全部更新成功”。

## 2. 仓库中的文件各做什么

| 文件 | 作用 | 网页入口 |
| --- | --- | --- |
| `Id.html` | 印尼完整监控快照 | [印尼监控](https://maxyu-0302.github.io/overseas-collection-monitor/Id.html) |
| `Ph.html` | 菲律宾完整监控快照 | [菲律宾监控](https://maxyu-0302.github.io/overseas-collection-monitor/Ph.html) |
| `Th.html` | 泰国完整监控快照 | [泰国监控](https://maxyu-0302.github.io/overseas-collection-monitor/Th.html) |
| `Mx.html` | 墨西哥完整网页：结构、内嵌数据、真实楷体、样式、筛选、图表和新版检查脚本 | [墨西哥监控](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html) |
| `Mx.version.json` | 告诉已打开的墨西哥页面是否有新版；不取数、不计算目标、不保存定时任务 | [墨西哥版本标记](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.version.json) |
| `README.md` | 仓库原有总说明，墨西哥维护不修改它 | 仓库入口 |
| `README-MX.md` | 本墨西哥维护说明；记录规则和步骤，不执行更新 | 当前文档 |

文件名区分大小写。墨西哥固定入口为 `Mx.html`，观远填写 `github.io` 网页地址。不要填GitHub仓库页面、`blob/main`文件预览或旧`chatgpt.site`地址。

仓库及Pages网页目前公开。用户已明确允许完整墨西哥监控公开，保留催员姓名、个人业绩及每日历史。独立核对资料、完整源码包、SQL、查询回执和凭据不随日常发布上传。外部网页直接访问不继承观远权限。

## 3. 哪一份是最终版

最终版保留已确认的non-actual、业务组账龄及补入口径，并按回款发生时承接队列归组；LS现金及目标合并到SD-agent。M4-HPT只有一个目标，不出现虚构的跨账龄分组。

下面金额**都是11月14日、MXN**，差额定义为“本版－观远”：

| 用途 | M2合计 | 与观远差额 |
| --- | ---: | ---: |
| p3截图同口径复现，仅作对照 | 1,724,675.70 | −2,348.19 |
| 用户最后确认的最终监控口径 | **1,738,373.96** | **+11,350.07** |

不能把p3复现值当作最终监控的验收值。逐项差异放在独立核心说明，不加入日常监控正文。

V12主HTML基线SHA256：

```text
8fad6e0d8110bf5b4dc2d39a1792b1a8221f956dc4b68c9fc03ef76133dc1604
```

这是**本地主HTML原文件**摘要；加入新版检查、Git换行规范化后，线上完整HTML摘要会不同，须分别核验。上游数据字典参考提交为 `41dd4f4ca9b83f017216ab859e051d687fd09fd7`，不是此展示仓库的发布提交。

定版个人日目标以包内 `config.json` 为准，计算保留精度：M2为3477.075766 MXN、M3为2468.337 MXN、M4-HPT为1455.416529 MXN；显示可以四舍五入，不能倒用旧目标。日目标乘30得到全月个人目标，序时按实际天数计算。

## 4. 三份HTML、完整包和代码在哪里

**本仓库只保存展示文件。本节文件在维护机/交接包中，不会随克隆本仓库自动下载。**

当前维护机根目录：

```text
C:\Users\user\Documents\ChatGPT\海外5过长账龄
```

最终交付目录（下文简称“定版目录”）：

```text
outputs/墨西哥监控_展示定稿_p3代码同步_20261117/
```

| 定版目录内文件 | 用途 |
| --- | --- |
| `墨西哥长账龄监控_最终版.html` | 日常阅读：目标与实收、催员业绩、每日结论三页签；独立HTML、内嵌真实KaiTi |
| `逐笔归属与核心代码说明.html` | 数据表、字段、关联、加工规则、p3复现和最终版与观远差异；线下核对使用 |
| `本地复刻说明.html` | 详细离线复算、真实刷新、输入输出及验收标准；其中旧原生三栏接入是历史方案，当前日常发布按本README-MX.md的Pages外链方案 |
| `data.json` | 本批完整加工结果，已内嵌于主HTML；不是数仓连接配置 |
| `每日结论留存.json` | 按数据日及修订版本留存结论；新日追加，同日修订留档 |
| `每日预估留存.json`、`预估参数版本.json` | 每日预估及参数历史；不能把最新参数静默覆盖旧记录 |
| `核对数据/` | 业务组、催员、p3对照和最终版差异等线下核对表 |
| `核验结果.json`、`版本与核验来源.json` | 本批验收结果、来源与哈希；是历史证据，不是下一日自动通过的凭证 |
| `代码/` | 可复算本批快照的脚本、SQL、完整结果、模板及字典 |
| `附件SQL/`、`验收截图/` | 专项核验材料及本批界面验收证据 |

完整ZIP在：

```text
outputs/墨西哥监控_展示定稿_p3代码同步_完整包_20261117.zip
```

本批留存51条日报修订、15条预估记录，原36条日报保留。包内已记录独立目录离线复算逐字节一致；这证明本批可复算，不代表已重新查询下一日数据。

### 4.1 关键加工程序

这些文件在定版目录的 `代码/`，开发运行目录为 `work/mx_monitor_p3_synced_20261117_v12/`：

| 文件 | 作用 |
| --- | --- |
| `config.json` | latest、end、updated、版本、已确认日目标、LS转SD-agent规则 |
| `confirmed_baseline.json` | 冻结目标和历史基线；不动态读取别的验收分支 |
| `core_facts_final.sql`及结果 | 原ACTUAL资格及确认non-actual核心事实；保留原始归组供事件桥核验 |
| `p3_event_sources/`、`event_queue_sync.py` | 逐周期核对原事实，按回款时队列转移现金；本金和件数不随事件重复 |
| `assemble.py` | 合并核心、已核回捞、冻结及181+财务数据，统一LS管理归属，生成data.json；调用日报及预估加工 |
| `build_history_compare.py` | 历史同期加工；历史冻结不变时复用已确认快照 |
| `build_daily_reports.py` | 生成整体、账龄、人催、AI及跟进名单的逐日结论 |
| `build_forecasts.py`、`forecast_config.json` | 每日预估、CPS及参数版本处理 |
| `build_p3_comparison.py` | 对保存的11月14日观远快照复现p3并列最终差异；不能当作新日观远对账 |
| `build_final_delivery.py` | 输出三份HTML及交接文件；重新生成文档时需要包外字体处理依赖和真实字体 |
| `ui.html`、`dashboard.css`、`compact.js` | 定稿展示与交互；`ui.html`包含实际页面运行代码，只改独立compact.js不等于已重建页面 |
| `复算快照.py` | 不联网，按已保存输入重跑加工并重建主HTML |
| `重建本地HTML.py`、`样式.css` | 仅由现有data.json重建主HTML；样式含已嵌入字体 |

### 4.2 发布工具和定时任务

以下均在维护机，不在公开仓库运行：

| 文件 | 作用 |
| --- | --- |
| `work/mx_git_deploy/release_approval.json` | 指定批准版本、主HTML路径及基线摘要；现已绑定V12 |
| 同目录 `github_pages_authorization.json` | 完整监控公开授权范围；不保存凭据，也不代替版本验收 |
| 同目录 `prepare_pages_candidate.py` | 检查版本、日期、字体，生成配套Mx.html及Mx.version.json；默认读取批准基线，`--source`指定已核新批次 |
| 同目录 `pages_refresh.js` | 每5分钟及恢复可见时检查新版；打包时内联到Mx.html，不在README里执行 |
| 同目录 `publish_pages.py` | 打包后仅提交两个墨西哥文件；默认不推送，`--publish`才写远程；保留其他国家文件、原README.md及README-MX.md |
| 同目录 `verify_pages.py` | 读取正式网页和JSON，验证版本、日期、实际Git文件摘要；不负责取数 |
| 同目录 `pages_latest.json`、`pages_publication.json`、`pages_runs/` | 当前尝试、最近成功线上核验及每次发布记录 |
| 同目录 `automation_pages_configuration.json` | 真实定时配置的本地副本；修改副本不改变定时器 |
| 同目录 `README-MX.repo.md`、`publish_readme.py`、`readme_mx_publication.json` | 墨西哥说明维护源、仅改README-MX.md的发布工具及读回回执；与日常报表发布分开 |
| `outputs/墨西哥GitHubPages待发布包_20261117/网站文件_仅这两个文件可提交/` | 打包结果，只上传其中Mx.html和Mx.version.json；其他交接资料留线下 |
| `work/mx_monitor_20261115/revision/DAILY_UPDATE.md` | 历史维护记录，已追加V12交接说明；旧revision生成流程不再作为本次最终版输入 |
| `work/mx_guanyuan_native/`、`outputs/墨西哥监控自助更新/` | 旧观远自定义图表三栏转换工具；Pages外链接入后不用每天粘贴三栏 |

真实定时任务为Codex **“墨西哥长账龄每日结论”**，ID `automation`。本机配置位置：

```text
C:\Users\user\.codex\automations\automation\automation.toml
```

它不是GitHub Actions。README、JSON版本标记、配置副本都不会自行启动取数。

## 5. 每日17点的流程和卡点

```text
本机Codex每日17:00开始（Asia/Shanghai）
 → 查询真实最新完整业务日，保存SQL、完整结果和原回执
 → 按V12加工，追加日报/预估并保留旧修订
 → 核验金额、目标、范围、去重、历史、字体与交互
 → 生成本批主HTML并指定为--source
 → 同批打包Mx.html及Mx.version.json
 → Git正常提交main，保留其他文件
 → 等待GitHub Pages部署
 → 读回正式网页及JSON，核验成功才记为网页更新完成
 → 已接入的观远固定外链检查版本并刷新
```

| 时间/配置 | 当前含义 | 修改位置 |
| --- | --- | --- |
| 北京时间17:00 | 开始取数；不是保证17点已发布完毕 | 修改原Codex任务，不新建重复任务 |
| 核验完成后 | 推送并等待Pages发布 | 发布流程 |
| 可见时每5分钟、重新切回页面时 | 比较版本；不同才刷新 | pages_refresh.js，修改后需重新打包发布 |
| latest / end / updated | 真实数据日 / 查询右开上界 / 本次加工日 | 新批次config.json及对应SQL；不能只改config而不查新数据 |

可在Codex要求：“将现有墨西哥长账龄每日结论改为北京时间每天XX:XX，保留原任务。”若要求17点前可见，要根据实际耗时提前启动并预留部署时间。

当前依赖**维护机开机联网、Codex运行、查询和Git认证有效**。锁屏不等于后台进程停止，但认证弹窗、交互登录或浏览器步骤可能受阻；休眠、关机或应用未运行不能完成本地刷新。旧Pages网页仍可访问，不代表有新数据。查询失败、截断、认证过期或校验失败时保留上一成功网页，说明具体失败阶段。

目前没有常驻服务器取数服务、无人值守服务认证或本仓库每日17点取数工作流。迁移到服务器需IT提供常驻执行环境、只读服务认证、公司网络、发布身份和故障接收方式；跑通真实全流程、验证个人电脑关机后仍更新，再停用本机生产发布。当前只维护2026年11月，跨月须先确认新目标。

## 6. 自己复刻、更新与发布

### 6.1 离线复算已保存的定版

1. 从维护机取得上述完整ZIP，完整解压，保留目录结构。
2. 双击三份HTML即可阅读；无需数仓登录。
3. 安装Python 3，在解压后的“代码”目录运行：

```powershell
python .\复算快照.py
```

它重跑已保存输入并重建主HTML，**不取新数、不发布**。仅根据已有data.json改展示时，可运行：

```powershell
python .\重建本地HTML.py
```

改页面要修改实际ui.html及样式来源，再重建并核验；直接改输出HTML会在下次生成时丢失。只有克隆展示仓库，无法复刻取数环境。

### 6.2 真实刷新到下一日

1. 复制已确认运行目录为新批次，保留上次完整HTML、数据、结论、预估及参数；不要改写归档基线。
2. 通过获准只读查询确认最新完整业务日；更新新批次config的latest、end和updated，并调整对应SQL日期上界。
3. 同步刷新原核心事实和p3事件桥，再刷新催员、在职、回捞、冻结、181+财务及本金；保留原查询ID和完整结果，要求success且NOT_LIMITED。不能只查ACTUAL而漏掉确认补充。
4. 更新派生专项台账并逐笔排除重复覆盖；不把旧例外名单直接套给新交易。使用包内说明核实输入依赖。当前没有已验收的一键服务器取数命令。
5. 顺序运行build_history_compare.py、assemble.py、build_p3_comparison.py、build_final_delivery.py；历史源未变可沿用已核历史。保存的观远对照仍标原日期，不能写成新日已对账。
6. 检查各数据日现金守恒、事件与核心对应、分案本金和件数不重复、四目标合计、181+、个人目标、专项去重及历史保留；再检查三个页签、筛选、币种、导出和真实KaiTi。
7. 只发布本批核验通过的主HTML。新日结论须简短列缺口与达成、昨日跟进、近3日趋势及低于70%且无改善的人/供应商；同日修订保留旧档。源日未前进不伪造新日结论。

**事件桥必须读取原资格事实，不能把已转过现金归组的data.json再次当作原事实输入。**同一笔冻结/回捞已包含于主实收时不能再加一次。

### 6.3 手动打包、推送和验证

当前维护机已验证的Python路径如下；应用升级后用实际安装并验证的路径替换。发布工具还需Git、字体处理依赖及现有正常Git授权；Python命令只打包/发布，**不会查询新数据**。

```powershell
Set-Location 'C:\Users\user\Documents\ChatGPT\海外5过长账龄'
$mxPython = 'C:\Program Files\WindowsApps\OpenAI.CodexPrimaryRuntime.v26-1112-611-0_26.1112.611.0_x64__3k8sg7r9htsxt\dependencies\python\python.exe'
# 首次发布当前归档定版：
& $mxPython '.\work\mx_git_deploy\prepare_pages_candidate.py'
# 检查输出包的数据日、金额与页面后，实际推送：
& $mxPython '.\work\mx_git_deploy\publish_pages.py' --publish
# 等同一次Pages部署完成，再读回核验：
& $mxPython '.\work\mx_git_deploy\verify_pages.py'
```

以后发布新批次时，显式指定已经完成取数及核验的主HTML路径，避免重复发布旧基线：

```powershell
# 把路径替换成真实存在的本批主HTML：
$mxNewReport = 'C:\实际新批次目录\墨西哥长账龄监控_最终版.html'
& $mxPython '.\work\mx_git_deploy\publish_pages.py' --source $mxNewReport --publish
& $mxPython '.\work\mx_git_deploy\verify_pages.py'
```

默认不带`--publish`仅准备Git提交，不推送；仍会生成本地包并读取远程。若线上尚未完成部署，稍后重试**核验命令**，不为等待反复推送。

不用命令行也可手工上传：先用prepare生成同批两个文件，在GitHub仓库main的“Add file → Upload files”同时上传Mx.html和Mx.version.json；不要整包上传。遵守仓库当前保护/审阅规则，保留其他国家、原README.md及README-MX.md。进入Actions确认本次Pages部署成功，再打开固定网址及版本JSON核对。手工上传不会自动生成本机发布回执，应另记提交号、数据日、来源摘要和验收结果。

### 6.4 换一台机器维护

取得完整V12交接包和完整`work/mx_git_deploy/`发布工具、保留历史及所引用依赖。离线复算使用内嵌字体；重新生成三份文档/打包手册还用到真实`C:/Windows/Fonts/simkai.ttf`、`work/mx_guanyuan_native/.deps`中的fonttools与brotli。现有环境版本为fonttools 4.68.0、brotli 1.2.1。另配置Python、Git、必要的Node及页面核验工具、公司查询工具和正常授权；本地绝对路径、代理端口需按目标环境调整。

首次先手动跑通真实取数、加工、页面核验、推送及线上读回，再建立17点任务。保留一个生产发布者，避免两台机器同时写历史或互相覆盖。不要复制个人Cookie或把认证信息提交到此仓库。

## 7. 观远一次性接入步骤

1. 独立打开[墨西哥Pages网页](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html)，确认直接显示报表，并检查版本与数据日。
2. 打开已有“墨西哥长账龄每日监控”仪表板，点击“编辑”。
3. 新建卡片 → **外链**，填写名称“墨西哥长账龄监控”。
4. 填入固定网址：`https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html`。
5. 保存卡片，将宽度拉到整行、调整高度；保存后发布父仪表板。
6. 在正式查看页核对三个页签、筛选、币种、数据日和金额与独立网页一致，登记验收日期及版本。
7. 保留原自定义图表作回退，新外链验收后再决定是否移入卡片池。

后续日常更新只推送同名HTML与JSON，观远地址保持不变，**不用每天替换HTML/CSS/JavaScript三栏，也不用每天重新发布仪表板**。观远筛选不会自动传给HTML，使用HTML内部筛选。新窗口与后台标签可能受缓存和限频影响，切回可见会再检查，也可手动刷新。

原OpenAI外链曾进入ChatGPT登录页，登录后仍被嵌入限制阻挡；本方案使用GitHub Pages直出静态HTML，避免这条登录跳转。当前是否成功仍以观远实际验收为准。

## 8. JSON、新版检查与成功标准

| Mx.version.json字段 | 含义 |
| --- | --- |
| version | 输入完整主HTML的SHA256；不是Token，也不是SQL任务 |
| data_through | 真实业务数据截止日 |
| generated_at_shanghai | 打包时间；不等于数据截止日 |
| report | 关联的Mx.html文件名 |

Mx.html内脚本读取同目录JSON，版本变化才刷新，并尽量保留当前筛选。**JSON与HTML必须同批一起提交；只改JSON日期、README或本地HTML不会自动改变线上数据。**

完成标准：真实数据及业务核验通过；Git只改预期文件；Pages本次部署成功；线上JSON匹配版本/数据日；线上HTML匹配实际提交的Git blob。Windows换行可能规范化，以Git提交对象摘要验证，不放宽金额检查。观远另做一次接入验收。

## 9. 故障处理和回退

| 现象 | 检查与操作 |
| --- | --- |
| 网页仍是旧版 | 看本次提交和Pages部署；比对JSON版本/数据日，重试线上核验 |
| 网页新、观远旧 | 核对是否仍看旧自定义图表、外链是否为github.io/Mx.html；切回可见或刷新 |
| 显示OpenAI登录或拒绝连接 | 检查是否仍引用旧chatgpt.site；换为本README的Pages网址 |
| 基线摘要变化/版本不符 | 不绕过断言；归档基线保持原样，真实新批次用--source并按批准规则核验 |
| 原事实与事件桥不一致 | 两边同步刷新；排除把已归组结果重复输入，不跳过守恒断言 |
| 查询/认证失败或结果截断 | 保留旧网页；通过正常认证恢复原查询，确认完整结果后重跑 |
| Git遇到别人新提交 | 获取最新main、保留他人文件、重建本次提交；不强推 |
| 无新完整业务日 | 不造新日期；同日真实修订单独留档，必要时重新发布 |

回退只恢复最近成功的同一批Mx.html和Mx.version.json，再提交一个正常恢复版本并核验；不回退整个仓库、不撤销同事其他国家提交。发布工具会拒绝更早数据覆盖正式页，紧急历史回退需单独明确并记录。

## 10. 维护时需要同步什么

- 业务/目标/模板改动先做候选验收，再确认发布版本；日常数据刷新沿用批准规则。
- 修改取数时间要更新真实Codex任务；修改刷新检查要重新打包发布；修改墨西哥说明只更新README-MX.md，不修改原README.md。
- 每日结论、预估和参数连续留档，不覆盖旧记录；独立核对说明在线下保存。
- 主监控标题、正文、数字、表格、控件均用真实内嵌KaiTi。GitHub README字体由平台控制。
- 当前完成V12定版发布、正式HTML及版本读回核验和墨西哥维护说明；首次真实17点定时取数全链路、用户侧观远验收仍需分别登记。手动发布成功不等于下一次自动任务已验收。

参考：[GitHub Pages创建及发布](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)、[Codex本地定时任务](https://learn.chatgpt.com/docs/automations)、[观远外链卡片](https://docs.guandata.com/?a=index&aid=656371261059891200&id=1&m=Article)。
