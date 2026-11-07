---
name: edu-timetable-conflict-diagnosis-agent-core
display_name: '排课冲突诊断核心助手'
display_name_en: 'Timetable Conflict Diagnosis Agent Core Assistant'
description: '为排课冲突诊断提供输入校验、结构化整理和成果模板支持'
description_zh: '校验课表、约束、冲突报告、优先级、可用资源和调整权限的完整性，并整理为可交付结构'
description_en: 'Validate structured inputs and prepare an output-ready structure for the parent agent.'
examples_zh:
  - '检查我提交的输入字段是否完整'
  - '整理这份业务资料并标出冲突项'
examples_en:
  - 'Check whether my structured input is complete.'
  - 'Organize the supplied business information and flag conflicts.'
version: 1.0.2
author: '广州金励泽科技服务有限公司'
---

# 排课冲突诊断核心助手

本Skill是Agent内部的结构化支持组件，不替代Agent的诊断、方案设计、人工确认和复盘职责。

## 产品契约

- 核心任务：排课冲突诊断和替代方案。
- 主要风险：忽略硬约束或未经授权自动重排
- 去重边界：与智能排课区别：对已有冲突做诊断和比较；不生成完整初始排课。

## 输入

- 课表
- 约束
- 冲突报告
- 优先级
- 可用资源和调整权限

## 工作流程

1. 用户提供结构化JSON时，先执行 @scripts/validate_input.js。
2. 输入缺失时返回缺失字段，不要求Agent自行编造。
3. 输入冲突时返回确认项，暂停正式结论。
4. 安全检查通过后，按 @templates/OUTPUT_TEMPLATE.md 建立空结构。
5. 将结构交回Agent继续专业处理。

## 专属检查

- 先提取班级、教师、教室、时间、学生约束和硬性规则，再生成排程草案。
- 硬冲突不得被软约束覆盖；无法消解时列出冲突、影响和升级责任人。
- 所有变更保留原状态、目标状态、生效时间和回退方式。
- 正式课表、考勤和审批结果必须由有权限人员确认后生效。

## 边界

不得未经授权修改正式课表或审批状态，不得处理无权访问的学生资料。

本Skill不产生最终业务结论，不调用外部收费API，不保存用户数据。
