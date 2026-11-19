# 墨西哥长账龄监控：复刻与维护说明

本文件统一维护于 `README-MX.md`。记录更新时间：2026-11-19；原仓库 `README.md` 保留。

## 当前定版

业务版本 `MX_EVENT_QUEUE_LS_MERGED_V12`，日报修订 `WABA_DAILY_CONCLUSION_R3_GT180_20261119`，数据截至2026-11-18。

本次落实已确认的180天以上真实分案补全：M3增加25,418.50 MXN，并同步催员及债务人去重案件量。主实收4,017,615.89 MXN（1,462,866.26 CNY），回款债务人1,244。已有核心周期的5,000及740 MXN继续按核心窗口，不额外补计。所有目标及原账龄率分子/对应本金保持不变。

旧86条日报和34条预估保留，追加18日修订后87条/35条，预估参数未改。旧日期保留原版本。日报包括WABA，不把历史覆盖为最新结论。

业务发布提交 `e0afd24c9b9acb5372591d7022dc204c2a004ec0`，正式Pages的HTML和版本JSON已读回核验；本次未目视观远。此为手动修订，不代表17点无人值守全链路已验收。

## 文件作用

| 文件 | 作用 |
| --- | --- |
| `Mx.html` | 完整监控、内嵌数据、真实KaiTi、筛选/MTD/三个页签和新版检查脚本 |
| `Mx.version.json` | 页面检查新版的标记；不查询、不计算、不保存定时任务 |
| `README-MX.md` | 本墨西哥维护步骤和版本记录 |
| `README.md`、其他国家HTML | 原有总说明及其他国家资料，墨西哥维护不改 |

