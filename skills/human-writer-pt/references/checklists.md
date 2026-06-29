# Pre-Publish Checklists (human-writer-pt)

> Ready-to-paste self-review checklists, one per content-type, for Brazilian Portuguese prose. Run `analyze.py --lang pt` first, then walk through the relevant checklist before delivery. Each checklist is short, actionable, and covers the tells most likely to trigger AI detectors for that specific format. The pt-BR quick-triage at the end is the Brazilian-Portuguese-specific addition.

---

## Marketing Long-Form

Before publishing blogs, READMEs, landing pages, or long-form newsletters in Portuguese, confirm:

- [ ] Analyzer score ≤ 24 with `--lang pt --type marketing`
- [ ] First 100 words contain zero Tier-1 suspect vocabulary
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] First paragraph does not open with "No mundo atual", "Na era digital", "Vale ressaltar", or "Seja você X ou Y"
- [ ] Closing paragraph does not start with "Em conclusão", "Em suma", "Em última análise", "Por fim", or "Em resumo"
<!-- human-writer:ignore-end -->
- [ ] Em-dash count ≤ 1 per 1000 words (run `analyze.py` to check); only genuine dialogue travessões allowed
- [ ] File is properly accented (ç ã õ á é í ó ô õ ú â ê) — no stripped-accent prose
- [ ] At least one specific number, named entity, or first-person opinion per ~300 words
- [ ] Bulleted lists vary opening verbs (≤ 80% share the same first word)
- [ ] No H2 has exactly 3 H3 children (if 2+ H2s exist, vary H3 counts)
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] No "Pontos-chave" / "O que você vai aprender" / "Os X melhores" standalone block
<!-- human-writer:ignore-end -->
- [ ] No emoji as section header
- [ ] Address form is "você" (not "tu"); progressive is the gerund ("está fazendo", not "está a fazer")

If any item fails: fix before delivery. If analyzer score is 25–49 after fixes, apply the top 3 recommendations and re-score. If 50+, reconsider your angle.

---

## Short-Form Communications

Before sending emails, LinkedIn posts, or customer replies in Portuguese, confirm:

- [ ] Analyzer score ≤ 24 with `--lang pt --type short-comms`
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] No "Espero que este e-mail o encontre bem" opening
- [ ] No "Fico no aguardo do seu retorno" / "Sem mais para o momento" boilerplate closing
- [ ] No "Venho por meio deste", "Não hesite em me escrever", "Em caso de dúvidas, não hesite em"
<!-- human-writer:ignore-end -->
- [ ] Em-dashes: 0 preferred, never 2+ in messages under 200 words
- [ ] At least one contraction, sentence fragment, or first-person verb in replies over 30 words
- [ ] Signoff is first name, short phrase, or nothing, not corporate boilerplate ("Atenciosamente" every email)
- [ ] First line is not "Venho por meio deste" / "Escrevo para" / "Gostaria de entrar em contato"

If any item fails: revise before sending. (Note: short messages are legitimately accent-sparse and well under the accent-detector word-count floor, so it will not flag them.)

---

## Technical Documentation

Before publishing internal READMEs, RFCs, or technical journals in Portuguese, confirm:

- [ ] Analyzer score ≤ 24 with `--lang pt --type technical`
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] First sentence states the WHY (problem this doc solves), not "Neste documento, vamos explorar..."
- [ ] No "Vamos nessa!" / "Bora começar!" / "Sem mais delongas" filler
- [ ] No "Conclusão" section (unless >500 words and earns a summary)
- [ ] Every instance of "robusto", "escalável", "alavancar", "elegante", "potente" passes the "replace with 'bom'" test
<!-- human-writer:ignore-end -->
- [ ] Code blocks are not surrounded by paragraphs that re-explain them line-by-line
- [ ] One sentence per concept: no restating or hedging the same idea twice
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] Zero hedging openers ("Vale ressaltar", "Convém lembrar", "É importante notar", "Nota:")
<!-- human-writer:ignore-end -->
- [ ] Accents intact even in prose around code (don't ship de-accented text just because the surrounding snippets are ASCII)

If any item fails: revise. Technical docs should be direct and economical.

---

## Editorial-SEO Articles

Before publishing ranking-optimized articles in Portuguese, confirm:

- [ ] Analyzer score ≤ 24 with `--lang pt --type editorial-seo`
- [ ] Target keyword appears in: title, first 100 words, and ≥1 H2
- [ ] First 100 words contain a specific data point or opinion (not just the keyword)
- [ ] H2 hierarchy is varied, not pyramid (not 3 H3s per H2 uniformly)
- [ ] At least 1 internal link with natural anchor text (not "clique aqui")
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] No "No mundo atual de X," / "Na era digital," opener
- [ ] No "Conclusão" that just restates the intro / tl;dr
<!-- human-writer:ignore-end -->
- [ ] At least one opinion that someone could reasonably disagree with
<!-- human-writer:ignore-start (checklist quotes the tells to look for) -->
- [ ] No "Guia definitivo", "Tudo o que você precisa saber", "Guia completo" UNLESS your keyword data demands it
<!-- human-writer:ignore-end -->
- [ ] Sentence-length standard deviation ≥ 8 (mix short and long)
- [ ] Title in sentence case, not Title Case Every Word

