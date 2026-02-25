<h1 align="center">📚 book-to-skill</h1>

<p align="center">
  <strong>把书拆成 AI Agent 可执行的 Skill，让书中的智慧变成你的决策副驾驶</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/stargazers"><img src="https://img.shields.io/github/stars/apple-ouyang/book-to-skill?style=for-the-badge" alt="GitHub Stars"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/network/members"><img src="https://img.shields.io/github/forks/apple-ouyang/book-to-skill?style=for-the-badge" alt="GitHub Forks"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/issues"><img src="https://img.shields.io/github/issues/apple-ouyang/book-to-skill?style=for-the-badge" alt="Issues"></a>
</p>

<p align="center">
  <a href="#快速安装">快速安装</a> · <a href="docs/README_en.md">English</a> · <a href="#已有-skills">已有 Skills</a> · <a href="#想拆的书单欢迎认领">书单认领</a> · <a href="CONTRIBUTING.md">贡献指南</a>
</p>

---

## 为什么需要 book-to-skill？

我们读过很多好书，但在真正需要做决定的时候，书里的方法论往往想不起来。

你可能读过《行为设计学》里的 WRAP 框架，但面对"要不要辞职创业"时，你还记得"消失选项测试"怎么用吗？

**book-to-skill 解决这个问题：**

把书籍中的框架、案例和操作步骤，拆解成 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 的 Skill 格式。当你面临决策时，AI Agent 会自动调用对应的思维框架，一步步引导你分析——而不是给你一个模糊的建议。

```
/making-decisions 我在纠结要不要辞职创业
```

Agent 会自动走 WRAP 流程：拓宽选择 → 验证假设 → 留出距离 → 准备出错，每一步都有真实案例辅助理解。

> ⭐ **Star 这个项目**，我们会持续拆解更多经典书籍。你不用自己拆——有人拆了你直接用。

### ✅ 在你用之前，你可能想知道

| | |
|---|---|
| 📖 **来自真实书籍** | 每个 Skill 都拆解自经典书籍，不是 AI 编的鸡汤 |
| 🎯 **可执行，不是摘要** | 不是"你应该拓宽思路"，而是"问自己：如果当前选项都不可行，你会怎么办？" |
| 🤖 **Agent 自动调用** | 安装后 Agent 会根据你的场景自动选择对应的 Skill |
| 🧩 **主 Skill + 子 Skill** | 复杂框架拆成路由结构，主 Skill 判断场景，子 Skill 执行具体步骤 |
| 🐝 **支持蜂群拆书** | 长书用 Swarm 多 Agent 并行处理，一个人拆不过来就让 Agent 团队帮你 |

---

## 已有 Skills

### 📕 决策系列（来源：《行为设计学：掌控关键决策》）

| Skill | 触发场景 | 说明 |
|-------|---------|------|
| `making-decisions` | "要不要做 X"、"我在纠结" | WRAP 决策主框架：拓宽选择 → 验证假设 → 留出距离 → 准备出错 |
| `reality-testing-decisions` | "我觉得这个会成功" | 用最小成本实验替代预测，CarsDirect/Intuit 等案例 |
| `seeking-disconfirming-evidence` | "大家都同意"、"感觉太明显了" | 魔鬼代言人、条件法、刻意犯错，打破确认偏误 |
| `decision-tripwires` | "再等等看"、"已经投了很多" | 设定触发点、隔断效应、事前析误，对抗沉没成本 |

### 🛠️ 工具类

| Skill | 说明 |
|-------|------|
| `swarm` | 蜂群协作：自动规划 Agent 团队，并行处理任务。拆书时用它分配多个 Agent 同时处理不同章节 |
| `book-to-skill` | 拆书元技能：把一本书变成 Skill 的标准流程，包含上下文窗口估算和 Agent 分配策略 |

---

## 快速安装

### 方式一：一句话安装

把下面这段话发给你的 Claude Code：

```
帮我安装 book-to-skill 的所有 Skills：https://github.com/apple-ouyang/book-to-skill
```

就这一步。Agent 会自己克隆仓库并复制 Skill 文件。

### 方式二：手动安装

```bash
# 克隆仓库
git clone https://github.com/apple-ouyang/book-to-skill.git

# 复制你需要的 Skill 到 Claude Code skills 目录
cp -r book-to-skill/skills/making-decisions ~/.claude/skills/
cp -r book-to-skill/skills/reality-testing-decisions ~/.claude/skills/
cp -r book-to-skill/skills/seeking-disconfirming-evidence ~/.claude/skills/
cp -r book-to-skill/skills/decision-tripwires ~/.claude/skills/
cp -r book-to-skill/skills/swarm ~/.claude/skills/
cp -r book-to-skill/skills/book-to-skill ~/.claude/skills/
```

<details>
<summary>可选依赖：PDF Skill（拆书时需要）</summary>

拆书流程依赖 PDF Skill 来读取 PDF 格式的书籍：

```bash
npx @anthropic-ai/claude-code-skills install pdf
```

</details>

---

## 使用示例

不需要记命令，直接告诉 Agent 你的问题：

```
# 面临重大决策时
/making-decisions 我在纠结要不要辞职创业

# 想验证一个商业想法
/reality-testing-decisions 我觉得这个产品会有市场

# 团队都同意某个方案，你觉得不对劲
/seeking-disconfirming-evidence 大家都觉得应该收购这家公司

# 项目投了很多钱，不知道该不该继续
/decision-tripwires 这个项目已经投了 50 万，还没看到回报

# 想把一本新书拆成 Skill
/book-to-skill 帮我把《原则》拆成可执行的 Skill
```

---

## 想拆的书单（欢迎认领）

以下是我们计划拆解的书籍，欢迎 PR 认领：

- [ ] 《原则》— Ray Dalio
- [ ] 《思考，快与慢》— Daniel Kahneman
- [ ] 《高效能人士的七个习惯》— Stephen Covey
- [ ] 《巴菲特致股东的信》— Warren Buffett
- [ ] 《穷查理宝典》— Charlie Munger

想拆其他书？直接开 [Issue](https://github.com/apple-ouyang/book-to-skill/issues) 提议，或者 Fork 后提 PR。

---

## 如何贡献

详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

核心原则：
1. **一个 Skill 解决一个具体问题**，不要做大而全的万能 Skill
2. **必须包含真实案例**，不要只有抽象理论
3. **操作步骤要具体到 Agent 可以直接执行**

---

## 项目结构

```
book-to-skill/
├── skills/
│   ├── making-decisions/          # WRAP 决策主框架
│   │   ├── SKILL.md
│   │   └── references/
│   ├── reality-testing-decisions/  # 用实验替代预测
│   │   ├── SKILL.md
│   │   └── references/
│   ├── seeking-disconfirming-evidence/ # 寻找反对证据
│   │   ├── SKILL.md
│   │   └── references/
│   ├── decision-tripwires/        # 设定止损触发器
│   │   ├── SKILL.md
│   │   └── references/
│   ├── swarm/                     # 蜂群协作工具
│   │   ├── SKILL.md
│   │   └── references/
│   └── book-to-skill/            # 拆书元技能
│       └── SKILL.md
├── docs/
│   └── README_en.md              # English README
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

## 灵感来源

决策系列 Skill 拆解自 Chip Heath & Dan Heath 的《Decisive: How to Make Better Choices in Life and Work》（中文版：《行为设计学：掌控关键决策》）。这本书提出了 WRAP 框架，用大量真实案例说明如何避免决策中的四大陷阱。

## License

[MIT](LICENSE)