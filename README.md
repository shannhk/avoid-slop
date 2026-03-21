<p align="center">
  <img src="banner.png" alt="Avoid Slop" width="100%">
</p>

# Avoid Slop

A curated directory of open-source tools and techniques for eliminating AI-generated slop from text, code, and design.

AI models have defaults they collapse toward — the same phrases, the same layouts, the same color palettes. These tools fight that.

---

## The Tools

### [stop-slop](https://github.com/hardikpandya/stop-slop)

A skill file for removing AI tells from prose.

| | |
|---|---|
| **Author** | Hardik Pandya |
| **Stars** | 2,100+ |
| **License** | MIT |
| **Domain** | Written prose |
| **Format** | Claude skill (Markdown) |

**What it does:** Provides ~30 banned phrases across 7 categories (throat-clearing openers, emphasis crutches, business jargon, adverbs, meta-commentary), 8 banned structural patterns, and a 5-dimension scoring rubric that triggers revision when writing scores below 35/50.

**How to use it:** Drop the skill file into Claude Projects, custom instructions, or API system prompts. Works immediately — no build step, no dependencies.

**Sharpest idea:** "False agency" detection. AI gives inanimate things human verbs ("the data tells us", "the market rewards") to avoid naming actual actors. Naming the human fixes it.

**Notable rule:** Em-dashes are categorically banned. Not "use sparingly" — banned.

---

### [unslop](https://github.com/mshumer/unslop)

Empirically detects a model's default patterns, then generates a custom avoidance profile.

| | |
|---|---|
| **Author** | Matt Shumer |
| **Stars** | 180+ |
| **License** | MIT |
| **Domain** | Any (text, visual, code) |
| **Format** | Python CLI tool |

**What it does:** Generates 50+ domain-specific outputs from a model, statistically analyzes them for recurring defaults, and writes a custom `skill.md` that tells the model what to avoid. Visual mode screenshots HTML outputs to catch CSS/layout/color cliches too.

**How to use it:** Clone the repo, set up a Python venv, run `python3 unslop.py --domain "blog writing"`. Ships with prebuilt profiles for writing and React design.

**Sharpest idea:** Self-bootstrapping — Claude analyzes its own corpus to find its own defaults. Empirical over editorial. No human has to guess which patterns are overused; the data shows it.

**Key principle:** Anti-prescription. Telling a model to write "better" just creates a new flavor of slop. The right fix is listing what *not* to do, which forces genuine novelty rather than template substitution.

---

### [impeccable](https://github.com/pbakaus/impeccable)

A design language and command toolkit that makes AI-generated frontends look human-designed.

| | |
|---|---|
| **Author** | Paul Bakaus |
| **Stars** | 11,700+ |
| **License** | Apache 2.0 |
| **Domain** | Frontend UI/UX |
| **Format** | Multi-provider skill system (21 commands) |

**What it does:** Loads domain-specific design expertise (typography, color theory, spatial design, motion, interaction design) as persistent LLM context. Provides 20 slash commands (`/audit`, `/polish`, `/critique`, `/bolder`, `/quieter`, `/colorize`, `/animate`, `/overdrive`) that act as steering verbs for design quality. The `/critique` command runs an explicit "AI Slop Detection" check as its first-pass evaluation.

**How to use it:** Install from [impeccable.style](https://impeccable.style) or copy from the repo. Works with Claude Code, Cursor, Gemini CLI, Codex CLI, VS Code Copilot, and more.

**Sharpest idea:** The distinctiveness test — "Would a viewer immediately identify this as AI-made?" proposed as a concrete design quality metric, not a vibe check.

**Notable technical rule:** Stop using HSL. Use OKLCH. Pure gray is a mistake — add 0.01 chroma of your brand hue to all neutrals for subconscious cohesion.

---

## Comparison

| | stop-slop | unslop | impeccable |
|---|---|---|---|
| **Domain** | Written prose | Any (text, visual, code) | Frontend UI/UX |
| **Approach** | Curated editorial rules | Empirical detection + profiling | Design expertise injection |
| **Setup effort** | Drop-in (copy a file) | CLI workflow (Python) | Install or copy skills |
| **Customization** | Edit the rules by hand | Auto-generates per domain | `/teach-impeccable` creates project context |
| **Philosophy** | Ban the bad patterns | Measure defaults, suppress them | Inject enough knowledge to choose well |
| **Best for** | Writers, content teams | Building domain-specific profiles | Developers shipping frontend |

## What They Agree On

All three identify the same root cause: **LLMs collapse to defaults**. They attack it differently — editorial rules, empirical measurement, or expertise injection — but share one conviction: prescribing a "better" style just creates new slop. The fix is either removing defaults or adding enough context that the model can make genuinely informed choices.

---

## Contributing

Know of another tool, technique, or resource for fighting AI slop? Open a PR or issue. The bar: it should be open-source, actively maintained, and take a specific, opinionated stance rather than offering generic "write better" advice.

## License

MIT
