<p align="center">
  <img src="banner.png" alt="Avoid Slop" width="100%">
</p>

Open-source tools for eliminating AI-generated slop from text, code, and design.

AI models have defaults they collapse toward. The same phrases, the same layouts, the same color palettes. These tools fight that.

Writing skills below follow the ranking in [Juampi's roundup](https://x.com/juampitech/status/2090834948332655011). Code and design tools sit in a separate section.

---

## Writing

### [stop-slop](https://github.com/hardikpandya/stop-slop)

A skill file for removing AI tells from prose. By Hardik Pandya. MIT. 16,200+ stars.

> About 30 banned phrases across 7 categories (throat-clearing openers, emphasis crutches, business jargon, adverbs, meta-commentary), 8 banned structural patterns, and a scoring rubric that triggers revision when writing scores below 35/50.

Drop the skill file into Claude Projects, custom instructions, or API system prompts. No build step, no dependencies.

The best idea in here is "false agency" detection. AI gives inanimate things human verbs ("the data tells us", "the market rewards") to avoid naming actual actors. Naming the human fixes it.

Em-dashes are categorically banned. Not "use sparingly." Banned.

---

### [no-ai-slop](https://github.com/petergyang/no-ai-slop)

Removes 20+ patterns of AI slop without flattening the writer's voice. By Peter Yang. MIT. 5,800+ stars.

> Catches binary contrasts ("It's not X. It's Y."), throat-clearing openers, faux-insight setups, colon reveals, dramatic fragments, weasel attribution, synonym cycling, and fake-profound endings. Two jobs: edit the draft, or detect patterns without rewriting.

`npx skills add petergyang/no-ai-slop --skill no-ai-slop --global --yes`

The detect mode is the standout. It names each pattern, quotes the line, and gives the fix in a few words. It does not guess whether AI wrote the text. Detectors guess. Named patterns are evidence you can check.

It treats voice preservation as a first-class job, not a footnote. The usual failure of these skills is turning distinctive writing into generic polished prose. This one is built to avoid that.

---

### [humanizer](https://github.com/blader/humanizer)

An agent skill that removes signs of AI-generated writing from text. By blader. MIT. 37,400+ stars.

> Based on Wikipedia's "Signs of AI writing" guide, maintained by WikiProject AI Cleanup. Covers 25 pattern categories: inflated significance, promotional language, superficial -ing analyses, vague attributions, AI vocabulary words, em dash overuse, rule of three, negative parallelisms, sycophantic tone, filler phrases, and more.

`npx skills add blader/humanizer@humanizer -g -y` or clone directly into your skills directory. Works as a slash command (`/humanizer`) in Claude Code and other agents.

What sets it apart from a simple word blocklist: it runs a two-pass audit. First rewrite, then it asks "what makes this obviously AI generated?" about its own output and revises again. The self-critique loop catches patterns that survive the first edit.

Also pushes you to add voice, not just remove slop. Sterile, voiceless writing is just as obvious as the bad patterns. The skill explicitly checks for opinions, varied rhythm, and first-person perspective where appropriate.

---

### [unslop](https://github.com/cursor/plugins) (Cursor)

The writing skill from Cursor's official plugins, originally by Lauren Tan ([@poteto](https://x.com/poteto)). 6,100+ installs.

> Scan, rewrite, add soul, then self-audit. Pattern catalog covers significance inflation, promotional language, AI vocabulary, copula avoidance, negative parallelisms, rule of three, em dash overuse, chatbot phrases, and abstract metaphor nouns ("substrate", "wedge", "vector").

`npx skills add https://github.com/cursor/plugins --skill unslop`

"Adding soul" is the distinctive step. Removing patterns is half the job. The skill then forces opinions, varied rhythm, first person, and specific detail so the rewrite does not collapse into voiceless clean prose.

Different tool from [Matt Shumer's unslop](#unslop-empirical-profiler) below. This one edits a draft. That one profiles a model's defaults.

---

### [slopbeth](https://github.com/ehmo/slopkit)

A writing skill that cuts AI tells without changing what the draft can honestly claim. By Rasty Turek. MIT. 80+ stars. Lives in [slopkit](https://github.com/ehmo/slopkit) next to **slopgent**, which cleans the agent's own status reports.

> Source-locked rewrites: named entities, numbers, dates, URLs, citations, and technical claims stay put. Unsupported uplift ("faster decisions", "better alignment") becomes a proof gap, a question, or an attributed claim. Ships an 88-case corpus and judge panels, not only a banned-word list.

`npx skills add ehmo/slopkit --skill slopbeth`

The useful split: slopbeth edits the document you hand over. slopgent shapes what the agent tells *you* while it works. Point the wrong skill at the wrong text and you get clipped formula prose, or a build narration with nothing to preserve.

Most humanizer skills turn slop into cleaner slop. slopbeth's bet is density plus evidence. Every sentence has to carry a claim, example, constraint, number, or argumentative move.

---

### [humanizer](https://github.com/Aboudjem/humanizer-skill) (Adam Boudjemaa)

Pattern detector and rewriter with a 0-100 AI-tell score. By Adam Boudjemaa. MIT. 180+ stars.

> 53 numbered patterns, 5 voice profiles (casual, professional, technical, warm, blunt), and three modes: detect, rewrite, edit. Burstiness (sentence-length variation) and perplexity sit at the center of the method. Pure Markdown. No network calls.

`npx skills add Aboudjem/humanizer-skill`

The score is the useful extra. You get a number and the patterns that produced it, so you can measure before and after instead of trusting a vibe check. Optional Node CLI and CI gate compute the same signals without an LLM.

Voice profiles change rhythm, not just a few words. That is a different bet from skills that only delete tells.

---

### [deslop](https://github.com/stephenturner/skill-deslop)

A Claude skill for removing AI writing patterns from prose, weighted toward scientific writing. By Stephen Turner. MIT. 350+ stars.

> Filler phrases, formulaic structures, false agency, dramatic fragmentation, vague declaratives, plus a 1-10 rubric across directness, rhythm, trust, authenticity, and density. Below 35/50: revise. Accounts for conventions like passive voice in methods sections.

Copy `SKILL.md` and `references/` into your skills directory, or build a `.skill` file from the repo.

Built by combining [tropes.fyi](https://tropes.fyi/) with [stop-slop](https://github.com/hardikpandya/stop-slop). The scientific-writing bias is the reason to pick it over a generic prose skill: it will not "fix" passive voice in a methods section just because other skills ban it.

---

### [anti-slop](https://github.com/elithrar/dotfiles/tree/main/.agents/skills/anti-slop) (elithrar)

A review skill that removes machine-authorship tells while preserving the author's voice. By elithrar. MIT. Lives in [elithrar/dotfiles](https://github.com/elithrar/dotfiles).

> Prime directive: decide slop vs voice before deleting anything. A false positive that flattens a good sentence is worse than one surviving tell. Surgical phrasing edits only. Do not restructure paragraphs or change meaning unless asked.

`npx skills add https://github.com/elithrar/dotfiles --skill anti-slop`

The catalog names tells most lists miss: demonstrative kickers ("That instinct backfires."), importance-flagging ("This matters."), clever metaphor flourishes, correlative bloat. It also names what to keep: earned fragments, deliberate parallelism, a strong closing line, first-person conviction the author would defend.

This is the conservative editor in the set. Change phrasing, not substance.

---

### [humanize](https://github.com/aashaexo/soundshuman)

A merger of rewrite skill, machine-readable rules, and a zero-dependency CLI. By aashaexo. MIT. 270+ stars.

> 41 patterns from Wikipedia / humanizer, stop-slop structural rules, and brandonwise/humanizer's statistical tells. Detection lives in a versioned JSON rule pack. `sloplint` scores text 0-100, applies safe mechanical fixes, scans a docs folder, and gates CI.

`npx skills add https://github.com/aashaexo/soundshuman --skill humanize`

The CLI is the distinctive piece. Most of these tools only work inside an agent session. `sloplint scan docs/ --fail-above 50` is a repo gate you can run in CI without an LLM. Rules as data means a house rule is a one-line diff, not a prompt rewrite.

---

### [anti-ai-slop-writing](https://github.com/jalaalrd/anti-ai-slop-writing)

Generation-time constraints that force human-sounding text before a draft exists. By Jalaaldeen. MIT. 400+ stars.

> 50+ banned words, 35+ banned phrases, 16 banned sentence openers, 10 structural patterns, plus punctuation and formatting leaks. Based on Carnegie Mellon (2025), Wikipedia's Signs of AI Writing, Buffer's 52M post analysis, and community detection patterns.

`npx skills add https://github.com/jalaalrd/anti-ai-slop-writing --skill anti-ai-slop-writing`

Most skills in this list are editors. This one is a writing directive: load the banned list, then never use those words. The structural rules that matter: no default rule of three, no three consecutive sentences of the same length, no parataxis (short sentence. Then another. Then another.).

Uniform sentence length is treated as the single most measurable detection signal.

---

### [Zero Slop](https://github.com/manavmishra/ZeroSlop)

Scores a draft 0-100 for AI slop, then edits it under a fact gate that can reject the rewrite. By Manav Mishra. MIT. 13 stars.

> 290 weighted patterns and a 96-term lexicon: binary contrasts, throat-clearing openers, faux-insight setups, colon reveals, dramatic fragments, importance puffery, weasel attribution, synonym cycling, and marketing riders that only score beside a marketing trigger. A separate reading pass covers document-level defects no span pattern reaches: one sentence shape repeated seven times, statistics piled into a paragraph, paragraphs that shuffle without loss.

`npx skills add manavmishra/ZeroSlop --global`

The distinctive part is that the fact gate is a program, not an instruction. Any rewrite that adds or drops a name, number, quotation, link, code block, table or path is rejected and redone. The model is never trusted to have preserved the facts; a local check decides, and it fails the pass rather than warning.

The score is deliberately not a detector, and the README keeps saying so. Human writing in its own corpus scores 9 to 21 and unedited AI drafts average 77, but neither number identifies who wrote anything. Eight editorial roles run as separate passes so nothing grades its own output.

Everything local runs offline on Python's standard library. No account, no network call. `slopscore.py --batch drafts/ --gate 25` fails a build above the threshold, so it works as a CI check rather than only an interactive skill.

The repo also publishes a same-model replay against several tools in this list. Drafts, mappings and hashes are committed, so it can be rerun and disputed. It is self-run, so read it as a regression study and not an independent ranking.

---

## Code and design

### [unslop](https://github.com/mshumer/unslop) (empirical profiler)

Detects a model's default patterns empirically, then generates a custom avoidance profile. By Matt Shumer. MIT. 520+ stars.

> Generates 50+ domain-specific outputs from a model, runs statistical analysis on recurring defaults, and writes a custom `skill.md` telling the model what to avoid. Visual mode screenshots HTML outputs to catch CSS/layout/color cliches too.

Clone the repo, set up a Python venv, run `python3 unslop.py --domain "blog writing"`. Ships with prebuilt profiles for writing and React design.

The clever part: Claude analyzes its own corpus to find its own defaults. No human has to guess which patterns are overused. The data shows it.

The philosophy is anti-prescription. Telling a model to write "better" just creates a new flavor of slop. Listing what *not* to do forces novelty rather than template substitution.

---

### [impeccable](https://github.com/pbakaus/impeccable)

A design language and command toolkit for making AI-generated frontends look human-designed. By Paul Bakaus. Apache 2.0. 62,000+ stars.

> Loads design expertise (typography, color theory, spatial design, motion, interaction design) as persistent LLM context. Has 20 slash commands (`/audit`, `/polish`, `/critique`, `/bolder`, `/quieter`, `/colorize`, `/animate`, `/overdrive`) for steering design quality. The `/critique` command runs an "AI Slop Detection" check as its first pass.

Install from [impeccable.style](https://impeccable.style) or copy from the repo. Works with Claude Code, Cursor, Gemini CLI, Codex CLI, VS Code Copilot, and more.

The distinctiveness test is the standout idea: "Would a viewer immediately identify this as AI-made?" as a concrete quality metric, not a vibe check.

Worth noting: stop using HSL. Use OKLCH. Pure gray is a mistake. Add 0.01 chroma of your brand hue to all neutrals for subconscious cohesion.

---

### [anti-slop](https://github.com/dmmulroy/anti-slop) (Oxlint)

Opinionated Oxlint rules that reject low-evidence TypeScript and JavaScript patterns. By Dillon Mulroy. MIT. 3,500+ stars. Flagged in [the same thread](https://x.com/sec0ndstate/status/2090863864338374966) as missing from the writing-skill ranking.

> Vendored plugin, not a pinned npm dependency. Generic rules catch chained type assertions, known-value widening, `unknown` laundering, module mocks, `Reflect.get` / `Reflect.apply`, ad hoc `typeof` narrowing, and assertions without a safety comment. Optional Effect rule group.

`npx skills add dmmulroy/anti-slop --skill install-anti-slop`

This is code slop, not prose slop. Agents fabricate type evidence (`input as object as User`), spread empty objects to omit fields, and widen a known value so they can assert it back. The linter makes those patterns fail the build.

Meant to be copied into the repo and owned. Read the rules. Change them.

---

## Comparison

| Tool | Domain | Approach | Distinctive idea |
|---|---|---|---|
| stop-slop | Prose | Banned phrases + structures + rubric | False agency; em dashes banned |
| no-ai-slop | Prose | Edit or detect, preserve voice | Named patterns as evidence, not a detector score |
| humanizer (blader) | Prose | Pattern catalog + two-pass self-audit | Rewrite, then ask what still sounds like AI |
| unslop (Cursor) | Prose | Scan, rewrite, add soul, self-audit | Soul pass so clean prose does not stay voiceless |
| slopbeth | Prose | Source-locked rewrite + benchmarks | Keep every sourced fact; cut unsupported uplift |
| humanizer (Boudjemaa) | Prose | 53 patterns, 5 voices, 0-100 score | Burstiness as a measurable tell |
| deslop | Prose / science | stop-slop + tropes.fyi, scientific defaults | Passive voice allowed in methods |
| anti-slop (elithrar) | Prose | Surgical review, slop vs voice | False positive that flattens is worse than a leftover tell |
| humanize (soundshuman) | Prose + CI | Skill + JSON rules + `sloplint` | Repo-wide score and CI gate, no LLM required |
| anti-ai-slop-writing | Prose | Generation-time bans | Constraints before the draft, not after |
| Zero Slop | Prose | 0-100 score, fact gate, reading pass | Rewrite is rejected if a name or number moves |
| unslop (Shumer) | Text, visual, code | Empirical profiling | Measure the model's defaults, then suppress them |
| impeccable | Frontend UI/UX | Design expertise injection | "Would a viewer identify this as AI-made?" |
| anti-slop (Oxlint) | TypeScript / JS | Vendored lint rules | Reject type laundering at compile time |

## What they agree on

These tools identify the same problem: LLMs collapse to defaults. They attack it differently, but share one conviction: prescribing a "better" style just creates new slop. The fix is either removing defaults, adding enough context that the model can choose, or making the bad pattern fail a check.

Sterile, voiceless output is its own tell. Deleting "delve" is not enough.

---

## Contributing

Know of another tool or technique for fighting AI slop? Open a PR or issue. The bar: open-source, actively maintained, and takes a specific, opinionated stance rather than offering generic "write better" advice.

## License

MIT
