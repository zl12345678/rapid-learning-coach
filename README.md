# Rapid Learning Coach

[English](#english) | [中文](#中文)

---

## English

`rapid-learning-coach` is a Codex skill for fast, conversation-based learning. It helps an AI turn a vague learning request into a clear learning diagnosis, recommend a suitable learning mode and time box, then guide the user through explanation, practice, self-test, recap, resources, and Feynman-style verification.

### What It Does

When a user asks to learn something, the skill first infers a compact learning setup from the user's message:

- Real goal
- Current level
- Learning type
- Recommended learning mode
- Recommended learning time

The AI asks the user to confirm or edit this diagnosis before teaching. This keeps the session focused on the user's actual goal instead of jumping straight into generic content.

### Learning Modes

The skill supports three modes:

1. `closed-loop coach`: Balanced fast learning and application. Best when the user wants to learn quickly and use the skill soon.
2. `course planner`: Learning ladder, priorities, short-term plan, resources, and light checks. Best when the user first wants a route.
3. `socratic sparring`: One-question-at-a-time active recall. Best when the user wants output pressure, self-testing, or interview-style practice.

If the user does not choose, the AI recommends a mode based on the goal, current level, learning type, and time.

### Learning Loop

Every mode keeps the same six-step loop, with different emphasis:

1. Build a 3-5 level learning ladder.
2. Use the Pareto rule to select the core 20 percent.
3. Run progressive one-on-one self-tests.
4. Produce a compact one-page cheat sheet.
5. Curate at most five high-value resources.
6. Verify understanding with the Feynman method.

After the learning loop, the AI asks whether to organize a session-specific learning note. If the user confirms, the note is saved as a Markdown file under `learning-notes/` by default. The default filename is `YYYY-MM-DD-学习主题-学习阶段.md`.

The note can record the user's actual problems, corrections, difficult points, common mistakes, weak spots, and next practice step.

### Example

User:

```text
I want to learn how to deploy a Java project.
```

The skill should start by producing a diagnosis like:

```text
Real goal: Deploy a Java project to a runnable environment.
Current level: Not specified; I will assume you know Java basics but have limited deployment experience.
Learning type: Hands-on practice / project delivery.
Recommended mode: closed-loop coach.
Recommended time: 2 hours for a first runnable deployment path.
Reason: Deployment needs step-by-step execution, result checks, troubleshooting, and a final operation note.

Does this look right? You can edit any item or reply "start".
```

Only after the user confirms should the AI begin teaching.

### Installation

Clone this repository:

```powershell
git clone https://github.com/zl12345678/rapid-learning-coach.git
```

Copy the skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse .\rapid-learning-coach "$env:USERPROFILE\.codex\skills\rapid-learning-coach"
```

The skill folder is:

```text
rapid-learning-coach/
├── SKILL.md
└── agents/
    └── openai.yaml
```

### Usage

Invoke the skill explicitly:

```text
Use $rapid-learning-coach to help me quickly learn Docker deployment.
```

Or ask a learning request that matches the skill:

```text
I have 90 minutes. Help me learn enough SQL indexing to optimize slow queries.
```

### Repository Layout

```text
rapid-learning-coach/                 # Codex skill
docs/superpowers/specs/               # Design notes
docs/superpowers/plans/               # Implementation plan
learning-notes/                       # Default output folder for generated learning notes
README.md                             # Project overview
```

---

## 中文

`rapid-learning-coach` 是一个用于快速学习的 Codex skill。它会把用户模糊的学习需求转成清晰的学习诊断，推荐合适的学习方式和学习时间，然后通过讲解、练习、自测、复盘、资源筛选和费曼验证带用户完成一轮学习闭环。

### 功能概览

当用户提出学习需求时，skill 会先根据用户原话推断一份简短的学习诊断：

- 真实目标
- 当前水平
- 学习类型
- 推荐学习方式
- 推荐学习时间

AI 会先让用户确认或修改这份诊断，再开始教学。这样可以避免一上来就输出泛泛的内容，让学习过程始终围绕用户真正想达成的目标。

### 学习方式

skill 支持三种学习方式：

1. `closed-loop coach`：闭环教练型。讲解和练习均衡，适合想快速学会并马上应用。
2. `course planner`：课程规划型。重点给学习阶梯、优先级、短期计划、资源和轻量检查，适合先拿路线。
3. `socratic sparring`：苏格拉底陪练型。一次只问一个问题，通过主动回忆、自测和追问暴露薄弱点，适合需要输出压力或查漏补缺。

如果用户没有选择，AI 会根据目标、当前水平、学习类型和时间自动推荐一种方式。

### 学习闭环

每种方式都会保留同一套六步闭环，只是侧重点不同：

1. 搭建 3-5 层学习阶梯。
2. 用二八法则筛选最核心的 20%。
3. 进行一对一递进自测。
4. 生成一页速查表。
5. 筛选最多五份高价值资源。
6. 用费曼法验证理解。

学习结束后，AI 会询问是否整理本次学习笔记。如果用户确认，笔记会默认持久化保存为 `learning-notes/` 目录下的 Markdown 文件。默认文件名为 `YYYY-MM-DD-学习主题-学习阶段.md`。

笔记可以记录用户实际遇到的问题、修正方案、难点、易错点、薄弱点和下一步练习。

### 示例

用户：

```text
我想学习部署 Java 项目。
```

skill 应该先输出类似这样的诊断：

```text
真实目标：把 Java 项目部署到一个可运行环境。
当前水平：未明确，我先按有 Java 基础但部署经验较少处理。
学习类型：偏实操 / 项目落地。
推荐方式：closed-loop coach。
推荐时间：2 小时，完成一次最小可运行部署路径。
推荐理由：部署学习需要按步骤执行、检查结果、排查错误，并在最后整理操作笔记。

这个判断对吗？你可以修改任意一项，或者回复“开始”。
```

只有在用户确认后，AI 才正式开始教学。

### 安装

克隆仓库：

```powershell
git clone https://github.com/zl12345678/rapid-learning-coach.git
```

把 skill 文件夹复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse .\rapid-learning-coach "$env:USERPROFILE\.codex\skills\rapid-learning-coach"
```

skill 文件夹结构：

```text
rapid-learning-coach/
├── SKILL.md
└── agents/
    └── openai.yaml
```

### 使用方式

显式调用 skill：

```text
Use $rapid-learning-coach to help me quickly learn Docker deployment.
```

也可以直接提出符合 skill 的学习需求：

```text
我有 90 分钟，帮我学会 SQL 索引优化慢查询的核心方法。
```

### 仓库结构

```text
rapid-learning-coach/                 # Codex skill
docs/superpowers/specs/               # 设计说明
docs/superpowers/plans/               # 实施计划
learning-notes/                       # 生成学习笔记的默认输出目录
README.md                             # 项目说明
```
