---
name: cold-start-setup
description: >
  Run the cold-start setup — learns preferences and writes CLAUDE.md. Use on first run, when
  CLAUDE.md is missing or has placeholders, or when the user says "set up the
  plugin", "onboard me", "configure plugin", or wants to re-run the
  setup.
argument-hint: "[--redo to re-run]"
---

# /cold-start-setup

1. Check `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` — if populated and no `--redo`, confirm before overwriting.
2. Run the interview workflow below.
3. Seed docs: privacy policy (URL or file), DPA template, one reference PIA. Read all three.
4. Extract: policy commitments, DPA positions (note deltas vs. stated), PIA structure.
5. Migration: if a populated CLAUDE.md (no `[PLACEHOLDER]` markers) exists at `~/.claude/plugins/cache/company-brain-4-sellers-marketplace/company-brain/*/CLAUDE.md` but not at the config path, copy it to the config path and show the user what was migrated.
6. Write `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` (create parent directories as needed). Show summary. Offer first task.


```
/company-brain:cold-start-setup
```

---

# Cold-Start Setup: Building personal knowledge bases using LLMs and wiki-style notes

## Purpose

Learn how *this* team works — what topics actually apply to them, what rules to organize their information. Write it into `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` so every other skill reads from the same understanding.

Personal knowledge practices vary wildly by person. This process figures out personal preferences.

## Cold-start check

Read `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md`:
- **Does not exist** → start the interview.
- **Contains `<!-- SETUP PAUSED AT: -->`** → greet the user and offer to resume from that section.
- **Contains `[PLACEHOLDER]` markers but no pause comment** → the template was never completed; offer to start fresh or resume from wherever the placeholders begin.
- **Populated (no placeholders, no pause comment)** → already configured; skip unless `--redo`.

The template structure lives at `${CLAUDE_PLUGIN_ROOT}/CLAUDE.md` — use it as the section scaffold. Write the completed profile to the config path, creating parent directories as needed.

If a CLAUDE.md exists at the old cache path `~/.claude/plugins/cache/company-brain-4-sellers-marketplace/company-brain/*/CLAUDE.md` but not at the config path, copy it forward.

## Check for the shared company profile

Look for `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-profile.md`.

- **If it exists:** Read it. Show a one-line confirmation: "This wiki is for company [name], [practice setting], at [company], operating in [industry]. Right? (Or say 'update' to change the shared profile.)" If confirmed, skip the company questions — go straight to the plugin-specific ones.
- **If it doesn't exist:** You'll be the first plugin this user set up. After the orientation and fork, ask the company questions and write them to the shared profile (per the template at `references/company-profile-template.md` in the plugin root), then continue with the plugin-specific questions. Tell the user: "I've saved your company profile — the other plugins will read it and skip these questions."

The company questions that belong in the shared profile (and should NOT be re-asked if it exists): company name, industry, webpage, size, regulators. 

## Install scope check

