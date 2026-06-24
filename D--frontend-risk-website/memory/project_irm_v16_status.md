---
name: project-irm-v16-status
description: IRM V1.6 需求 1-9 的开发状态，包含阻塞原因
metadata: 
  node_type: memory
  type: project
  originSessionId: 9bb91633-bb1f-46a3-af9d-ffcdbb514ed4
---

IRM V1.6 UAT 截止日期：2026-06-16

| # | 编号 | 需求 | 状态 | 备注 |
|---|------|------|------|------|
| 1 | IRM-042 | Treatment Approach 条件逻辑 | ✅ 前端完成 | |
| 2 | IRM-044 | 新建控制措施后自动关联 | ✅ 前端完成 | |
| 3 | IRM-047 | LDAP 头像同步 | ⏭ 跳过 | 无方案文档 |
| 4 | IRM-048 | AddActivityModal 企业风险分组下拉 + categoryId 传参；ProposalViewModal 审批回填 riskLibraryId | ✅ 前端完成 | |
| 5 | IRM-058 | Cycle 管理阶段结构 | ✅ 前端完成 | |
| 6 | IRM-059a | 仪表盘图表点击下钻 | ⚠️ 前端基本完成，调试中 | ChartDrillDownModal Details 按钮 click 事件有待确认（debug console.log 和 onClose 注释需清理）；RiskFixedDashboard & E04 枚举/翻译均已完成 |
| 7 | IRM-059b | RIA 评估完成状态标记 | ⚠️ 前端完成，等后端 | Assessment/Control/Treatment 三列均已接入 completionStatus 图标；后端 completionStatus 字段待修复 |
| 8 | IRM-059c | 添加后删除 Risk 异常修复 | ⏳ 待后端修复 | |
| 9 | IRM-060a | 默认展示部门全部活动 + 双面板选择器 | ✅ 前端完成 | |

**Why:** 记录各需求阻塞原因，避免重复排查。

**How to apply:** 开始某项需求前先查此表确认后端是否就绪。
