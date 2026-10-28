# Standards Skills — Expertise-as-Skills

AI agent skills that make the agent an **instant expert on published engineering standards**. Each skill encodes the full content of one standard — procedures, symbols, formulas, tables, worked examples — not just pointers to it. On installation the agent internalises the standard's methodology and can perform the analysis exactly as the standard prescribes.

## The standards

| Skill ID | Standard | Domain | Expertise encoded |
|---|---|---|---|
| [`iec-61025`](skills/iec-61025/SKILL.md) | IEC 61025:2006 (2nd ed.) | Fault Tree Analysis (FTA) | Qualitative/quantitative methods, all event/gate symbols with exact formulas, immediate-cause construction, Boolean reduction, minimal cut sets, Annex B disjointing, labelling rules, report requirements |
| [`mil-std-882e`](skills/mil-std-882e/SKILL.md) | MIL-STD-882E (with Change 1, 2023) | System Safety | 8-element process, 25 tasks with what each requires, severity/probability/RAC matrices, design order of precedence, software safety (SCC→SwCI→LOR), HTS data elements, risk acceptance, tailoring |
| [`nureg-0492`](skills/nureg-0492/SKILL.md) | Fault Tree Handbook (US NRC, 1981, 210 pp) | Fault Tree Analysis (in-depth methodology) | Five ground rules, fault taxonomy, Boolean/probability foundations, Shannon expansion, cut-set quantification with exact equations Table XI-2/XI-3, importances, common cause, pressure-tank and three-motor examples, WASH-1400 data |

## Why these formats

Skills are plain `SKILL.md` files with `name`/`description` frontmatter — the de-facto portable skills format supported by:

- **OpenCode** — install globally under `~/.config/opencode/skills/`, or use the HTTP catalog below
- **Claude Code / Claude apps** — copy to `~/.claude/skills/` or `.claude/skills/`
- **Agents-emitting tools** (`agents.md` ecosystem) — copy to `.agents/skills/`
- Any agent that can read files: point it at `references/` and load `SKILL.md`

## Install (OpenCode)

### One-liner — HTTP catalog
Add to any `opencode.json` / `opencode.jsonc` (global or project):

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": ["https://raw.githubusercontent.com/strangerx003/standards-skills/master/skills/"]
}
```

### Manual
```bash
opencode skill install standards-skills    # if you publish via the CLI
# or copy:
git clone https://github.com/strangerx003/standards-skills
cp -r skills/* ~/.config/opencode/skills/   # global, all standards
cp -r skills/iec-61025 ~/.config/opencode/skills/   # just one standard
```

## Install (Claude)
```bash
cp -r skills/* ~/.claude/skills/
```

## Install (any agent)
Give the agent this instruction:
> Load and internalise `skills/<standard>/SKILL.md`, then read `skills/<standard>/reference/*.md` fully before answering anything about that standard.

## Local development (this working copy)

`opencode.json` in this folder registers `./skills` as a source, so the skills auto-load whenever you work from this directory. The original PDFs stay at the repo root as ground truth.

## Verify an install

After installing, ask the agent:

| Ask | Expert answer must contain |
|---|---|
| "Series system → which IEC 61025 gate and formula?" | OR gate, F_S = 1 − ∏(1−Fᵢ) |
| "Can PPE alone close out a Catastrophic MIL-STD-882E hazard?" | No — severity 1 requires design-level mitigation; PPE is last in precedence, cannot reach level F |
| "Give me the NUREG-0492 ground rules." | All five: fault written with what/when, component-vs-system rule, no miracles, complete-the-gate, no gate-to-gate |

## Contributing a new standard

1. Drop the PDF in the repo root.
2. Extract text (`pypdf`) or OCR (`pypdfium2` + `tesseract`, see `.claude`-style workflow in git history).
3. Read the full document, then write `skills/<id>/SKILL.md` (when-to-use, hard rules, workflow) + `skills/<id>/reference/<id>.md` (complete structured summary with equations/tables).
4. Update `index.json` (bump `version`) and the table in this README.
