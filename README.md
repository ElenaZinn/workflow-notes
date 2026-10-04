# 工程工作流笔记

> 工程工作流的流程笔记：**bug 修复**、**代码/语言迁移**、**定时轮询与多条件判断**。每套包含步骤、产出物、失效模式清单，以及可填写的模板。

[English](README.en.md)

---

## 解决什么问题

- **bug 修不动**：能定位到但改不对；改完没效果；修好又复发；偶现、复现不了。
- **迁移失控**：全量重写工期爆炸，原有契约与行为语义丢失；局部乱改一改崩一片。
- **轮询出事**：重复触发导致重复扣款；上游数据滞后；条件判断漏了默认兜底。

这三类问题的共同点是：**正常路径都不难写，出事都在异常路径和「跳步」上。**

## 共同原则

这些笔记遵守同一套原则：

1. **先定位根因，再动代码。** 在没有证据之前，任何改动都只是猜测。
2. **每一步都有产出物。** 能被交接给下一个人，或下一次的自己。
3. **规则要落到机器上。** 禁止事项写进 CI gate 或 checklist，而不是靠记忆和自觉。
4. **先设计异常路径。** 线上事故大多发生在没人写下来的那条路径上。
5. **留痕。** 记录里「卡住的地方」是最值钱的一栏。

## 包含什么

| 工作流 | 什么时候用 | 关键产出物 |
| --- | --- | --- |
| [bugfix-diagnosis-flow](bugfix-diagnosis-flow/SKILL.md) | 难复现、定位到但改不对、修完又复发的 bug | 时序图 / 调用链、改动点、bug 记录 |
| [language-migration-flow](language-migration-flow/SKILL.md) | 跨语言迁移（如 Kotlin/Java → Rust），或任何增量改造 | 迁移规范 spec、CI gate 与禁止规则、阶段计划、变更记录 |
| [scheduled-polling-flow](scheduled-polling-flow/SKILL.md) | 定时询价、价格/库存轮询、周期性校验等多条件判断逻辑 | 任务表、校验规则、决策矩阵、退路映射 |

## 目录结构

```text
.
├── .github/
│   ├── ISSUE_TEMPLATE/feedback.yml
│   └── PULL_REQUEST_TEMPLATE.md
├── LICENSE
├── README.md
├── README.en.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── bugfix-diagnosis-flow/
│   ├── SKILL.md
│   └── references/bug-record-template.md
├── language-migration-flow/
│   ├── SKILL.md
│   └── references/migration-checklist.md
└── scheduled-polling-flow/
    └── SKILL.md
```

## 怎么用

- **作为 Agent Skill**：每个目录都是一份带 YAML frontmatter（`name` / `description`）的 `SKILL.md`。放进 Agent 的 skills 目录后，会在匹配到对应场景时触发。
- **作为个人 / 团队 checklist**：直接读，当作「下一步该做什么」的检查清单用。
- **作为模板**：`references/` 里是可填写的模板——迁移规范、CI gate 与禁止规则、阶段 checklist、变更记录、bug 记录。

## 工作流概览

### bugfix-diagnosis-flow

1. 问题定格与优先级
2. 收集证据，定位根因
3. 画时序图与调用链
4. 定位改动点
5. 出修复方案
6. 修复未生效时的排查顺序
7. 复盘与沉淀

### language-migration-flow

1. 现状盘点
2. 写迁移规范（spec）
3. 锁定不可变契约
4. 搭建 CI gate 与禁止规则
5. 划分阶段
6. 变更留痕
7. 先建测试基线，再重构结构
8. 阶段验收与返工

### scheduled-polling-flow

1. 定义任务表
2. 设触发点与校验点
3. 统一调度与去重
4. 多条件判断：决策矩阵
5. 三类硬约束：幂等 / 时限 / 精度
6. 失效模式与退路
7. 沉淀

## Roadmap

- [ ] 代码评审工作流
- [ ] 线上故障响应工作流
- [ ] 发布与回滚 checklist

## License

[MIT](LICENSE)

## 反馈

欢迎提 issue 或建议，贡献方式见 [CONTRIBUTING.md](CONTRIBUTING.md)，交流规范见 [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)。
