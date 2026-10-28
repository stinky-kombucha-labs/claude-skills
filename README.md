# claude-skills

Claude skills I use day to day for SOC work, research and learning.

Each skill is a folder with a `SKILL.md` file (YAML frontmatter + instructions) and sometimes extra references or scripts.

## Skills

| Skill | What it does |
|---|---|
| [soc-article-review](soc-article-review) | Reviews English write-ups about SOC and IR cases: reasoning, technical accuracy checked against sources, English mistakes and confidentiality leaks. |
| [explain-log-screenshot-for-notes](explain-log-screenshot-for-notes) | Explains a SIEM or audit log screenshot in two sentences, ready to paste into notes. |
| [doc-answer](doc-answer) | Answers questions only from official documentation, with exact quotes and source URLs. |
| [direct-and-to-the-point](direct-and-to-the-point) | A working style for research tasks: every claim has a source, instructions are concrete, no filler. |
| [relearn-forgotten-concept-through-recall](relearn-forgotten-concept-through-recall) | Helps relearn a forgotten concept through a recall attempt, hints, feedback and a retelling instead of a direct answer. |
| [self-learning-strategist](self-learning-strategist) | Builds a learning plan with the SELF framework from Dan Martell's video [How To Become Dangerously Self-Educated (with AI)](https://www.youtube.com/watch?v=6poBPhfB-WY). |
| [obsidian-note-writer](obsidian-note-writer) | Turns screenshots of learning materials into compact Obsidian markdown notes. |

## Install

**Claude Code:** copy a skill folder into `~/.claude/skills/` (all projects) or `.claude/skills/` inside a project.

```bash
git clone https://github.com/stinky-kombucha-labs/claude-skills.git
cp -r claude-skills/soc-article-review ~/.claude/skills/
```

**Claude apps (claude.ai / desktop):** zip a skill folder and upload it in the Skills section of the settings.

## Notes

Some skills answer in Ukrainian and keep technical terms in English, because that is how I take notes. Change the language rules in `SKILL.md` if you need another language.