固定网页：[墨西哥监控](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html)；版本标记：[Mx.version.json](https://maxyu-0302.github.io/overseas-collection-monitor/Mx.version.json)。文件名大小写必须一致。

用户已授权完整监控公开，含催员及业绩。源码、SQL、查询回执和身份键映射仍保存在本地完整包，不随展示仓库上传。

## 原定版整套资料与修订档案

维护机根目录：`C:/Users/user/Documents/ChatGPT/海外5过长账龄/`。

统一入口为原定版目录 `outputs/墨西哥监控_展示定稿_p3代码同步_20261117/最新定版入口.html`。同目录 `修订记录/20261119_180天以上补入/` 为本次完整归档，包含以下内容；同级保留完整ZIP及清单。旧定版和原ZIP保留。

| 离线文件/目录 | 用途 |
| --- | --- |
| `墨西哥长账龄监控_最终版.html` | 日常监控：目标与实收、催员业绩、每日结论，默认及重置CNY |
| `逐笔归属与核心代码说明.html` | 最新口径、金额前后、分案与催员证明、两例周期、实际案例SQL |
| `本地复刻说明.html` | 离线复算、下一日取数、构建、核验、发布和观远操作 |
| `data.json`、每日结论/预估/参数JSON | 本批完整加工结果及连续历史 |
| `代码/` | SQL、完整结果、加工/页面模板和实际核验脚本 |
| `核对数据/`、`案例核对SQL_R2/` | 原对照及核心周期证据，均注明历史日期 |
| `本次调整全套留档/` | 调整前后说明、查询回执、金额/界面核验、实际任务读回、发布工具与状态 |
| `定版发布回执.json`、`核验结果.json` | 本批发布与验收证据，不能代替下一批核验 |
| `全套文件清单.json` | 归档文件路径、大小与SHA256，用于复刻完整性核对 |

当前实际运行来源见 `work/mx_git_deploy/last_business_update.json`，最新成功包为 `outputs/墨西哥监控_181补入修订_20261119/`。修订归档是留存副本，下一日从最后成功包复制加工。

本地发布工具 `work/mx_git_deploy/` 中：`release_approval.json`记录批准版本及发布门禁，`github_pages_authorization.json`记录公开范围；`prepare_pages_candidate.py`同批打包HTML和版本JSON，`publish_pages.py`安全推送两文件，`verify_pages.py`正式读回；`pages_latest.json`、`pages_publication.json`及`pages_runs/`保存实际状态。`pages_refresh.js`在打包时内联，不从README执行。文档专用工具`publish_readme.py`只更新README-MX.md。

## 本次180天以上补全规则

1. 当前核心分案覆盖至180天。超过180天且核心无周期的真实分案，不能仅因缺核心行排除现金。
2. 按现金 `source_id → 回收batch → mission_log → 实际业务组/催员` 核实归属，核对原始和财务四类现金，排除DS及资格不符。
3. 排除核心、HPT、M7、回捞重叠后，将合格金额从pending移到events，同步主实收、催员和债务人去重案件量。重复构建不双加。
4. 已有核心周期的交易按核心统计窗口，5,000和740本次未补。后续用新核心证据复查，不统一移日或按财务组强行覆盖。
5. `config.include_verified_gt180_cash=true`。专项缺对应本金时不扩大账龄实收率分子。M账龄归属按确认规则，不出现跨账龄虚构组；M4-HPT只有一个目标。

关键文件：`生成180以上归属核验SQL.py`生成本批查询；`补入180以上实收.py`核重及准入；`日更冻结现金核验.py`重建底账并调用补入；`assemble.py`同步个人、主实收与结论；`build_paid_debtor_counts.py`核债务人去重与现金守恒。实际新增归属查询470274，51行，success/NOT_LIMITED。

原11/14的p3截图复现M2为1,724,675.70 MXN，与保存观远差−2,348.19；原最终口径M2为1,738,373.96，与观远差+11,350.07。两者为历史对照，不是本次新日总实收。逐项差异和统计口径留在线下说明。

## 每天17点真实更新

现有Codex任务“墨西哥长账龄每日结论”，ID `automation`，北京时间17:00开始；实际任务位置 `C:/Users/user/.codex/automations/automation/automation.toml`。通过Codex应用修改真实任务，不直接编辑TOML，不重复创建。`automation_pages_configuration.json`只是实际任务的本地副本。

本机取数 → 加工与核验 → 主HTML → 同批Mx.html/JSON → GitHub Pages → 正式读回 → 观远固定外链。

当前依赖维护机开机联网、Codex运行及有效认证；不是服务器取数任务。17点是开始时间。锁屏不必然停止后台，但登录等交互可能受阻；关机、休眠或应用未运行时不能完成本地更新。旧网页能访问不代表源数已更新。11月目标不自动沿用到下月。

1. 复制最后成功包到新批次，保留日报/预估/参数与匿名键。核最新完整业务日，再改config的latest、右开end及updated；不只改日期。
2. 用获准墨西哥只读查询刷新核心ACTUAL、确认non-actual、事件桥、个人/在职、回捞、冻结、181+财务及本金。按回款发生时队列归组，LS现金及目标只合并一次到SD-agent。事件桥读取原资格事实，不能将已转组data.json再转一次。
3. 补齐paid_core两日分片、paid_m7_finance和paid_recall_identity。按当前筛选累计净实收为正的债务人去重，各组和合计分别去重，不能加总组件件数。
4. 按当批frozen_source_items扩展相关SQL资产名单，运行减免证明、核心周期证明及180以上真实分案证明的生成器，执行生成SQL后再加工。
5. 单并发查询，保存SQL、完整结果、query_id和回执；要求success/NOT_LIMITED、明细少于5,000行。已有提交按原ID恢复；旧提交未知减免查询RkRKaefC4EJ不重提、不当作成功。认证需本人时保留旧网页并说明卡点。
6. 核回捞及跨日现金，运行日更冻结现金核验.py、build_history_compare.py、assemble.py、build_p3_comparison.py、重建本地HTML.py。不要用旧build_final_delivery.py覆盖新UI。
7. 检查金额守恒、目标、本金、专项覆盖、个人资格及去重，检查三页签、筛选、MTD、导出、低于70%高亮及真实嵌入KaiTi。默认人民币；non-actual包含常规实收，不单列、不双加。
8. 每日结论简短写整体/M2/61+、M2/M3/M4人催、AI供应商和WABA的倒推目标缺口、达成、近3日改善，并闭环昨日名单；点名低于70%且无改善催员。新日及同日修订均留旧档，预估参数连续保存。

## 离线复算与发布命令

在完整包副本中执行，仅重跑已保存输入，不取新数或发布：

```powershell
python .\代码\日更冻结现金核验.py
python .\代码\复算快照.py
node .\代码\验证WABA结论.cjs
node .\代码\验证回款案件量与展示.cjs
```

发布工具位于本地 `work/mx_git_deploy/`，离线包也附副本。换机须恢复工作区结构并配置Python、Git、公司网络/查询权限；字体重新制作需真实simkai.ttf和fonttools/brotli。Git可用MX_MONITOR_GIT指定实际路径。不要复制或上传Cookie、Token。

本批真实刷新及核验通过后，在实际维护工作区执行，显式指定source：

```powershell
python .\work\mx_git_deploy\publish_pages.py --source '本批主HTML的绝对路径' --publish
python .\work\mx_git_deploy\verify_pages.py
```

仅提交 `Mx.html`、`Mx.version.json`；正常推送，不强推，不覆盖其他国家和README。部署未完成时重试verify，不反复推送。版本JSON和HTML须同批提交。以源日、版本和实际Git文件摘要的正式读回为成功标准，不把本地生成或Git提交当作部署成功。

## 观远接入与刷新

1. 独立打开固定Pages网址，确认无需ChatGPT登录并核数据日。
2. 观远已有仪表板进入编辑，新建“外链”卡片，名称墨西哥长账龄监控。
3. 填入 `https://maxyu-0302.github.io/overseas-collection-monitor/Mx.html`，保存，宽度整行并调整高度，保存并发布父仪表板。
4. 在正式查看页核对三页签、日期、币种和金额与独立网页一致，另记观远目视验收。

日常不再粘贴HTML/CSS/JavaScript三栏，不改固定地址，不需每天重发父仪表板。内嵌脚本在页面可见时每5分钟及恢复可见时检查JSON，发现新版后刷新，也可手动刷新。观远筛选不会自动传入HTML，使用网页内部筛选。

GitHub Pages直接提供静态HTML；旧chatgpt.site曾跳转OpenAI登录且嵌入失败，不再作为正式外链。Git仓库地址和blob预览都不是报表网址。

## 每次变更全套留档

固定记录：`work/mx_git_deploy/CHANGELOG-MX.md` 和 `change_records/<变更编号>.json`。业务修正编号 `MX-20261119-GT180-CORRECTION-R3`；本次全套整理编号 `MX-20261119-GT180-DOCUMENTATION-R1`。

每次保存用户要求、前后源码/SQL/结果、实际变化的文件清单与SHA、业务影响与核验、历史修订、真实任务更新读回、Git提交/Pages读回及观远观察状态。复制未变文件不算代码修改。本次业务修正代码目录实际改24个（19修改、5新增），线上报表只改2文件；本次资料整理不再修改业务代码或实收。

归档更新两份线下说明、维护交接及本README-MX，统一放回原定版整套资料的修订记录。原基线及旧ZIP保留。源码、SQL、身份键和完整包不上传公开仓库；文档维护仅更新README-MX.md，不改README.md。

故障时保留最近成功网页：查询截断/核验失败先修复，线上旧版检查本次Pages和JSON，观远旧版检查固定外链与缓存，Git冲突先获取新main并保留他人文件。回退使用同一批配套HTML/JSON，正常提交恢复版本，不回退整个仓库。
