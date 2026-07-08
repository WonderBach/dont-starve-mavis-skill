# 《饥荒》新手四季生存规划数据库

文档状态：草稿，待导师确认  
目标：支撑 PC 应用宝 / Marvis 的《饥荒》新手生存规划 Agent MVP  
主口径：Don't Starve 单机 Reign of Giants / Giant Edition 默认世界，一年四季基础生存；首冬作为冬季重点子模块保留

## 文件结构

- `SKILL.md`：Mavis Skill 运行规约，定义取材料引导、截图分析、文字问答诊断、可选自动获取死亡记录和统一复盘输出策略。
- `data/sources.json`：来源索引，每条事实可回溯到 wiki 页面。
- `data/facts.json`：小型事实库，覆盖版本口径、时间节点、关键物资、冬季变化和主要威胁。
- `data/rules.json`：首冬/冬季能力规则层，按保暖链、食物链、光源链三条因果链判断风险。
- `data/seasonal_survival.json`：四季总规则层，覆盖秋季建设、冬季保暖、春季雨湿、夏季降温和防火。
- `data/death_causes.json`：停尸房死因映射库，覆盖冬季、春季、夏季和全年通用死因。
- `data/agent_cards.json`：用户分流卡片、动态补问、固定输出结构和控制台援助代码包。
- `data/morgue_ocr_rules.json`：停尸房截图解读规则，覆盖意图识别、图片 OCR、死因到根因链推理。
- `docs/mentor_alignment_note.md`：给导师看的口径说明和 MVP 边界。
- `docs/scope_expansion_assessment.md`：从首冬扩到一年四季的工作量和范围评估。
- `docs/morgue_screenshot_first_workflow.md`：取材料引导优先后的 Agent/Mavis/Skill 分工和工作量评估。
- `docs/skill_decision_flow.md`：完整判定流程图，覆盖取材料引导、截图分析、文字问答诊断、可选自动获取、OCR、失败回退和介入策略。
- `docs/framework_comparison.md`：新旧死亡逻辑框架对比，以及为什么规则层采用三链模型。

## 关键口径

中文玩家常说的“普通单机版”容易混淆三种情况：

1. 裸 `Don't Starve` 本体：只有 Summer/Winter 两季，没有 Autumn。默认周期是 20 天 Summer + 16 天 Winter，首冬第 21 天开始。
2. 单机 `Reign of Giants`：有 Autumn/Winter/Spring/Summer。新版 MVP 以“一年四季基础生存”为主，但首冬仍是冬季重点。
3. `Don't Starve Together`：首冬第 21 天开始，到第 35 天结束，冬季 15 天；多人机制另有差异。

因此本数据库把主线写成“单机 RoG/Giant Edition 四季生存”，同时保留裸本体和 DST 的兼容备注。

## 四季死亡逻辑

四季生存采用“通用生存链 + 当季环境链”的判断方式，而不是按 UI 三维直接判断：

- 通用链：食物链、光源链、基础战斗安全链、基地安全链。
- 冬季环境链：保暖链，判断暖石、御寒装备、火源和燃料。
- 春季环境链：雨季/潮湿链，判断雨具、避雷、替代食物路线和理智压力。
- 夏季环境链：降温链和防火链，判断冷火、冷暖石、防暑装备、灭火/远离自燃风险。

血量、饥饿、理智是实时结果；链状态才是可提前判断和规划的根因。基地、战斗和探索距离作为上下文放大因子处理。

## Agent 入口与固定输出

主入口优先使用取材料引导：用户只说“帮我看看饥荒怎么活得更久”但没有提供死亡记录或局内信息时，先让用户选择上传停尸房/讣告/死亡结算截图、直接文字描述死亡情况，或在环境允许时尝试自动获取死亡记录。只有用户明确选择自动获取或明确要求打开游戏/进入停尸房/获取死亡记录时，才启动 App Agent。

拿到截图或文字材料后，统一输出：

1. 生存天数
2. 死因
3. 死亡阶段
4. 直接原因
5. 根因链
6. 下一局最低修正方案

## 主要来源

优先使用 dontstarve.wiki.gg。具体页面见 `data/sources.json`。
