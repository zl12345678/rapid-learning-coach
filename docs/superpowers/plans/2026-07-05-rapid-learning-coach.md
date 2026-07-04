# Rapid Learning Coach Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a `rapid-learning-coach` Codex skill in this repository for real-time, multi-mode rapid learning conversations.

**Architecture:** Create a single skill folder at `rapid-learning-coach/` with a concise `SKILL.md` and generated `agents/openai.yaml` metadata. Keep the skill instruction-only because the workflow is conversational and does not need scripts, assets, or reference files.

**Tech Stack:** Codex skill markdown, YAML frontmatter, `skill-creator` helper scripts, git.

## Global Constraints

- Skill name must be `rapid-learning-coach`.
- The skill must support three opening modes: `closed-loop coach`, `course planner`, and `socratic sparring`.
- The skill must preserve the six-step loop in every mode: learning ladder, Pareto content selection, progressive self-test, one-page cheat sheet, curated resources, and Feynman verification.
- The skill must default to `closed-loop coach` and 90 minutes when choices are open.
- The skill must ask only one question at a time during tests and sparring.
- The skill must recommend at most five resources.
- The skill must ask whether to organize a session-specific learning note after the learning loop ends.
- Saved files must be created only when the user explicitly asks.
- The skill must validate cleanly with the skill creator validation script.

---

### Task 1: Initialize Skill Skeleton

**Files:**
- Create: `rapid-learning-coach/SKILL.md`
- Create: `rapid-learning-coach/agents/openai.yaml`

**Interfaces:**
- Consumes: `docs/superpowers/specs/2026-07-05-rapid-learning-coach-design.md`
- Produces: A valid Codex skill folder named `rapid-learning-coach`

- [ ] **Step 1: Locate the skill creator helper scripts**

Run:

```powershell
Get-ChildItem C:\Users\admin\.codex\skills\.system\skill-creator\scripts
```

Expected: output includes `init_skill.py` and `quick_validate.py`.

- [ ] **Step 2: Initialize the skill in the repository**

Run:

```powershell
python C:\Users\admin\.codex\skills\.system\skill-creator\scripts\init_skill.py rapid-learning-coach --path D:\Documents\study-skill --interface display_name="Rapid Learning Coach" --interface short_description="Guide fast learning with selectable coaching, planning, and Socratic modes." --interface default_prompt="Help me quickly learn a topic using a selectable rapid-learning mode."
```

Expected: command exits successfully and creates `D:\Documents\study-skill\rapid-learning-coach`.

- [ ] **Step 3: Verify generated files exist**

Run:

```powershell
Test-Path D:\Documents\study-skill\rapid-learning-coach\SKILL.md
Test-Path D:\Documents\study-skill\rapid-learning-coach\agents\openai.yaml
```

Expected: both lines print `True`.

- [ ] **Step 4: Commit skeleton**

Run:

```powershell
git add rapid-learning-coach
git commit -m "Initialize rapid learning coach skill"
```

Expected: commit succeeds with the generated skill skeleton.

### Task 2: Write Skill Instructions

**Files:**
- Modify: `rapid-learning-coach/SKILL.md`

**Interfaces:**
- Consumes: `rapid-learning-coach/SKILL.md` skeleton
- Produces: Complete skill instructions with valid `name` and `description` frontmatter

- [ ] **Step 1: Replace `SKILL.md` with final content**

Use this exact structure and content:

