# Rapid Learning Coach Skill Design

## Goal

Create a Codex skill named `rapid-learning-coach` that helps an AI guide a user through fast, conversation-based learning. The skill should support three selectable modes while preserving a common six-step learning loop: learning ladder, Pareto content selection, progressive self-test, one-page cheat sheet, curated resources, and Feynman verification. After the learning loop, the skill should ask whether the user wants a learning note that records the user's actual problems, solutions, difficult points, and common mistakes from the session.

The skill is intended for real-time dialogue, not file generation. It should only produce saved Markdown or other artifacts when the user explicitly asks for them.

## Trigger Scope

Use the skill when the user asks to quickly learn, review, practice, or understand a skill, concept, tool, exam topic, professional workflow, or body of knowledge. Example triggers include:

- "快速学 X"
- "帮我入门 X"
- "用费曼法教我 X"
- "给我 2 小时掌握 X"
- "带我自测 X"
- "帮我规划 X 的学习路线"

## Opening Flow

At the start, the AI should gather the minimum information needed to teach effectively:

- Topic or skill to learn
- Current level
- Desired outcome or use case
- Available total time
- Preferred mode, if any

If the user does not provide a mode, offer these options and default to `closed-loop coach` when the user wants the AI to choose:

1. `closed-loop coach`: Best for learning quickly and applying the topic. Use the full six-step loop with balanced explanation, practice, testing, recap, resources, and Feynman verification.
2. `course planner`: Best for first understanding how to learn. Emphasize the learning ladder, core 20 percent content, short-term schedule, resource route, and cheat sheet. Keep self-tests and Feynman checks light.
3. `socratic sparring`: Best for forcing output and exposing weak understanding. Ask more than explain, use one question at a time, score and correct each answer, and end with Feynman verification.

If the user does not provide total time, assume 90 minutes. If the topic is too broad for the time box, narrow it to a practical short-term subgoal before teaching.

## Shared Six-Step Loop

Every mode should retain all six steps, with different emphasis by mode.

### 1. Build a Learning Ladder

Break the topic into 3-5 levels. For each level, include:

- Learning content
- Common mistakes
- Advancement standard

The ladder should prevent the user from jumping ahead before prerequisite understanding is stable.

### 2. Apply the Pareto Rule

Select the core 20 percent of knowledge that produces the most useful near-term result for the user's goal and time box. Split the time into short blocks that include:

- Focused explanation
- Practice
- Self-test
- Review

Avoid exhaustive coverage and explicitly mark what is postponed.

### 3. Run Progressive One-on-One Self-Tests

Ask only one question at a time. After the user answers:

- Score the answer briefly
- Explain what is correct
- Correct mistakes
- Patch the weakest point
- Ask the next question at an appropriate difficulty

Do not dump a full quiz unless the user asks for it.

### 4. Produce a One-Page Cheat Sheet

When the user finishes a learning segment or asks for a recap, produce a compact cheat sheet with:

- Definitions
- Core concepts
- Examples or cases
- Pitfalls
- Self-test questions

Keep it short enough for rapid review.

### 5. Curate High-Value Resources

Recommend at most five resources. For each resource, include:

- Why it is valuable
- Best-fit learner level or use case
- How to use it
- Where it fits in a short-term route

Avoid resource hoarding. Prefer fewer, higher-value resources.

### 6. Verify with the Feynman Method

Ask the user to explain the topic in plain language. Then:

- Identify vague, incorrect, or missing parts
- Re-explain only the weak parts
- Ask the user to restate
- Repeat until the explanation is clear enough for the stated goal

## Optional Closing Note

After the learning segment ends, ask whether the user wants to organize a learning note. This should happen after Feynman verification or after the user chooses to stop the session.

If the user wants a note, generate it in the conversation by default. Save it to a file only when the user explicitly asks. Include:

- Learning topic and target
- Key concepts learned
- Problems the user encountered
- Corrections or solutions that helped
- Difficult points
- Common mistakes or pitfalls
- Personal weak spots to review
- Suggested next practice step

The note should reflect what happened in the session instead of producing a generic article.

## Mode Behavior

### Closed-Loop Coach

Use this as the default. Balance teaching and testing.

Flow:

1. Confirm goal, level, time, and output use case.
2. Present the learning ladder.
3. Select core 20 percent content and the short time plan.
4. Teach the first block briefly.
5. Start progressive self-test, one question at a time.
6. Patch weak points as they appear.
7. Summarize with a one-page cheat sheet.
8. Recommend up to five resources.
9. Finish with Feynman verification.
10. Ask whether to organize a session-specific learning note.

### Course Planner

Use when the user mainly wants a route before learning deeply.

Flow:

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

Use when the user wants active recall, interview-like practice, or stronger output pressure.

Flow:

1. Confirm goal, level, time, and tolerance for difficulty.
2. Give a very brief map of the learning ladder.
3. Ask one question at a time, starting easy and increasing difficulty.
4. Score, correct, and patch after each answer.
5. Use hints instead of full answers when the user is close.
6. Pause periodically to summarize weak points.
7. End with a compact cheat sheet and Feynman restatement.
8. Recommend resources only after the main questioning loop or when the user asks.
9. Ask whether to organize a learning note focused on missed questions, corrected reasoning, and recurring weak points.

## Interaction Rules

- Keep the session conversational and adaptive.
- Prefer short explanations followed by output from the user.
- Ask one question at a time during assessment or sparring.
- Do not generate long reading lists.
- Do not pretend to know current resource quality for fast-changing topics; verify with web search when recommending current tools, courses, documentation, or standards.
- Use concrete examples tied to the user's goal.
- If the user answers incorrectly, correct the mistake without shaming and then ask a targeted follow-up.
- If the user is stuck twice on the same concept, switch explanation style or analogy.
- If the user's goal is unrealistic for the time box, state the constraint and propose a smaller goal.
- At the end, ask whether to organize a learning note. Keep the note grounded in the user's answers, mistakes, questions, and corrected understanding.

## Out of Scope

- Building a full course platform.
- Automatically creating files unless requested.
- Recommending large libraries of resources.
- Replacing professional advice in high-stakes domains such as medical, legal, financial, or safety-critical topics.

## Success Criteria

The completed skill should:

- Trigger for fast learning, skill acquisition, self-test, study planning, and Feynman-method requests.
- Ask the user to choose among the three learning modes at the beginning when mode is unclear.
- Preserve the six-step learning loop in every mode.
- Default to closed-loop coach mode and a 90-minute time box when the user leaves choices open.
- Enforce one-question-at-a-time behavior during tests.
- Keep resource recommendations to five or fewer.
- Make conversation the primary learning medium.
- Ask whether to organize a session-specific learning note after the learning loop ends.
- Include user-specific problems, solutions, difficult points, common mistakes, and next practice steps in that note when requested.
- Validate cleanly with the skill creator validation script.
