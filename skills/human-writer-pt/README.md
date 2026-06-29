# Human Writer — Brazilian Portuguese (pt) — a Claude skill

A Claude Code skill that produces **Brazilian Portuguese (pt-BR)** prose reading as human-authored, sanitizes pt-BR AI drafts to remove detector tells, and scores any pt-BR draft for AI-detection risk before publication.

This is the **Brazilian Portuguese member** of the `human-writer` per-language family — one autonomous skill per language (`en`, `fr`, `es`, `pt`, `de`, `ar`, `hi`), all built on the same architecture. They install side by side and do not conflict: each activates on its own language triggers.

## Why this skill exists

`mr-bridge.com` ships localized marketing and editorial copy in Brazilian Portuguese (`ogLocale: pt_BR`). Modern Sonnet / Opus / GPT-class pt-BR output is fluent enough to ship, but it carries fingerprints that commercial detectors (Copyleaks, GPTZero, Originality.ai) latch onto, and pt-BR carries its own tells a bare statistical detector never checks:

- **Statistical:** low burstiness, narrow type-token ratio (language-agnostic).
- **Stylistic:** the same forty or fifty inflated words repeated across drafts ("vale ressaltar", "sem dúvida", "alavancar", "robusto"), formulaic frames ("Não se trata apenas de X, mas de Y").
- **Typographic (pt-BR-specific):** an entire file emitted with its accents stripped (ç ã õ á é í ó ú â ê dropped), Anglo spaced em-dashes "—" used where native Portuguese uses commas or the dialogue travessão, EN→pt calques ("sem emendas", "acionável", "deletar", "navegar por").

A draft drops, a reviewer runs it through a detector, the score comes back at 70%+, and it's rejected. The fix is a disciplined sweep of the specific pt-BR tells detectors weight. This skill encodes that doctrine plus a deterministic analyzer so any Claude Code session can produce, clean, or audit pt-BR prose to a target score before delivery.

## What it can do

**Three modes:**
- **Write (escrever):** produce new pt-BR content already engineered to score LOW_RISK.
- **Clean (limpar):** rewrite an existing pt-BR AI draft to strip tells, preserving meaning.
- **Audit (auditar):** score a pt-BR draft, surface the top offending tells, recommend fixes without rewriting it.

**One language, fully specialized:**
- **Brazilian Portuguese (pt):** ~170-entry suspect vocabulary (Tier 1 + Tier 2), pt-BR AI-construction regex bank, Portuguese tricolon detector (`e` conjunction), and a dedicated **accent-stripping** typography detector — calibrated NOT to false-fire on clean native prose or short accent-sparse snippets.

**Four content-types** (each with its own adapter): marketing long-form, short-comms, technical, editorial-SEO.

**Optional external integration:** live scoring via Copyleaks, GPTZero, or Originality.ai (`--external <provider>`). Lazy `httpx` import, so the analyzer works fully offline.

## What's inside

```
human-writer-pt/
├── SKILL.md                          # Orchestration hub: routing + master checklist + anti-patterns (pt)
├── README.md                         # This file
├── INSTALL.md                        # Installation instructions
├── requirements.txt                  # pyyaml (required) + httpx (optional) — only for --external mode
├── references/
│   ├── tells-stylistic-pt.md         # ⭐ CORE: pt suspect vocab + AI constructions + accent-stripping + calques
│   ├── tells-statistical.md          # burstiness / TTR (language-agnostic)
│   ├── tells-structural.md           # bullets / headers / tricolons / emoji
│   ├── humanization-techniques.md    # the ten humanization moves (Portuguese worked examples)
│   ├── adapter-marketing.md          # marketing long-form adapter
│   ├── adapter-short-comms.md        # short-form comms adapter
│   ├── adapter-technical.md          # technical-docs adapter (prose-only contract)
│   ├── adapter-editorial-seo.md      # editorial-SEO adapter
│   ├── external-detectors.md         # Copyleaks / GPTZero / Originality.ai integration notes
│   └── checklists.md                 # pre-publish checklists + pt-BR quick-triage
└── scripts/
    ├── rules.yaml                    # ⭐ pt: vocab + constructions + thresholds (incl. min_accent_ratio)
    └── analyze.py                    # ⭐ pt-adapted: tricolon (e) + detect_accent_stripping
```