```markdown
---
name: rapid-learning-coach
description: Real-time rapid learning coach for quickly learning, reviewing, practicing, planning, or testing understanding of a skill, concept, tool, exam topic, professional workflow, or body of knowledge. Use when the user asks to quickly learn something, build a learning path, apply the Pareto rule to study, run one-on-one progressive self-tests, create a compact cheat sheet, curate a small set of high-value resources, use the Feynman method, or organize session-specific learning notes after a learning conversation.
---

# Rapid Learning Coach

Guide the user through fast, conversation-based learning. Prefer live interaction over static content. Use saved files only when the user explicitly asks.

## Opening

Collect only the minimum context needed:

- Topic or skill
- Current level
- Desired outcome or use case
- Available total time
- Preferred mode

If the user has not chosen a mode, offer:

1. `closed-loop coach`: balanced fast learning and application.
2. `course planner`: route, priorities, schedule, resources, and light checks.
3. `socratic sparring`: one-question-at-a-time active recall with stronger pressure.

Default to `closed-loop coach` when the user wants the AI to choose. Default to 90 minutes when no time box is given. If the topic is too broad for the time box, narrow it to a practical short-term subgoal before teaching.

## Shared Loop

Preserve these six steps in every mode, changing only the emphasis:

1. Build a 3-5 level learning ladder with learning content, common mistakes, and advancement standards.
2. Apply the Pareto rule by selecting the core 20 percent that best serves the user's goal and time box. Mark postponed content.
3. Run progressive one-on-one self-tests. Ask only one question at a time, wait for the answer, score briefly, correct mistakes, patch the weakest point, then ask the next suitable question.
4. Produce a compact one-page cheat sheet with definitions, core concepts, examples, pitfalls, and self-test questions when the user finishes a segment or asks for review.
5. Curate at most five high-value resources. For each, explain fit, learner level, usage, and where it belongs in a short-term route. Verify current resource quality with web search for fast-changing topics.
6. Verify with the Feynman method by asking the user to explain in plain language, identifying gaps, re-explaining weak parts, and asking for a restatement until the explanation is clear enough for the user's goal.

## Modes

### Closed-Loop Coach

Use this as the default. Flow:

1. Confirm goal, level, time, and use case.
2. Present the learning ladder.
3. Select the core 20 percent and short time plan.
4. Teach the first block briefly.
5. Start progressive self-test, one question at a time.
6. Patch weak points as they appear.
7. Summarize with a one-page cheat sheet.
8. Recommend up to five resources.
9. Finish with Feynman verification.
10. Ask whether to organize a session-specific learning note.

### Course Planner

Use when the user mainly wants a route before learning deeply. Flow:

1. Confirm goal, level, time, and target deadline.
2. Present the learning ladder in more detail.
3. Identify the core 20 percent and postponed content.
4. Create a short-term route with practice and review blocks.
5. Add a lightweight diagnostic self-test.
6. Produce a one-page cheat sheet or route recap.
7. Recommend up to five resources with usage instructions.
8. Offer a short Feynman check if the user wants to validate understanding immediately.
9. Ask whether to organize a learning note, especially if the user discussed blockers, constraints, or confusing areas.

### Socratic Sparring

Use when the user wants active recall, interview-like practice, or stronger output pressure. Flow:

1. Confirm goal, level, time, and tolerance for difficulty.
2. Give a very brief map of the learning ladder.
3. Ask one question at a time, starting easy and increasing difficulty.
4. Score, correct, and patch after each answer.
5. Use hints instead of full answers when the user is close.
6. Pause periodically to summarize weak points.
7. End with a compact cheat sheet and Feynman restatement.
8. Recommend resources only after the main questioning loop or when the user asks.
9. Ask whether to organize a learning note focused on missed questions, corrected reasoning, and recurring weak points.

## Learning Notes

After Feynman verification or when the user stops the session, ask whether to organize a learning note. Generate the note in the conversation by default. Save it to a file only when explicitly asked.

When requested, include:

- Learning topic and target
- Key concepts learned
- Problems the user encountered
- Corrections or solutions that helped
- Difficult points
- Common mistakes or pitfalls
- Personal weak spots to review
- Suggested next practice step

Make the note session-specific. Base it on the user's answers, mistakes, questions, and corrected understanding instead of writing a generic article.

## Interaction Rules

- Keep the session conversational and adaptive.
- Prefer short explanations followed by user output.
- During assessment or sparring, ask one question at a time.
- Do not dump a full quiz unless the user asks.
- Do not generate long reading lists.
- Correct mistakes directly and kindly, then ask a targeted follow-up.
- If the user is stuck twice on the same concept, switch explanation style or analogy.
- If the user's goal is unrealistic for the time box, state the constraint and propose a smaller goal.
- Do not replace professional advice in high-stakes medical, legal, financial, or safety-critical topics.
```

- [ ] **Step 2: Check frontmatter**

Run:

```powershell
Get-Content -First 5 D:\Documents\study-skill\rapid-learning-coach\SKILL.md
```

Expected: first lines include `name: rapid-learning-coach` and the long `description`.

- [ ] **Step 3: Commit skill instructions**

Run:

```powershell
git add rapid-learning-coach\SKILL.md
git commit -m "Write rapid learning coach instructions"
```

Expected: commit succeeds with the completed `SKILL.md`.

### Task 3: Validate Skill and Metadata

**Files:**
- Modify if needed: `rapid-learning-coach/agents/openai.yaml`

**Interfaces:**
- Consumes: completed `rapid-learning-coach/SKILL.md`
- Produces: validated skill folder

- [ ] **Step 1: Run quick validation**

Run:

```powershell
python C:\Users\admin\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\Documents\study-skill\rapid-learning-coach
```

Expected: validation passes with no required-field, YAML, or naming errors.

- [ ] **Step 2: Inspect UI metadata**

Run:

```powershell
Get-Content -Raw D:\Documents\study-skill\rapid-learning-coach\agents\openai.yaml
```

Expected: metadata uses `Rapid Learning Coach`, a short description matching the skill, and a default prompt about quickly learning a topic.

- [ ] **Step 3: Regenerate metadata if it is stale**

Run this only if Step 2 shows missing or stale metadata:

```powershell
python C:\Users\admin\.codex\skills\.system\skill-creator\scripts\generate_openai_yaml.py D:\Documents\study-skill\rapid-learning-coach --interface display_name="Rapid Learning Coach" --interface short_description="Guide fast learning with selectable coaching, planning, and Socratic modes." --interface default_prompt="Help me quickly learn a topic using a selectable rapid-learning mode."
```

Expected: metadata is regenerated successfully.

- [ ] **Step 4: Re-run validation**

Run:

```powershell
python C:\Users\admin\.codex\skills\.system\skill-creator\scripts\quick_validate.py D:\Documents\study-skill\rapid-learning-coach
```

Expected: validation passes.

- [ ] **Step 5: Commit validation updates**

Run:

```powershell
git add rapid-learning-coach
git commit -m "Validate rapid learning coach skill"
```

Expected: commit succeeds if metadata changed. If there are no changes after validation, skip the commit and record that validation passed.

### Task 4: Final Repository Check

**Files:**
- Read: `rapid-learning-coach/SKILL.md`
- Read: `rapid-learning-coach/agents/openai.yaml`

**Interfaces:**
- Consumes: validated skill folder
- Produces: final verified repository state

- [ ] **Step 1: Review generated file list**

Run:

```powershell
git ls-files
```

Expected: output includes the spec, this plan, `rapid-learning-coach/SKILL.md`, and `rapid-learning-coach/agents/openai.yaml`.

- [ ] **Step 2: Confirm working tree is clean**

Run:

```powershell
git status --short
```

Expected: no output.

- [ ] **Step 3: Report completion**

Report the skill path, validation command result, and commit hashes created during implementation.