Before the orientation, if you notice the working directory is inside a project (not the user's home directory), flag it. Say once:

> **Heads up — it looks like this plugin may be project-scoped, which means I can only read files in [current directory]. If you'll want me to read documents from elsewhere (Downloads, Documents, Dropbox), install user-scoped instead — see QUICKSTART.md. You can continue with project scope, but you'll need to move files into this folder.**

Ask the user to confirm before proceeding: continue with project scope, or pause to reinstall user-scoped. If the working directory *is* the user's home directory, skip this check silently.


## After the scope check

Orient the user before the first interview question:

> "This plugin maintains your knowledge wiki organize your raw sources into linked wiki pages following your own style. Everything you answer can be changed later. Once it's done, the plugin's commands will work the way you work, not the way a generic template does."
>
> Then: "Ready? A few quick questions first, then we'll go deeper."


Populate the company profile only from the user's typed answers. Do not read `~/CLAUDE.md` or pull practice facts from ambient context. If something relevant is already visible in the conversation, ask before using it.

**start path:** ask the existing interview flow below. Close with: "Done. You can start using the commands now. Run `/company-brain:cold-start-setup --redo ` to re-do."


## Interview pacing

- **Assume the answer exists somewhere.** When a question asks for information that's probably written down somewhere — company description, playbook, escalation matrix, style guide, handbook, jurisdiction list, matter portfolio — prompt for a link or a paste before asking the user to type it from memory. "Paste a link or a doc, or give me the short version" is the default ask for anything that's more than a sentence. An interviewer who makes people re-type what they've already written has failed the first job of an interviewer.
- **Batch size — count subparts.** "Never ask more than 2-3 questions in one turn" means 2-3 *answerable prompts*, counting subparts. One question with 5 subparts is 5 questions. The test: can the user answer without scrolling? If the questions don't fit on one screen, it's too many. Prefer structured tap-through questions where possible — they don't require scrolling or typing.

**Pause for real answers.** Some questions have quick tap-through answers (controller vs. processor, regulatory footprint). Others need the user to type something, describe something, or upload a document (privacy policy, DPA template, reference PIA, DPA negotiating positions, systems-list for DSARs). When a question needs more than a quick tap:

- **Ask the question and wait.** Say explicitly: "This one needs a typed answer — I'll wait." Do not move to the next question until the user responds.
- **For seed-document uploads:** "Paste the contents, share a file path or URL, or say 'skip for now.' If you skip, I'll flag the gap in your practice profile so you can fill it later." Then actually wait.
- **Before writing the practice profile:** review the interview. List any questions that were skipped or answered with placeholders. Say: "Before I write your practice profile, here's what's still open: [list]. Want to fill any of these now, or leave them as placeholders?" Then wait for the answer.
- **Never** write a practice profile with silent gaps. Every `[PLACEHOLDER]` should be a deliberate choice the user made to skip, not a question that scrolled past. If the DPA template or reference PIA was skipped, note `[POSITIONS UNTESTED]` so downstream skills know.
- **Pause and resume.** Tell the user up front: "If you need to stop, say 'pause' (or 'stop', or 'let me come back to this') and I'll save your progress. Run `/company-brain:cold-start-setup` again later and I'll pick up where you left off." When the user pauses, write a partial configuration to `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` with a `<!-- SETUP PAUSED AT: [section name] — run /company-brain:cold-start-setup to resume -->` comment at the top and `[PENDING]` markers (distinct from `[PLACEHOLDER]`) on unanswered fields. When setup re-runs and finds a paused config, greet the user: "Welcome back. You paused at [section]. Your earlier answers are saved. Pick up where we left off, or start over?" Do not re-ask questions already answered.

**Verify user-stated legal facts as they come up in setup.** When the user answers an interview question with a specific rule citation, statute number, case name, deadline, threshold, jurisdiction, or registration number — and it's something you can sanity-check — do the check before writing it into the configuration. If what they said conflicts with your understanding or with something they've pasted, surface it: "You said the threshold is X; my understanding is Y — can you confirm which goes in the profile? `[premise flagged — verify]`" A wrong fact written into CLAUDE.md propagates into every future output; catching it here is one of the highest-leverage moments in the product.

## The interview

### Opening

> I'm going to help with with some question to define the structure of your own LLM wiki. This question will help to understand the type of company you try to sell products.
>
> Then I'm going to ask you some question to understand the compnay name, industry as well as it is regulated. I'll learn more from those than from anything you tell me.

### To whom you are trying to sell products 

> **Here's what I'm good at in privacy practice:**
>
> - **Company Name** — e.g., "Company name we are trying to approach and research to identify potential sell opportunities." 
> - **Industry** — e.g., "Industry associated to this company." 
> - **WebPage** — e.g., "official URL of the companies webpage or investors reports." 
> - **Size** — e.g., "Approximate number of employees." 
> - **Regulated** — e.g., "Who are the regulators that this company is subject toß or N/A if not applicable." 

Created the base folder structure for the plugin and write the CLAUDE.md file in the selected scope. If the user is in a project scope, create the config path under the project folder. If the user is in a user scope, create the config path under `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md`.

## After writing

**Show what this plugin can do.** Before closing, offer:

> **Want to see what I can help with?**

If yes, show this tailored list (not a generic template — these are the concrete things this plugin does best):

> **Here's what I'm good at in privacy practice:**
>
> - **Ingest new data against your wiki** — e.g., "Automatically reads from raw_sources and updates the wiki." Try: `/company-brain:ingest`
> - **Query data against your wiki** — e.g., "Query against your wiki to provide information." Try: `/company-brain:query`
> - **Lint against your wiki** — e.g., "Check and lint your wiki." Try: `/company-brain:lint`
>
> - **Whitespace Agent** — e.g., "Once filled some information do some resarch with the whitespace agent." Try: `find white space, what should we pitch next, heat map gaps, qualify new opportunities`


1. **Show the summary.** 
   > "Done. Your practice profile is at `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` — a plain text file you can read and edit directly. Here's a summary of what you told me:"
   >
   > - Company name: [company name]
   > - Industry: [industry]
   > - WebPage: [webpage]
   > - Size: [size]
   > - Regulated: [regulators]

2. **Close with the "you can change anything later" note:**

   > "Your practice profile is at `~/.claude/plugins/config/company-brain-4-sellers-marketplace/company-brain/CLAUDE.md` — a plain text file you can read and edit directly. Anything you answered can be changed:
   >
   > - Edit the file directly for a quick change
   > - Run `/company-brain:cold-start-setup --redo` for a full re-interview
   >




