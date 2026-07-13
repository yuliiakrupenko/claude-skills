**claude-skills**

A personal library of reusable Claude Skills — instruction sets Claude follows to produce a consistent, structured output, instead of a one-off prompt you have to rewrite every time you need the same thing done.

This repo grows over time as new skills are built. Each skill lives in its own .md file with a name, a description, and a set of instructions Claude follows when triggered.

**What is a Claude Skill**

A Skill is a markdown file with a small frontmatter block (name + description + trigger phrases) followed by structured instructions — research steps, formatting rules, decision logic, output specs. Once added to a Project or to Claude Code, Claude recognizes the trigger phrases in conversation and runs the skill automatically, instead of you having to explain the task from scratch each time.

Skills are best suited to tasks you repeat on a recurring basis, where consistency matters — a weekly report, a recurring analysis, a standard document format — rather than a single ad hoc request.

**How to use a skill from this repo**


Open the .md file for the skill you want.
Add it to Claude as a Skill:

Claude.ai / Claude Projects: Settings → Skills → upload the file.
Claude Code: place the file in your project's skills directory.



Trigger it in conversation using the natural-language phrases listed at the bottom of the skill file (e.g. "run the weekly report"). Claude follows the skill's instructions automatically.
Most skills will ask a short intake the first time you run them — company name, key details, preferences — and remember that context for the rest of the session.


**Skills in this repo**

SkillWhat it doescompetitor-intelligence-SKILL.mdA parameterized competitor intelligence system for B2B product companies — weekly research, pipeline threat scoring, Build/Partner/Ignore verdicts, and role-based leadership summaries (CEO/CMO/CPO). Runs in three modes depending on the depth needed.

(More skills will be added here as they're built.)

**Adding a new skill to this repo**


One .md file per skill, named [skill-name]-SKILL.md.
Include frontmatter: name, description (with trigger phrases), so Claude knows when to use it.
Write instructions generically with placeholders where possible (e.g. [COMPANY_NAME]), so the skill is reusable across contexts rather than hard-coded to one specific use case.
Add a row to the table above.


**Notes**


Skills here are written to avoid vague or unverifiable output — findings should be dated and sourced where applicable, and instructions include explicit fallbacks for missing information rather than allowing Claude to guess.
Output formats vary by skill (HTML reports, documents, etc.) but are specified inside each skill file.
