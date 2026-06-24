---
name: contractor-sync-rule
description: hse-website 中 Contractor 相关页面改动需同步到 hse-contractor 客户端项目
metadata: 
  node_type: memory
  type: project
  originSessionId: 5c0aa3d6-8502-498a-843f-f1330c18af4a
---

凡涉及以下两个路径的改动，必须同步到 `D:\frontend\hse-contractor` 的对应位置：

- `src/pages/Contractor` → 同步到 hse-contractor 的对应 Contractor 页面
- `src/pages/PermitToWork/ContractorPortal` → 同步到 hse-contractor 的对应 ContractorPortal 页面

**Why:** hse-contractor 是从 hse-website 拆分出的独立客户端，两边共享这两块功能代码，改 hse-website 不同步会导致两端行为不一致。

**How to apply:** 每次修改上述路径的文件，改完 hse-website 后，立即定位 hse-contractor 中的对应文件，执行相同改动。同步前先读一下 hse-contractor 的文件，确认结构一致再修改。
