# 日语学习功能 PRD 文档包

本文档包还原“日语相关学习功能，含增删查改、游戏录入、听日语等”的当前业务能力。正文只描述业务事实与可迁移的产品能力，不绑定当前工程或技术栈。

## 阅读顺序

1. 先读 `01-product-scope.md`，理解产品范围和独立落地边界。
2. 再读 `02-users-and-scenarios.md`，理解使用角色和场景。
3. 继续读 `03-functional-requirements.md` 到 `08-interface-contracts.md`，获得功能、规则、数据、流程、权限和交互契约。
4. 读 `09-non-functional-requirements.md` 和 `10-acceptance-criteria.md`，作为实现质量和验收依据。
5. 最后读 `11-open-questions.md` 和 `12-source-evidence.md`，区分已确认事实与待确认问题。

## 功能范围

本 PRD 覆盖以下业务能力：

- 日语学习资源的维护、查询、查看、删除、导出和来源分组。
- 日语文本、中文释义、日语朗读音频、中文朗读音频的管理。
- 基础日语学习资源的卡片化查看和音频播放。
- 批量生成朗读音频、批量补充中文释义、按所选资源合成听力课程音频。
- 游戏式录入日语句子，自动获得中文释义与音频，保存为学习资源。
- 每日学习数量、每日学习时长、累计学习数量、累计学习时长的统计展示与更新。
- 录入时的日文/中文输入辅助切换。

## 文档索引

- `01-product-scope.md`：产品目标、用户价值、边界和独立产品形态。
- `02-users-and-scenarios.md`：角色、场景、用户目标、前置条件和完成条件。
- `03-functional-requirements.md`：可实现的功能需求清单。
- `04-business-rules.md`：限制、默认行为、异常处理和业务判断。
- `05-data-model.md`：稳定业务数据模型。
- `06-workflows-and-states.md`：关键流程、状态流转、失败和重试。
- `07-permissions-and-boundaries.md`：权限、访问边界和跨业务关系。
- `08-interface-contracts.md`：技术无关的命令、查询、事件和错误语义。
- `09-non-functional-requirements.md`：性能、可用性、安全、隐私和可维护性。
- `10-acceptance-criteria.md`：可测试验收标准。
- `11-open-questions.md`：当前项目无法确认的问题。
- `12-source-evidence.md`：事实来源证据，只用于溯源审计。
