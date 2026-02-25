---
name: swarm
description: 'This skill should be used when the user asks to "create a team", "create agent team", "蜂群", "swarm", "团队协作", "parallel agents", "spawn teammates", "多 agent 协作", "组建团队", or executes "/swarm". Analyzes user tasks, designs optimal team structure (roles, count, prompts), presents plan for confirmation, then orchestrates team execution.'
---

# 蜂群 Swarm

分析用户任务，自动规划 Agent 团队结构（角色、数量、提示词），确认后执行团队协作。

## 核心流程

```
分析任务 → 选择团队模式 → 设计角色与提示词 → 用户确认 → 创建团队 → 分配任务 → 监控执行
```

## 第一步：分析任务

收到用户任务描述后，从以下维度分析：

| 维度 | 评估内容 |
|------|---------|
| 任务类型 | 功能开发 / 代码审计 / Bug 调试 / 技术选型 / 重构迁移 |
| 可并行度 | 哪些子任务可以同时进行 |
| 文件冲突 | 不同角色是否会修改同一文件 |
| 依赖关系 | 哪些任务必须按顺序执行 |
| 复杂度 | 决定团队规模（2-8 人） |

## 第二步：选择团队模式

根据分析结果，从预定义模式中选择最匹配的模式。详见 `references/team-patterns.md`。

**五种基础模式**：
1. **功能开发** — 新功能、跨层变更
2. **代码审计** — PR Review、安全审计
3. **调试竞争** — Bug 排查、假设验证
4. **研究辩论** — 技术选型、方案评估
5. **重构迁移** — 大规模重构、架构迁移

可混合使用或自定义。如果任务不完全匹配任何模式，基于模式原则自行设计。

## 第三步：设计角色与提示词

为每个 teammate 设计：

1. **角色名称**：简短描述（如 `frontend-dev`、`security-reviewer`）
2. **Agent 类型**：根据职责选择（详见 `references/agent-types.md`）
3. **模型**：根据任务复杂度选择（opus/sonnet/haiku）
4. **权限模式**：default / plan / bypassPermissions
5. **提示词**：包含角色、职责、文件范围、输出要求、协作规则
6. **文件范围**：明确可操作的目录，避免冲突

**提示词结构**：
```
角色：{role}
职责：{responsibilities}

工作范围：
- 只修改：{allowed_dirs}
- 不要触碰：{excluded_dirs}

输出要求：
- {output_format}

协作规则：
- 发现跨模块影响时，通过消息通知 {related_teammate}
- 完成后标记任务为 completed

完成标准：
- {completion_criteria}
```

## 第四步：展示计划并确认

以结构化格式展示团队计划，等待用户确认：

```markdown
## 团队计划

**任务**：{task_description}
**模式**：{pattern_name}
**团队规模**：{count} 人

### 角色分配

| # | 角色 | Agent 类型 | 模型 | 职责概要 |
|---|------|-----------|------|---------|
| 1 | {name} | {type} | {model} | {summary} |
| ...

### 任务列表与依赖

| ID | 任务 | 负责人 | 依赖 |
|----|------|--------|------|
| 1 | {task} | {owner} | - |
| 2 | {task} | {owner} | blockedBy: 1 |
| ...

### 文件分工（避免冲突）

| 角色 | 可操作目录 |
|------|-----------|
| {name} | {dirs} |
| ...

确认此计划？(Y/修改建议)
```

使用 `AskUserQuestion` 工具让用户确认或提出修改。

## 第五步：创建团队并执行

用户确认后，按以下顺序执行：

### 5.1 创建团队

```
TeamCreate → team_name: "{task-slug}"
```

### 5.2 创建任务列表

按计划创建所有任务（TaskCreate），设置依赖关系（TaskUpdate + addBlockedBy）。

### 5.3 启动 Teammates

对每个角色，使用 Task 工具启动 teammate：

```
Task → subagent_type: "{agent_type}"
       name: "{role_name}"
       team_name: "{team_name}"
       model: "{model}"
       mode: "{permission_mode}"
       prompt: "{designed_prompt}"
```

### 5.4 分配任务

通过 TaskUpdate 将任务分配给对应 teammate（设置 owner）。

## 第六步：监控与协调

团队运行期间：

1. **接收消息**：teammate 消息自动送达，及时回应
2. **解决冲突**：如果多个 teammate 需要修改同一文件，协调顺序
3. **重新分配**：如果某 teammate 卡住，重新分配任务或提供帮助
4. **质量把关**：审查 teammate 的输出，不合格则要求修改
5. **合成结果**：所有任务完成后，汇总最终成果

## 第七步：清理

所有任务完成后：

1. 向所有 teammate 发送 shutdown_request
2. 等待所有 teammate 关闭
3. 调用 TeamDelete 清理资源
4. 向用户汇报最终结果

## 关键规则

### 避免文件冲突

**最重要的规则**：不同 teammate 不能同时修改同一文件。

- 按目录/模块划分文件范围
- 共享文件（如配置文件）由领导统一修改
- 需要跨模块变更时，通过消息协调

### 控制团队规模

- 宁少勿多，每增加一个 teammate 都增加 token 消耗
- 简单任务（单模块）：2-3 人
- 中等任务（跨模块）：3-4 人
- 复杂任务（跨层）：4-6 人

### 使用 Delegate 模式

领导应专注协调，不直接写代码。如果发现自己在实现任务，停下来分配给 teammate。

### 提示词要具体

模糊的提示词导致 teammate 偏离方向。包含：
- 具体的文件路径和目录
- 明确的输出格式
- 清晰的完成标准

## 参考资源

### Reference Files

- **`references/team-patterns.md`** — 五种团队模式模板、决策树、规模建议
- **`references/agent-types.md`** — Agent 类型能力对照、模型选择、提示词模板
