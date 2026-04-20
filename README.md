<div align="center">

# Novel Flow / 小说流

[![Trae](https://img.shields.io/badge/Built%20for-Trae-blue)](https://trae.ai)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Skills](https://img.shields.io/badge/Skills-6-purple)](#features)
[![Styles](https://img.shields.io/badge/Styles-3-orange)](#writing-styles)

**AI-Powered Long-Form Novel Writing System**

6 collaborative Skills covering the full pipeline from idea to final draft.
De-AI · Style Engine · Structured Review · Anti-Drift

**[中文](README_zh.md)**

</div>

---

## Quick Start

**Trae users:** Copy the `skills` and `shared` folders into your project's `.trae` directory.

```
your-project/
└── .trae/
    ├── skills/     ← copy here
    └── shared/     ← copy here
```

**Other AI tools:** Tell your AI:
```
Install this skill: https://github.com/ZhangDongyang800/novel-flow-one-by-one.git
```

## Workflow

1. Tell AI your idea (anything works, even just the word "novel"). AI asks you genre, protagonist, world-building etc. — you just pick options (A or B)
2. Confirm the generated `project.md` (project settings) and character cards
3. AI auto-generates chapter outline `outline.md`, you confirm the chapter plan
4. AI writes prose scene by scene, auto-checking for AI-isms and formatting every 300-500 words
5. After you confirm the draft, AI runs a 6-dimension review (plot progress, character change, memorable moments, pacing, emotion, hooks)
6. Review passes → auto-sync setting changes → write next chapter; fails → revise and re-review

## Writing Styles

| Style | Best For | Core Traits |
| :---: | --- | --- |
| **Cold Minimalist** | Realism, historical, mystery, war | Restrained, emotionally subtle |
| **System Power Fantasy** | LitRPG, progression, urban, xianxia | Tension → reversal → payoff, face-slapping |
| **Weird Suspense** | Rule-based horror, infinite flow, Cthulhu, mind games | Rule design, information asymmetry, cognitive intrusion |

## Directory Structure

```
novel-flow/
├── skills/
│   ├── novel-orchestrator/   # Orchestration
│   ├── novel-brainstorm/     # Ideation & convergence
│   │   └── templates/        # project.md · character card
│   ├── novel-outline/        # Chapter planning
│   │   └── templates/        # outline.md
│   ├── novel-draft/          # Scene-by-scene writing
│   │   ├── templates/        # guide.md · chapter-xxx.md
│   │   └── styles/           # Cold Minimalist · System Power Fantasy · Weird Suspense
│   ├── novel-review/         # 6-dimension review
│   └── novel-update/         # Setting sync
└── shared/
    ├── file-contracts.md     # File contracts (data dictionary)
    └── state-rules.md        # State transition rules
```

## FAQ

**Q: AI didn't activate the skill and just wrote directly.**
A: Make sure the `skills/` and `shared/` folders are placed directly under `.trae/`, not nested inside another folder. The path must be `.trae/skills/novel-orchestrator/SKILL.md`.

**Q: The generated text still has an "AI flavor".**
A: This is normal. AI models have inherent writing patterns. The skill system significantly reduces AI-isms through rules and self-checks, but can't eliminate them 100%. When you spot AI-isms, point them out — the review skill will catch and fix them.

**Q: Math/logic errors in the text (e.g., wrong interest calculations).**
A: AI models are weak at math. The skill includes a "verify calculations" rule, but it's not foolproof. Double-check any numbers in the output yourself.

**Q: Chapter endings feel repetitive.**
A: The skill now includes a "reader perspective re-read" self-check that catches repetition. If it still happens, tell the AI directly: "This ending is too similar to the last chapter, change it."

**Q: The story drifts from the original setting.**
A: The update skill auto-syncs setting changes after each chapter. If drift still occurs, check `project.md` — the AI may have silently changed settings without recording them.

**Q: Brainstorm asks too many questions.**
A: You can say "skip" or "I don't care about this" at any step. The system will use a default and move on.

## License

[MIT](LICENSE)
