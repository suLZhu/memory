---
activation_count: 0
arousal: 0.6
created: '2026-10-14T03:16:10+00:00'
domain:
- 现实侧
- 技术
- 工具坑
id: a007b9dc70e5
importance: 7
last_active: '2026-10-14T03:16:10+00:00'
name: 2026-10-14 03-16-10 Operit workflow 工具坑actionConfig 传裸字符串不包 value
source_tool: hold
tags:
- workflow
- Operit
- 工具坑
- JSON
- 排查方法
title: Operit workflow 工具坑：actionConfig 传裸字符串不包 value
type: dynamic
valence: 0.6
---

【Operit 工具坑记录·workflow 传参】2026-10-14，在用 workflow:create_workflow 建定时回访工作流时反复报 params must be a valid JSON object。根因：给 actionConfig 里的参数（character_card_name、chat_id、message、persist_turn、timeout）都多包了一层 {"value": "..."} 对象。正确写法是直接传裸字符串：actionConfig 用 {"character_card_name": "言朔", "chat_id": "...", "message": "..."}，服务端会自动包装成 StaticValue。排查方法：A/B 对照（最简骨架 actionType=log 成功 + 同骨架换 extended_chat 裸参数成功）才定位到根因，而不是凭猜测删东西。教训：①不要凭未验证的猜测操作（曾误删过一份能用的工作流）；②A/B 对照才是排查，瞎试不是。适用范围：operate workflow 的 create/update/patch 所有涉及 actionConfig 的场合。