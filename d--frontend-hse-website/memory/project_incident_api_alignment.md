---
name: project-incident-api-alignment
description: Incident Report 前端字段与后端 API 的对齐问题，待修复清单
metadata: 
  node_type: memory
  type: project
  originSessionId: 15f2aaaf-484e-4b25-bfa7-f4648789654c
---

# Incident Report — API 对齐待办

**Why:** 前端 AddOrEdit / Detail 组件按设计图重写后，字段命名与后端实际 API 不一致，需要对齐后再联调。

**How to apply:** 下次修 Incident Report 提交逻辑时，按此表修正 `collectPayload` 和表单字段名。

---

## 已确认的后端 API 结构（saveDetailIncidentReport）

```
{
  incidentReportId       : int64
  incidentDate           : string          // "dd/MM/yyyy HH:mm"
  locationSystem         : string
  locationSystemAr       : string
  incidentDetails        : string
  incidentDetailsAr      : string
  actionsTaken           : string
  actionsTakenAr         : string
  attachmentList         : AttachmentDTO[]

  externalPartyInvolved  : int             // 0=No 1=Yes
  externalParties: [{
    id               : int64
    partyType        : int                 // 1=Police 2=Ambulance 3=FireDept 4=Others
    responseDetailsEn: string
    responseDetailsAr: string
    attachmentList   : AttachmentDTO[]
  }]

  employeeImpacted       : int             // 0=No 1=Yes
  propertyImpacted       : int             // 0=No 1=Yes
  otherImpacted          : int             // 0=No 1=Yes
  otherImpact            : string
  otherImpactAr          : string
  convertedAccident      : int

  incidentReportDetailEmployeeSaveRequests: [{
    userId           : int64
    title            : string
    natureOfInjury   : string
    natureOfInjuryAr : string
  }]

  incidentReportDetailPropertySaveRequests: [{
    propertyImpactedId : int64
    propertyName       : string
    propertyNameAr     : string
    natureOfDamage     : string
    natureOfDamageAr   : string
    attachmentList     : AttachmentDTO[]
  }]

  issues: [{
    id                 : int64
    notesRemarksEn     : string
    notesRemarksAr     : string
    correctiveActionEn : string            // 无 s
    correctiveActionAr : string            // 无 s
    responsibleOrgId   : int64             // 部门 ID，非文本
    targetClosureDate  : string
    attachmentList     : AttachmentDTO[]
  }]
}
```

---

## 前端待修正清单

| # | 问题 | 当前前端写法 | 应改为 |
|---|---|---|---|
| 1 | 地点字段 | `emergencyLocation` / `floorOfEmergency` | `locationSystem` / `locationSystemAr`（或等后端加新字段） |
| 2 | 外部参与方结构 | 每个 party 独立字段（`policeResponseDetailsAr` 等） | 统一数组 `externalParties[]`，`partyType` 区分 |
| 3 | 影响开关 | 仅本地 checkbox state，未上传 | 需传 `employeeImpacted` / `propertyImpacted` / `otherImpacted` |
| 4 | 纠正措施字段名 | `correctiveActionsAr` / `correctiveActions` | `correctiveActionAr` / `correctiveActionEn`（无 s） |
| 5 | 负责部门 | 文本 Input `responsibleDepartment` | `responsibleOrgId`（int64，需部门下拉选择器） |

**状态：** 待用户确认 API 结构后统一修正。