If any item fails: fix before publishing.

---

## Universal Baseline

Apply to **all** content types before delivery:

- [ ] Final `analyze.py --lang pt` run; score ≤ 24
- [ ] No Tier-1 suspect vocabulary in the first 100 words (check `rules.yaml` for the list)
- [ ] File is properly accented (ç ã õ á é í ó ô õ ú â ê) — re-accentuate any stripped-accent prose
- [ ] At least one specific element: number, name, date, fact, quote, not generic claims
- [ ] At least one stylistic asymmetry: a short sentence after long ones, a varied list length, unexpected structure
- [ ] Doesn't end with a summary or call-to-action that merely restates the opening

---

## pt-BR quick-triage (satellite-specific)

A 60-second eyeball pass for any Brazilian-Portuguese draft, in priority order — the fastest path from "looks AI" to "reads human". Mirrors the order in `tells-stylistic-pt.md` § Quick triage:

1. **Accents.** Is the file properly accented (ç ã õ á é í ó ô õ ú â ê)? A de-accented file reads as broken Portuguese — re-accentuate. (The detector flags long de-accented text; short snippets are exempt.)
2. **Spaced em-dashes.** Count Anglo "—" in expository prose. >1 per 500 words → replace with comma/colon/period/parentheses. Genuine dialogue travessões don't count.
3. **Opener.** First sentence starts with "no mundo atual / na era digital / vale ressaltar / mergulhe no"? Rewrite.
4. **Closer.** Last paragraph starts with "em suma / em última análise / por fim / em conclusão / em resumo"? Rewrite.
5. **Tier-1 vocab.** "alavancar (leverage), sem emendas, robusto, potencializar, empoderar, transformador, imprescindível" — cap 1 per paragraph.
6. **Constructions.** "não se trata apenas de…, mas de…", "seja você… ou…", "sem sombra de dúvida".
7. **Tricolons.** Count "X, Y e Z"; cap 1 per 200 words.
8. **Calques.** "sem emendas / perfeito" (seamless), "acionável" (actionable), "suportar um recurso" (support), "deletar" (delete), "eventualmente" (eventually), "assumir que" (assume), "navegar por" (navigate).
9. **POV.** At least one first-person mark if it's opinion; "você" (not "tu"); gerund (not "estar a").
10. **Typography.** Sentence-case title, curly quotes for pt-BR, decimal comma (3,5 milhões).

A passing piece: properly accented, 0 tier-1, ≤2 tier-2, 0 constructions, ≤1 tricolon/200w, ≤1 spaced em-dash/500w, one first-person mark if opinion, "você" + gerund, title in sentence case. That lands LOW_RISK (≤ 24) and survives Copyleaks/GPTZero at sub-25 % in most domains.

---

## How to Use These Checklists

1. Write or clean your draft.
2. Run `python3 scripts/analyze.py --input <draft> --lang pt --type <type> --format human` from the skill root.
3. If score > 24, apply the analyzer's top recommendations until ≤ 24.
4. Walk through the relevant checklist above (marketing, short-form, technical, or editorial-SEO) plus the pt-BR quick-triage.
5. Check off each item; revise any failures.
6. Re-run the analyzer if you made major changes.
7. Deliver only when both gates pass (analyzer ≤ 24 AND checklist complete).

---

## See Also

- `tells-stylistic-pt.md`: vocabulary, constructions, calques, punctuation tells (Portuguese)
- `adapter-marketing.md`: doctrine specific to long-form marketing
- `adapter-short-comms.md`: doctrine specific to short communications
- `humanization-techniques.md`: positive techniques for adding human voice (Portuguese examples)
- `scripts/analyze.py`: deterministic analyzer (run before checklist)
- `external-detectors.md`: optional integration with Copyleaks, GPTZero, etc.
