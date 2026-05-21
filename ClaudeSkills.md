# Calude Skills


> Skills are worth creating when you have a **repeatable workflow** that Claude gets wrong, inconsistently, or only right after lengthy prompting.

The clearest triggers:

- **You keep correcting the same thing.** If you're always saying "no, do it this way" for a specific task type, that correction belongs in a skill.
- **The task has a non-obvious sequence.** Multi-step workflows where phase order matters and Claude would otherwise improvise.
- **You rely on environment-specific constraints.** Available libraries, output paths, file conventions, API patterns that Claude can't infer from general training.
- **The output format is strict.** Reports, docs, or code that must match a specific shape every time.
- **You're teaching Claude about a tool or framework it doesn't know well.** A skill is basically a cheat sheet it reads before acting.

Skills are **not** worth creating when:

- The task is one-off or rarely repeated
- A short system prompt or user preference handles it
- You're just tweaking tone or style (user preferences cover that)

> The skill system is essentially "read this before you act." Its value scales with how often the task recurs and how much context Claude needs that isn't in its training data. The higher both of those are, the more a skill pays off.

> Skills are available for Pro, Max, Team, and Enterprise users. Free tier users do not have access to Skills.

<br>

---

<br>

# Skills vs Project Instructions

> A Project Instruction is freeform text Claude reads as context, it works, but it's passive

> A SKILL.md is a structured, opinionated guide I actively load before executing a task -- it enforces steps, output formats, phase gates, and quality criteria in a way a Project Instruction can't


<br>

---

<br>

# Working with Skills

> A skill is just a markdown file Claude reads before doing a task.

- Skills live in `/mnt/skills/` as `SKILL.md` files
- Each skill has a name, description, and a set of instructions written in plain markdown
- The description tells Claude when to load it, Claude scans available skills and pull the relevant one before writing any code or artifact
- Once loaded, Claude follows its instructions instead of winging it from training alone

> With claude.ai, you can upload your own skills as zip files through the Customize tab

<br>

---

<br>

## Where is `/mnt/skills` located

>  `/mnt/skills` lives in a sandboxed container environment that claude.ai spins up when Claude need to use computer/file tools.

**Think of it as a temporary Linux environment I get access to mid-conversation. It has:**

- /mnt/skills/public/ -- Anthropic-provided skills (docx, pdf, pptx, frontend-design, etc.)
- /mnt/skills/examples/ -- example/template skills (e.g. skill-creator) that demonstrate patterns
- /home/claude/ -- my working directory for files I generate
- /mnt/user-data/uploads/ -- files you upload to the chat
- /mnt/user-data/outputs/ -- files I produce for you to download

<br>

---

<br>

## The flow in practice:

```
You ask → I scan available skills → I read the matching SKILL.md → I follow its steps → I produce the output
```

## What goes inside a skill:

- Step-by-step process (your phase gates)
- Required outputs per phase
- Format specs (what the HTML prototype must include, what sections the SDD needs)
- Quality gates (what "approved" means before moving on)
- Any defaults or opinions baked in (like tech stack recommendation logic)

> The key insight: it's not magic -- it's structured context I load on demand. The power is that it's reusable and consistent across every project, not dependent on you re-explaining the process each time.

> See more about how to develop a skill [here](https://flash-notes.shannontlreed.workers.dev/notes/calude-ai-how-to-create-a-workflow-skill)

<br>

---

<br>


## How To Create A Skill

1. I build the `SKILL.md` file
2. You zip the folder
3. Go to claude.ai Customize tab and add skill
4. It's available in every conversation automatically

> Skills are simple to create, its just a folder with a SKILL.md file containing YAML frontmatter and instructions

```
dev-planning/
└── SKILL.md
```

## SKILL.md Format


```markdown
---
name: dev-planning
description: Three-phase development planning workflow covering MVP, prototype, and SDD
---

# Dev Planning Workflow
## Phase 1: Planning
...
```

### How Claude discovers it

1. At session start, Claude sees only each skill's name and description, roughly 100 tokens per skill. 
2. The full SKILL.md body loads only when the agent decides the skill is relevant to the current task

<br>

---

<br>


## The current path to upload a custom skill in Claude.ai

> The Skills section moved from Settings → Features into the top-level Customize menu when Anthropic restructured the personalization surface (Customize now houses Styles, Skills, and personal plugins together). The upload mechanism itself didn't change, just its location in the UI.
> So as of today(2/5/2026) this is the current way to do it

> **Prerequisite:** Settings → Capabilities → enable **Code Execution and File Creation**. 
- Skills won't run without it

**Upload steps:**

- Zip your skill folder (the folder containing `SKILL.md` at its root, not the `SKILL.md` file alone)
- Open Claude.ai → **Customize** → **Skills**
- Click the **+** button
- Select **Upload skill** and pick your zip
- Toggle the skill **on** in the list

**Verify it works:**

- Start a new chat
- Type a request that matches your skill's `description` field
- Claude should auto-load it. If it doesn't fire, the description is usually the culprit, not the instructions

**Common gotcha:** zip the **folder**, not the contents. If you select the files inside and zip those, `SKILL.md` ends up at the zip root with no parent folder, and Claude may reject it or fail to detect it.


