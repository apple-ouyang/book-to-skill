<h1 align="center">📚 book-to-skill</h1>

<p align="center">
  <strong>Turn books into executable AI Agent Skills — your decision-making copilot</strong>
</p>

<p align="center">
  <a href="../LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/stargazers"><img src="https://img.shields.io/github/stars/apple-ouyang/book-to-skill?style=for-the-badge" alt="GitHub Stars"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/network/members"><img src="https://img.shields.io/github/forks/apple-ouyang/book-to-skill?style=for-the-badge" alt="GitHub Forks"></a>
  <a href="https://github.com/apple-ouyang/book-to-skill/issues"><img src="https://img.shields.io/github/issues/apple-ouyang/book-to-skill?style=for-the-badge" alt="Issues"></a>
</p>

<p align="center">
  <a href="#quick-install">Quick Install</a> · <a href="../README.md">中文</a> · <a href="#available-skills">Skills</a> · <a href="#book-wishlist">Book Wishlist</a> · <a href="../CONTRIBUTING.md">Contributing</a>
</p>

---

## Why book-to-skill?

We've all read great books, but when it's time to make a real decision, the frameworks we learned are nowhere to be found.

You might have read about the WRAP framework in *Decisive*, but when facing "should I quit my job to start a business?", can you remember how to use the "Vanishing Options Test"?

**book-to-skill solves this:**

It breaks down frameworks, case studies, and actionable steps from books into [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill format. When you face a decision, the AI Agent automatically invokes the right thinking framework and guides you step by step — instead of giving you vague advice.

```
/making-decisions I'm torn between quitting my job or staying
```

The Agent walks you through the WRAP process: Widen options → Reality-test → Attain distance → Prepare to be wrong, with real case studies at every step.

> ⭐ **Star this project** — we're continuously breaking down more classic books. You don't have to do it yourself.

### ✅ Before you start

| | |
|---|---|
| 📖 **From real books** | Every Skill is extracted from classic books, not AI-generated fluff |
| 🎯 **Actionable, not summaries** | Not "broaden your thinking", but "ask yourself: if all current options disappeared, what would you do?" |
| 🤖 **Auto-invoked by Agent** | Once installed, the Agent picks the right Skill based on your situation |
| 🧩 **Router + Sub-Skills** | Complex frameworks split into routing structure — main Skill routes, sub-Skills execute |
| 🐝 **Swarm-powered book processing** | Long books processed by multiple Agents in parallel via Swarm |

---

## Available Skills

### 📕 Decision Series (Source: *Decisive* by Chip & Dan Heath)

| Skill | Trigger | Description |
|-------|---------|-------------|
| `making-decisions` | "Should I do X", "I'm torn" | WRAP framework: Widen → Reality-test → Attain distance → Prepare to be wrong |
| `reality-testing-decisions` | "I think this will work" | Replace predictions with low-cost experiments. CarsDirect/Intuit cases |
| `seeking-disconfirming-evidence` | "Everyone agrees", "Feels obvious" | Devil's advocate, conditional method, deliberate mistakes. Break confirmation bias |
| `decision-tripwires` | "Let's wait and see", "Already invested a lot" | Set tripwires, partition effects, pre-mortem. Fight sunk cost fallacy |

### 🛠️ Tools

| Skill | Description |
|-------|-------------|
| `swarm` | Swarm collaboration: auto-plan Agent teams for parallel task processing |
| `book-to-skill` | Meta-skill: standard process for turning a book into Skills, with context window estimation |

---

## Quick Install

### Option 1: One-liner

Send this to your Claude Code:

```
Install all book-to-skill Skills: https://github.com/apple-ouyang/book-to-skill
```

That's it. The Agent clones the repo and copies the Skill files.

### Option 2: Manual

```bash
git clone https://github.com/apple-ouyang/book-to-skill.git

cp -r book-to-skill/skills/making-decisions ~/.claude/skills/
cp -r book-to-skill/skills/reality-testing-decisions ~/.claude/skills/
cp -r book-to-skill/skills/seeking-disconfirming-evidence ~/.claude/skills/
cp -r book-to-skill/skills/decision-tripwires ~/.claude/skills/
cp -r book-to-skill/skills/swarm ~/.claude/skills/
cp -r book-to-skill/skills/book-to-skill ~/.claude/skills/
```

<details>
<summary>Optional: PDF Skill (needed for book processing)</summary>

```bash
npx @anthropic-ai/claude-code-skills install pdf
```

</details>

---

## Usage

Just tell the Agent your problem:

```
/making-decisions Should I quit my job to start a business?
/reality-testing-decisions I think this product has a market
/seeking-disconfirming-evidence The whole team agrees we should acquire this company
/decision-tripwires We've invested $500K with no returns yet
/book-to-skill Help me turn "Principles" into executable Skills
```

---

## Book Wishlist

Books we plan to break down — PRs welcome:

- [ ] *Principles* — Ray Dalio
- [ ] *Thinking, Fast and Slow* — Daniel Kahneman
- [ ] *The 7 Habits of Highly Effective People* — Stephen Covey
- [ ] *Berkshire Hathaway Letters to Shareholders* — Warren Buffett
- [ ] *Poor Charlie's Almanack* — Charlie Munger

Want to add a book? Open an [Issue](https://github.com/apple-ouyang/book-to-skill/issues) or submit a PR.

---

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md).

Core principles:
1. **One Skill solves one problem** — no catch-all mega-Skills
2. **Must include real case studies** — no abstract theory only
3. **Steps must be specific enough for an Agent to execute**

---

## Inspiration

The decision Skills are extracted from Chip Heath & Dan Heath's *Decisive: How to Make Better Choices in Life and Work*. The book introduces the WRAP framework with extensive real-world cases showing how to avoid the four villains of decision-making.

## License

[MIT](../LICENSE)
