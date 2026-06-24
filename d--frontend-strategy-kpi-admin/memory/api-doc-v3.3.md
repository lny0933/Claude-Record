---
name: api-doc-v3-3
description: Strategy KPI V3.3 API 接口文档摘要，后续需求以此为准（更新版，2026-06-02）
metadata: 
  node_type: memory
  type: reference
  originSessionId: 56c9c1a1-7251-4c87-a6a4-c9df3529a081
---

接口文档路径：`C:\Users\lny03\Downloads\V3.3-API-接口文档.md`
Apifox 导出：`C:\Users\lny03\Desktop\新建文件夹 (2)\strategy-kpi-3.3.apifox.json`（部分导出，仅含1个端点，见下）

## 核心变更（与旧文档差异）

### ID 类型全部改为 String
所有 ID 字段（teamId / actionId / kpiInfoId / id / ownerId / orgId / meetingId）均为 **String**，不再是 Long。

### R-437 KPI 附件（重要）
- **保存**：`processAttachment: [{ url, fileName, fileType, size }]`（Array）
- **列表 `/api/kpis/list` 新增两个字段**：
  - `processAttachmentFlag`：Integer，**0=无附件 1=有附件**（非流程KPI统一为0）
  - `processAttachmentFiles`：Array<AttachmentDto>（流程KPI有附件时有值）
- 判断是否显示回形针图标应用 `processAttachmentFlag === 1`，文件名从 `processAttachmentFiles[0].fileName` 取

### R-575 逾期提交列表
- `POST /api/lateSubmission/page` 新增请求字段 `bizType: Integer`（0=项目 1=KPI 2=举措，null=全部）

### R-571 进行中周期
- 新增 `dataType=4`（月度KPI专用，仅返回月度周期KPI）
- linkList 新增 `measurementCycle: Integer`（0=Annual 1=Semiannual 2=Quarter 3=Monthly）

### R-573 历史日志
- `POST /api/sys/operationLog/page`，`bizType` 参数修复（null 不再返回空）
- 支持 `bizType: project|kpi|initiative|cycle|objective|attachment|organization`

### R-574 邮件提醒（纯后端）
- 项目周期：截止前 **2天**（原3天）发送提醒；举措/KPI 不变（保持3天）

### R-456 行动项延期
- `POST /api/team/action/postpone`，请求字段：`actionId(String)` / `newTargetDate(DD/MM/YYYY)` / `reason(String可选)`
- `POST /api/team/action/postpone-history`，返回按时间倒序数组

### Committee KPI（R-446/R-458）
- `/api/committee-kpi/save|delete|detail|page|update-actual|breakdown`
- breakdown 返回4条（kpiType 1-4），含 `avgCompletion` 和 `count`

### 团队 KPI 三环图（R-458）
- `/api/team/kpi/breakdown`，返回 `{ teamKpis, individualKpis, adminKpis }`，每项含 `performance`

### 委员会仪表盘（R-448）
- `/api/dashboard/committee/overview`：总团队数 / 有KPI团队 / 平均完成率 / 团队快照
- `/api/dashboard/committee/team-scores`：按KPI类型分解（strategic/operational/process/enablerRate）
- `/api/dashboard/committee/mom-compliance`：会议数 / 出席率 / 行动项关闭率
- `/api/dashboard/committee/outstanding-actions`：逾期/即将到期行动项（urgency: overdue|due-soon）

### 组织层级（R-460）
- `POST /api/org/levels`，请求 `{}`，返回 `[{ level, name, nameAr }]`

### 错误码
- `71000005`：逾期提交防重复（R-570）
- `80100008`：已完成行动不可编辑/延期（R-455/456）

---

## Apifox 补充信息（来自 strategy-kpi-3.3.apifox.json）

> 该导出仅包含 1 个端点，其余 V3.3 端点未被导出（Apifox 选择性导出）。

### `POST /api/dashboard/statisticsCurrentDatePerformanceByType`（R-569）

**请求 Schema**（`PerformanceRequest`，所有字段可选）

| 字段 | 类型 | 说明 |
|---|---|---|
| `code` | String | |
| `cycleId` | Long | 周期 ID |
| `email` | String | 用户邮箱 |
| `endDate` | Date | 结束日期 |
| `kpiType` | Integer | KPI 类型（1=Strategic/2=Operational/3=Process/4=Enabler，null=不过滤） |
| `startDate` | Date | 开始日期 |
| `type` | Integer | 实体类型 |
| `view` | Integer | 视图模式 |
| `year` | Integer | 年份 |

**响应 data**（`PerformanceResponse`）

| 字段 | 类型 | 说明 |
|---|---|---|
| `totalPerformance` | Decimal | 整体绩效得分 |
| `performances` | Array | 各实体绩效列表 |

**`performances` 每项**（`PerformanceDTO`）

| 字段 | 类型 | 说明 |
|---|---|---|
| `bizId` | Long | 业务实体 ID |
| `name` | String | 实体名称（英文） |
| `nameAr` | String | 实体名称（阿拉伯文） |
| `performance` | Decimal | 绩效得分（%） |
| `userId` | Long | 关联用户 ID |

> **注意**：Apifox schema 中所有字段均非 required，后端实际校验以 Java 注解为准。`bizId` / `userId` 在 schema 中为 Long，但实际 JSON 序列化结果可能为 String（与其他接口 ID 类型一致的约定）。

### 未导出的端点（需以文字接口文档为准）
Committee KPI、team/kpi/breakdown、dashboard/committee/*、action/postpone、org/levels、kpis/save（附件）、lateSubmission、ongoing/list、log/page、team save/detail/page（R-454 字段）均未在 Apifox 文件中，以 `V3.3-API-接口文档.md` 为权威来源。

**Why:** 这是 V3.3 最新确认接口文档，优先于此前的旧版文档。
**How to apply:** 开发所有 V3.3 新需求时以此文档为准，特别注意 ID 类型为 String、R-437 附件字段名变化、R-575 列表过滤参数。
