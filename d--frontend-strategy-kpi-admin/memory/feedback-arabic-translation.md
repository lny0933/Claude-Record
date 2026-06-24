---
name: feedback-arabic-translation
description: 阿语翻译由产品团队负责，代码里阿语 locale 文件用英文占位，不自动翻译成阿语
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 757655b4-81a8-4992-8173-b6a433fffef0
---

阿语翻译不要自动生成，一律用英文原文作为占位符，等待产品团队提供正式阿语文本。

**Why:** 项目的阿语翻译由产品团队负责，自动翻译的阿语文本不准确，会被产品覆盖，提前写进去没有意义。

**How to apply:** 凡是需要新增或修改 `src/locale/arEG/` 或 `packages/common/src/locale/arEG/` 下的任何 JSON 文件时，value 直接填英文原文，不翻译成阿语。例如新增 `"return": "Return"`，arEG 文件里同样写 `"return": "Return"`，而不是 `"إرجاع"`。
