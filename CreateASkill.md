# High-level Workflow/Process To Create A Skill

> The hardest part isn't writing it, it's knowing what you actually do during the process vs. what you think you do. The first cut of any workflow skill captures the idealized version. The second cut, after testing, captures the real one.

## 1. Capture the workflow you already do mentally

- The skill is just that workflow encoded so you don't repeat yourself. 
- Before writing anything, articulate what you do by hand during the process. 
	- Most people skip this and end up writing skills that are abstract templates instead of encoded processes. 
	- A skill is only useful if it captures something specific you do repeatedly.
	- If the workflow lives only in your head, the skill will be vague. 
	- If you can write the workflow as a checklist on paper first, the skill writes itself.
- If you can't describe your process in plain English, you're not ready to write it as a skill.

## 2. Break the workflow into phases

- Each phase needs a clear input, a clear output, and a gate that stops Claude from advancing without your approval. 
- If two steps don't have a meaningful approval point between them, they're one phase, not two.
- Example: 
	- 4 phases because each one produces something the next one literally depends on

## 3. Write the description first, not last

> The description is the trigger. It's how Claude decides whether to load your skill at all. Two rules:

- Front-load _what it does_, then _when to use it_
- List multiple trigger phrases, including ones the user might use without saying "planning" or your skill's name. Skills tend to under-trigger by default.

## 4. Define core principles that apply across every phase

> These are the behaviors you want consistent regardless of phase. 

- Example: phase gates, brutal honesty, recommend don't impose, factor in user experience level, no em dashes. 
- Write these once at the top so you don't have to repeat them inside every phase.

## 5. For each phase, write four things

- **Goal**: one sentence on what this phase produces
- **Steps**: ordered actions Claude takes (questions to ask, what to propose)
- **Output**: the artifact and where it gets saved
- **Gate**: what counts as approval and what Claude waits for

## 6. Bake your preferences into the skill itself

- Don't rely on user preferences alone. 
- The skill should be self-contained so it works the same for anyone who installs it. 
- Repeat key style rules (formatting, tone, what to surface) inside the skill body even if they're elsewhere.

## 7. Test on a real project

- First version is always wrong somewhere. 
- Run it on something real, notice where it fights you or skips a step, then revise. 
- Skills are iterative, not one-shot.
