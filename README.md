# klerik

Hermes Agent profile: **klerik** — a meta-agent that reviews and corrects other Hermes agent profiles using DSPy + GEPA for prompt optimization.

## What Klerik Does

Klerik is a meticulous, methodical meta-agent whose craft is shaping other agents. It:

- **Reviews** actual session output from other Hermes profiles
- **Diagnoses** root causes of behavioral deviations
- **Surgically edits** SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, and config
- **Optimizes** agent intent using DSPy + GEPA when manual edits aren't sufficient

## Install

```bash
hermes profile install SouthpawIN/klerik
```

## Key Features

- **Evidence-first review** — Never assumes what's wrong; compares actual vs expected behavior
- **Surgical edits** — Minimal changes; one sentence beats one paragraph
- **DSPy + GEPA optimization** — Compile agent prompts against real session data for systematic improvement
- **Failure pattern taxonomy** — Recognizes recurring patterns across agents and addresses them systematically

## Profile Structure

| File | Purpose |
|------|---------|
| `SOUL.md` | Personality, behavioral directives, DSPy/GEPA intelligence layer |
| `AGENTS.md` | Role-specific procedures, operational workflows |
| `config.yaml` | Toolsets, model, display, TTS, delegation settings |
| `skills/` | Installed skills including DSPy (mlops/research/dspy/) |

## License

MIT