## Installation

See `INSTALL.md`. TL;DR for macOS/Linux:

```bash
mkdir -p ~/.claude/skills
unzip human-writer-pt.zip -d ~/.claude/skills/
pip install --user -r ~/.claude/skills/human-writer-pt/requirements.txt
```

## How to invoke

Once installed, the skill auto-activates on Brazilian Portuguese prose requests. Example prompts:

- "Escreva um artigo de 600 palavras sobre precificação de vinhos de guarda, que soe humano, não como IA"
- "Limpe este rascunho de IA para baixar a pontuação do Copyleaks abaixo de 25"
- "Audite este e-mail em português para detectar tells de IA antes de enviar"
- "Humanize este texto, está soando demais como ChatGPT"
- "Make this Portuguese landing-page copy read human, not AI"

If auto-activation misses, force it: "Use the `human-writer-pt` skill to..."

## The analyzer

`scripts/analyze.py` is a deterministic scorer that runs offline. It loads `scripts/rules.yaml` (Portuguese vocab lists, regex patterns, thresholds) and emits a 0-100 score plus a list of flagged tells.

```bash
# Audit mode (default, JSON output for tooling)
python3 scripts/analyze.py --input draft.md --lang pt --type marketing

# Human-readable report
python3 scripts/analyze.py --input draft.md --lang pt --type editorial-seo --format human

# Pipe via stdin
cat draft.md | python3 scripts/analyze.py --lang pt --type technical --format human
```

Required flags: `--lang pt`, `--type` (`marketing` / `short-comms` / `technical` / `editorial-seo`). `--input` is optional; stdin otherwise.

**Score bands** (4-band YAML, canonical):
- `0-24` **LOW_RISK:** ship it.
- `25-49` **MEDIUM_RISK:** apply the top 3 recommendations, re-score.
- `50-74` **HIGH_RISK:** in WRITE mode restart; in CLEAN mode apply a stronger rewrite.
- `75-100` **CRITICAL:** major rewrite.

**Detectors implemented:** em-dash density, sentence-length stdev (burstiness), TTR (lexical diversity), Portuguese suspect-vocabulary, Portuguese AI-construction regex bank, Portuguese tricolon (`e`), bullet parallelism, header pyramid, and the pt-BR-only **accent-stripping** detector (low-weight, word-count-guarded, register-calibrated).

**Prose-only scoring.** The analyzer strips fenced code blocks, markdown data tables, and opt-in ignore regions before scoring. Wrap any intentionally AI-flavored citation so it doesn't count against you:

```
<!-- human-writer:ignore-start (citação de mau exemplo) -->
No mundo atual, vale ressaltar soluções robustas e sem emendas.
<!-- human-writer:ignore-end -->
```

## What's NOT inside

- **English / French / Spanish / German / Arabic / Hindi content:** use the matching `human-writer-<lang>` family member.
- **Document structure** (which sections, which schemas, which headings): use a dedicated structure/content tool. This skill is the stylistic filter applied on top of whatever produces the structure.
- **Technical SEO audit of a web project:** use a dedicated SEO tool. This skill handles content style only.

This skill is a stylistic filter invoked on top of structure-producing tools, never as a replacement.

## Part of the mr-bridge.com toolkit

This skill is part of the [mr-bridge.com](https://mr-bridge.com) toolkit for scraping, data, and content automation. Related resources:

- [mr-bridge.com](https://mr-bridge.com) — home
- [Scrapers](https://mr-bridge.com/scrapers) — the Apify Actor portfolio
- [MCP servers](https://mr-bridge.com/mcp-servers) — Model Context Protocol servers
- [AI workflows](https://mr-bridge.com/ai-workflows) — agents and automation
- [Studies](https://mr-bridge.com/studies) — data studies and one-pagers
- [Articles](https://mr-bridge.com/articles) — write-ups and guides
- [Solutions](https://mr-bridge.com/solutions) — end-to-end solutions

## License

Personal use. Customize freely. No warranty. The external-detector endpoints in `analyze.py` are language-agnostic POSTs and carry `# (verify)` markers; they were not re-verified for Portuguese specifically.
