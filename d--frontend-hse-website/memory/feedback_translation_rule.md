---
name: feedback-translation-rule
description: HSE 项目整理翻译时的复用规则：优先查 src/locale 和 packages/common/src/locale，有相同翻译则直接复用
metadata: 
  node_type: memory
  type: feedback
  originSessionId: a43e634c-3c97-4c0e-8554-0b3197894492
---

整理翻译时，优先检查 `src/locale` 和 `packages/common/src/locale` 下是否已有相同文本的翻译，有则直接在页面组件里引用已有 key（无论是否同一模块），不必重复新增。只有两处都找不到时，才在对应模块的 locale 文件里新增。

**Why:** 用户明确要求减少重复翻译 key，优先复用 common 等公共 locale。

**How to apply:** 仅限 HSE 项目（D:/frontend/hse-website）。每次整理翻译时，先 grep common.json 和其他已有 locale，找到匹配的翻译后更新组件引用，再处理剩余缺失 key。
