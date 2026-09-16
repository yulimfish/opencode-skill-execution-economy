# opencode-skill-execution-economy

> opencode 技能：按风险分级决定"要检查/验证/审计到什么程度"，在安全、效果、速度之间取得平衡。

## 是什么

给 opencode 加一条"执行经济"工作流规则，回答主 Agent 每次都会遇到的那个问题：**这一步还要不要做？**

- 收到任务先确定**最终状态**，中间步骤（检查 / 暂存 / 建临时件 / 跑脚本）不算进度。
- 按风险分 **Level 1 / 2 / 3** 决定执行强度：低风险可逆直接连到底、不审；中等一次前置确认 + 一次针对性验证；高风险不可逆才备份 + 确认 + 严格审计。
- **最小充分验证**：每项验证必须能发现最可能的错、防数据损失、或为验收必需，否则不做；同一结论状态未变不重验。
- **窄范围即安全**：`git add <path>` 优于 `git add .` 再全量检查。
- **失败驱动复杂度**：happy path → 真实失败 → 才加一层，不预建全部防护。
- **环境问题绕过优先**：不为完成任务 A 重建环境 B。
- **连续执行不打断**：普通中间步骤不停等"继续"，汇报只报"X 已完成，正在 Y"。
- 还有：自动化成本控制、防止隔离升级循环、时间预算 / 退出条件、信任用户提供的有效结果、决策公式。

零 npm 依赖，纯 markdown；与 `tool-call-discipline` / `post-task-audit` / `clarify-before-act` / `swarm-cluster` 明确分工，不互相打架。

## 快速安装

```bash
git clone --depth=1 https://github.com/Yulimfish/opencode-skill-execution-economy.git \
  ~/.config/opencode/skills/execution-economy
```

或用 [opencode-workflow-kit](https://github.com/Yulimfish/opencode-workflow-kit) 一键装齐。

## 与其它技能的分工

| 技能 | 回答的问题 |
|---|---|
| `tool-call-discipline` | 工具**怎么调**不浪费轮次 |
| **execution-economy** | **要不要调、调到什么程度** |
| `post-task-audit` | 审计**怎么做** |
| **execution-economy** | **何时值得审**（Level 2/3） |
| `clarify-before-act` | 卡住问用户的**模板** |
| **execution-economy** | **何时该停**（Level 3 / 真分支） |
| `swarm-cluster` | 并行拆解的**并发规则** |
| **execution-economy** | 约束它**不要过度开集群**（自动化成本 / 隔离升级） |

## License

MIT © Yulimfish
