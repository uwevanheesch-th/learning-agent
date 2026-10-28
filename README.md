# Learning Agent

An **agentic prompt** that turns a tool-enabled LLM coding agent into a **learning companion** rather than a coding assistant. It is designed to help you learn to program independently — it optimizes for *your learning progress*, not for getting the task done for you.

Its behavior is defined entirely by [`AGENTS.md`](./AGENTS.md), a structured pedagogical prompt. The example configuration uses **Kotlin** as the teaching language, but the approach is language-agnostic and easy to adapt.

## What makes it a *learning* companion

The prompt encodes a set of pedagogical principles and guardrails:

- **Socratic by default** — it asks you guiding questions and reveals minimal information, rather than handing you answers.
- **Five interaction modes** — Socratic, Coach, Tutor, Evaluator, and Metacognitive — activated dynamically from how you talk to it.
- **A five-level hint ladder** with a *generation gate*: before producing a full solution, it asks whether you want a hint or the solution, and encourages you to try first.
- **IDE-first principle** — it reads your own files and describes *what to write and where*; it never pastes copy-paste solutions into the chat and never writes solution files for you.
- **Progress awareness via `diary.md`** — it maintains a learning diary that tracks each concept's coverage, your understanding, and its depth using the **SOLO taxonomy** (Biggs & Collis, 1982). There is no fixed curriculum; it orients itself around your current goal and what you have already learned.
- **Psychological safety first** — an explicit principle hierarchy puts your comfort to make mistakes above correctness and efficiency.
- **Response constraints** — concise answers, at most one new concept per turn, always ending with a single check-in question for you.

The guiding metric, stated in the prompt itself:

> **Success metric: you write more code than the agent does.**

## How to use it

1. Use an LLM coding agent that reads a prompt/instructions file and has file-reading and file-writing tools (e.g., Kiro CLI, Claude Code, or any agent that supports an `AGENTS.md`-style system prompt).
2. Place [`AGENTS.md`](./AGENTS.md) in your project so the agent loads it as its instructions.
3. Start a session. On the first turn it reads `diary.md` (creating it if absent) and asks you what you want to work on.
4. Write and edit code in your own IDE; the agent reads your files and guides, questions, and gives you feedback — without writing the solution for you.

### Adapting it

- **Change the language:** the prompt's Evaluator mode and examples reference Kotlin conventions. Replace the language-specific naming/style rules and the code snippets to target another language.
- **Adjust the tool names:** the prompt's *Tool Usage Guidelines* reference specific tool names (e.g., `read_file`, `fs_write`, `execute_bash`). Different agents expose different tool names and capabilities, so adapt this section to match the tools of the agent you actually use — the important part is the *intent* (read student files, only ever write `diary.md`, never run the student's code), not the exact names.
- **Tighten or loosen scope:** the prompt is deliberately curriculum-free and diary-driven. You can add a concepts file or course-specific constraints if you want to bound it to a syllabus.

## Background

This prompt originated in research on AI-based learning companions for software engineering education at [TH Köln](https://www.th-koeln.de/). A study-specific variant (bounded to a course curriculum) was used in an exploratory qualitative study on how advanced computer science students perceive such a companion. This repository publishes the **generic, curriculum-free** version for reuse.

## Citation

If you use or adapt this prompt in teaching or research, please cite it as:

> van Heesch, U. (2026). *Learning Agent: An agentic prompt for a pedagogically constrained AI learning companion.* TH Köln. https://github.com/uwevanheesch-th/learning-agent

## License

This work is licensed under a **Creative Commons Attribution 4.0 International License (CC BY 4.0)**. You are free to share and adapt it, including for commercial purposes, as long as you give appropriate credit. See [`LICENSE`](./LICENSE) for the full text, or <https://creativecommons.org/licenses/by/4.0/>.
