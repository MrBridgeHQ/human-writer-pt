# Stylistic Tells — Brazilian Portuguese (pt-BR)

> Doctrine for the `human-writer-pt` skill, Brazilian Portuguese side. Same axes as the rest of the `human-writer` per-language family, specialized to pt-BR. Doctrine prose is in English; the Portuguese words, phrases, and examples are the surface the analyzer matches against.

Brazilian Portuguese ChatGPT output, like French and Spanish, runs *louder* than its English counterpart, for two reasons:

1. The model leans on a neutral-formal "português de redação" register learned from journalism (*Folha*, *Estadão*), academic prose, and corporate copy. That register is naturally inflated — "vale ressaltar", "sem dúvida", "na era digital" — and it reads as marketing boilerplate the moment it lands on anything concrete.
2. English formulas leak through as calques: `leverage` → "alavancar", `seamless` → "perfeito / sem emendas", `robust` → "robusto", `dive into` → "mergulhe em". A native ear catches these immediately; the model never does.

This file codifies which words, phrases, openers, closers, and typographic choices are tells in pt-BR, with severity and rewrite. Portuguese has one structural failure mode the analyzer watches for: an entire file emitted **without its accents** (ç ã õ á é í ó ú â ê) reads as broken Portuguese on sight. AI/plain-text output sometimes strips them. That is both a typographic tell and a wired detector (`detect_accent_stripping`).

## Register note: this is Brazilian, not European, Portuguese

- **Address form: `você`, not `tu`.** Brazilian standard uses "você" (+ third-person verb) as the default second person. AI that mixes "tu" with "você", or conjugates "tu" with third-person verbs ("tu vai", a regional spoken form) inside otherwise-standard written prose, betrays stitched-together output. Pick "você" and hold it.
- **Progressive: gerúndio "está fazendo", not "está a fazer".** Brazilian uses the gerund ("estamos construindo", "está rodando"). The European "estar a + infinitive" ("estamos a construir") in Brazilian copy is a locale tell — wrong variety, reads as machine translation or a Lisbon template.
- **Vocabulary leans Brazilian.** "Time" (not "equipa"), "tela" (not "ecrã"), "ônibus", "celular", "arquivo", "cadastro" — use the Brazilian word. A European-Portuguese lexical item in pt-BR copy is a tell.
- **Spelling: post-1990 Acordo Ortográfico, Brazilian conventions.** "ação", "voo", "ideia" (no accent), "assembleia".

---

## Suspect vocabulary (PT)

The list is calibrated against typical ChatGPT/Gemini Brazilian-Portuguese output across marketing, editorial, and corporate copy.

**Hard rule.** Never use 2+ tier-1 items in the same paragraph. Cap any single tier-1 item at 1 per 500 words. Treat tier-1 items the way you would treat "delve" or "tapestry" in English: even one is suspicious; two is a giveaway.

**Soft rule.** Tier-2 items are legitimate in their domain. Track frequency: 3+ tier-2 items in a 300-word paragraph = the paragraph reads as AI-generated. Cap any single tier-2 item at 2 per 500 words.

**Pure-frequency rule.** Tier-3 items are individually invisible but flag the prose when 5+ co-occur in a single paragraph. The analyzer does NOT list tier-3 (false-positive risk on common Portuguese words is too high for a per-word matcher); the human reviewer does.

### Tier 1 — High signal (always avoid)

These are the Brazilian-Portuguese equivalents of English `delve`, `tapestry`, `realm`. Each line: the phrase, why it's a tell, a human alternative.

#### Connectors and meta-comments

- **"vale ressaltar"** / **"vale destacar"** / **"vale lembrar"** / **"vale mencionar"** / **"vale a pena ressaltar / destacar"** — Why: meta-textual hedge; reads as report-writing. The single most frequent pt-BR AI topic-sentence opener of 2025-2026. Alternative: drop the prefix, state the claim. "Vale ressaltar que as vendas subiram" → "As vendas subiram 12%."
- **"é importante destacar que"** / **"é importante ressaltar que"** / **"é importante salientar que"** / **"é importante notar que"** / **"é importante mencionar / lembrar que"** — English-calque family ("it's important to note"). Alternative: state the fact inline.
- **"é fundamental destacar que"** — Same family, heavier. Drop.
- **"convém lembrar que"** / **"convém ressaltar que"** — Pedantic, schoolbook. Alternative: state the fact without the meta-frame.
- **"cabe ressaltar"** / **"cabe destacar"** / **"cabe mencionar"** — Same. Drop.
- **"sem dúvida"** — Why: heavy "without a doubt" assertion AI sprinkles on any claim. Alternative: drop, or back the claim with a number.
- **"sem sombra de dúvida"** — Heavier variant. Drop.
- **"não há dúvida (de que)"** / **"não restam dúvidas"** — Same family. Drop.
- **"como sabemos"** / **"como todos sabem"** / **"como é sabido"** — Why: appeal to phantom consensus no native writer uses unless ironically. Alternative: drop.
- **"nesse sentido"** / **"neste sentido"** — Why: meta-textual signpost AI uses to glue paragraphs. Alternative: drop; the next sentence carries the logic.
- **"a esse respeito"** (as a paragraph connector) — Same. Drop or "sobre isso".
- **"dito isso"** (as a paragraph opener) — Fine mid-sentence; templated as an opener. Alternative: just write the next sentence.
- **"por outro lado"** / **"por sua vez"** (overused as connectors) — Schoolbook. Alternative: "e", "além disso", restructure.

#### Adverbs and phrases of certainty

- **"indubitavelmente"** / **"inegavelmente"** / **"inquestionavelmente"** — Why: heavy "of course" adverbs AI uses to assert authority. Alternative: drop, or "claramente".
- **"certamente"** / **"evidentemente"** / **"obviamente"** (as openers) — Why: AI's "obviously" reflex. Alternative: drop; if it's obvious, don't say it.
- **"naturalmente"** / **"seguramente"** (as intensifiers) — Alternative: drop or change the adjective.

#### Spatial-temporal abstractions

- **"no mundo atual"** / **"no mundo de hoje"** — Why: meta-frame opener with no date, event, or actor. Alternative: name the year, the event. "No mundo atual dos dados" → "Desde a LGPD de 2020…"
- **"na era digital"** / **"na era da IA"** / **"na era da informação"** — Same family. Alternative: a date, a fact.
- **"nos dias de hoje"** / **"nos dias atuais"** / **"atualmente"** (as scene-setters) — Why: vague time-stamps. Acceptable rarely; AI overuses. Alternative: a concrete date.
- **"num mundo onde"** / **"em um mundo onde"** / **"numa época em que"** — Why: lyrical opener. Alternative: name the actual situation.
- **"em pleno século XXI"** — Why: editorial cliché. Alternative: drop.
- **"ao longo de"** (as a lyrical scope-broadener, "ao longo dos anos") — Acceptable literally; AI overuses as filler. Alternative: name the period.
- **"no coração de"** (when not literal anatomy/geography) — Calque of "at the heart of". Alternative: "no centro de", "dentro de", or drop.
- **"no seio de"** — Calque of "within / au sein de". Stiff, AI-flavored. Alternative: "dentro de", "em".
- **"para além de"** (metaphorical scope-broadener) — Alternative: "além de", "fora".

#### Comparators and frames

- **"à luz de"** — Calque of "in the light of". Alternative: "a partir de", "considerando", "diante de".
- **"em prol de"** — Why: pompous "for the sake of". Alternative: "para", "em favor de" (sparingly).
- **"tendo em vista"** (overused) — Alternative: "por causa de", "já que".
- **"na hora de"** (as filler before an infinitive) — Why: AI padding ("na hora de escolher" = "when choosing"). Alternative: "ao escolher", "quando você escolhe".

#### Metaphorical inflators

- **"verdadeiro"** / **"verdadeira"** (as intensifiers, e.g. "uma verdadeira revolução") — Why: AI's go-to amplifier for nouns. Alternative: drop or use a concrete number.
- **"autêntico"** / **"autêntica"** (as intensifier) — Same. Drop.
- **"imprescindível"** / **"indispensável"** (marketing usage) — Why: marketing cliché now associated with AI prose. Alternative: "necessário" (sparingly), or name the reason.
- **"referência"** (as "a referência do setor") — Marketing inflator. Alternative: "o mais usado", a specific reason.
- **"emblemático"** / **"icônico"** — Why: marketing inflators. Alternative: name what makes it notable.
- **"revolucionário"** / **"revolucionária"** (outside literal politics) — Calque of "revolutionary". Alternative: "novo", "que muda as regras" (sparingly).
- **"transformador"** / **"transformadora"** — Calque of "transformative", barely idiomatic. Alternative: "decisivo", "importante".
- **"robusto"** / **"robusta"** (non-technical) — Calque of "robust". Alternative: "sólido", "confiável", "que aguenta".
- **"de ponta"** / **"de vanguarda"** / **"de última geração"** — Calque of "cutting-edge / state-of-the-art". Alternative: "novo", "atual" (with a date).
- **"de primeira linha"** / **"de classe mundial"** — Calque of "world-class / best-in-class". Alternative: cite a benchmark or a number.

#### Structural metaphors

- **"a pedra angular"** / **"o pilar fundamental"** / **"a espinha dorsal"** / **"o eixo central"** / **"a base sobre a qual"** — Why: AI scatters heroic nouns as if every concept needs one. Alternative: name the function ("X depende de Y").
- **"o motor de"** (metaphorical) — Same. Alternative: name what X actually does to Y.

#### Verbs and verbal phrases

- **"alavancar"** (when it means "leverage", e.g. "alavancar o potencial de") — Calque of "leverage". Alternative: "usar", "aproveitar", "tirar proveito de" (sparingly).
- **"potencializar"** (metaphorical: "potencializar seu negócio") — Why: AI's "empower / boost" reflex. Alternative: "melhorar", "reforçar".
- **"impulsionar"** (overused: "impulsionar o crescimento") — Alternative: "acelerar", "fazer crescer".
- **"empoderar"** — Calque of "empower". Outside genuine social/HR contexts, empty. Alternative: "dar os meios para", "permitir".
- **"desbravar"** (metaphorical: "desbravar novos mercados") — Why: heroic AI cliché. Alternative: "abrir", "entrar em".
- **"forjar"** / **"instaurar"** — Why: heavy verbs where "criar", "montar", "estabelecer" would do. Alternative: the simple verbs.
- **"encarnar"** — Why: AI's "embodies" reflex. Alternative: "representa", "é".
- **"materializar"** / **"cristalizar"** — Same. Alternative: "resume", "concretiza".
- **"catalisar"** — Same. Alternative: "desencadeia", "acelera".
- **"abraçar"** (metaphorical: "abraçar a mudança") — Calque of "embrace". Alternative: "aceitar", "adotar".
- **"mergulhe (em / no / nesse)"** / **"mergulhe no mundo"** — Why: AI's "dive into / immerse" opener. Banned as an introduction. Alternative: state the subject directly.
- **"embarque (nessa / nesta) jornada"** — Why: AI's "embark on this journey". Banned. Alternative: state the first step.
- **"desbloqueie (o potencial)"** / **"libere o potencial"** — Calque of "unlock the potential". Alternative: "use", "aproveite" (sparingly).

### Tier 2 — Medium signal (contextual)

Legitimate in domain (e.g. "otimizar" in an SRE post is fine). Flag when 3+ co-occur in 300 words.

#### Verbs

- **"explore"** / **"explorar"** (metaphorical: "vamos explorar") — Alt: "ver", "olhar", "examinar".
- **"descobrir"** (metaphorical) — Alt: "encontrar", "achar".
- **"desvendar"** / **"revelar"** — Why: marketing reveal verbs. Alt: "mostrar", "apresentar".
- **"transformar"** (overused: "transforme seu negócio") — Alt: "mudar", "melhorar".
- **"revolucionar"** — Cf. tier-1 "revolucionário". Alt: "mudar".
- **"otimizar"** / **"agilizar"** / **"simplificar"** — Domain-fine, AI filler otherwise. Alt: name the concrete change.
- **"fomentar"** / **"favorecer"** / **"propiciar"** — Hedge-y "helps to" verbs. Alt: "facilita", verb of the actual mechanism.
- **"garantir"** (overused) — Alt: "assegura", or state the condition.
- **"maximizar"** / **"minimizar"** — Corporate filler. Alt: "subir", "baixar", "reduzir".
- **"acompanhar"** (B2B "we accompany you") — Alt: "ajudar a" + verb.
- **"abordar"** (in the sense of "to address an issue") — Sometimes calque-flavored. Alt: "tratar", "resolver", "lidar com".
- **"gerenciar"** / **"gerir"** (overused as catch-all) — Alt: name the action.
- **"implementar"** — Calque-tinged in non-technical copy. Alt: "colocar em prática", "aplicar".
- **"monitorar"** — Alt: "acompanhar", "vigiar".
- **"navegar por"** (metaphorical: "navegar pela complexidade") — Calque of "navigate". Alt: "lidar com", "atravessar".

#### Adjectives of importance / intensity

- **"chave"** / **"fundamental"** / **"essencial"** / **"crucial"** / **"primordial"** / **"vital"** — All inflators. AI sprays them. Alt: drop, or quantify.
- **"notável"** / **"relevante"** / **"significativo"** / **"expressivo"** — Empty modifiers. Alt: the number.
- **"extraordinário"** / **"excepcional"** / **"impressionante"** / **"incrível"** / **"espetacular"** — AI's intensifier toolkit. Alt: name the specific quality.
- **"único"** (as "uma experiência única") — Alt: name what's actually different.
- **"inovador"** / **"inovadora"** — Empty self-praise. Alt: "novo", and show why.
- **"poderoso"** / **"potente"** (marketing) — Alt: a benchmark or number.
- **"elegante"** / **"sofisticado"** / **"intuitivo"** — Product-copy cliché. Alt: name the design choice.
- **"escalável"** (scalable, in marketing) — Alt: state the capacity number.
- **"perfeito"** / **"sem emendas"** / **"sem atritos"** — the canonical pt-BR renderings of "seamless / frictionless". Heavy tells. Alt: "direto", "sem problemas".

#### Abstract nouns

- **"sinergia"** / **"sinergias"** — Buzzword. Alt: name the relationship.
- **"ecossistema"** (metaphorical, outside biology) — Calque of "ecosystem". Alt: "mercado", "rede", "comunidade".
- **"universo"** (metaphorical: "o universo do vinho") — Alt: "o mundo do vinho", "o setor do vinho", or drop.
- **"paradigma"** — Academic filler outside Kuhn. Alt: "modelo", "abordagem".
- **"experiência"** (vague usage: "uma experiência inesquecível") — Alt: name what the user actually does.
- **"solução"** (vague, "nossa solução") — Alt: the actual thing: "o painel", "o cron", "a exportação CSV".
- **"jornada"** / **"trajetória"** / **"percurso"** (metaphorical) — Tourism/UX cliché ("a jornada do cliente"). Alt: name the steps.
- **"leque"** ("um amplo leque de") — Alt: a number, "vários".
- **"infinidade de"** ("uma infinidade de possibilidades") — Alt: a number, drop.
- **"uma série de"** / **"uma vasta gama de"** / **"uma ampla gama de"** — Alt: "muitos", a number.

#### Connectors (overuse)

- **"além disso"** / **"ademais"** / **"outrossim"** — Schoolbook (especially "outrossim", which is bureaucratic). Alt: "e", "também".
- **"por conseguinte"** / **"portanto"** (heavy, as paragraph opener) — Alt: "então", "assim".
- **"contudo"** / **"todavia"** / **"no entanto"** (every paragraph) — Alt: "mas", restructure.
- **"de fato"** (as filler) — Alt: drop.

### Tier 3 — Low signal (frequency-only)

Individually fine. Flag a paragraph if 5+ co-occur. (The analyzer does not list these; the reviewer does.)

abordagem, estratégia, desafio, oportunidade, perspectiva, visão, ambição, desempenho, eficiência, rentabilidade, crescimento, acompanhamento, valor agregado, benefício, vantagem, força, recurso, potencial, dinâmica, alavanca, eixo, pilar, dimensão, faceta, aspecto, elemento, componente, âmbito, panorama, governança, alinhamento, coerência, transversalidade, transparência, fluidez, simplicidade, eficácia, robustez, escalabilidade, modularidade, interoperabilidade, sustentabilidade, ESG, impacto, rastreabilidade, monitoramento, observabilidade, automação, industrialização.

**Why low signal**: each appears naturally in honest Brazilian B2B prose. **Why they still matter**: a paragraph with 5+ of them is corporate AI Esperanto.

### Replacements (consolidated)

| Tell | Human alternative |
|---|---|
| vale ressaltar / vale destacar | drop and state the claim |
| é importante destacar que | drop; state the fact inline |
| é importante notar que | parenthesize the qualifier, or drop |
| sem dúvida / sem sombra de dúvida | drop, or back with a number |
| no mundo atual | hoje / desde [data] / aqui |
| na era digital | hoje / desde [data concreta] |
| mergulhe / embarque nessa jornada | olhe / veja / aqui está |
| explore / descubra | vamos ver / olhe / aqui |
| desbloqueie / libere o potencial | use / aproveite (sparingly) |
| robusto (não técnico) | sólido / confiável / que aguenta |
| transformador | importante / decisivo / que muda as regras |
| no coração de | no centro de / dentro de |
| no seio de | dentro de / em |
| imprescindível (marketing) | necessário (com moderação) / name the reason |
| uma infinidade de / um leque de | muitos / vários / dezenas de (concrete) |
| uma ampla gama de | uma dezena de / vários / Ø |
| alavancar (leverage) | usar / aproveitar / tirar proveito de (sparingly) |
| potencializar / impulsionar | melhorar / acelerar / fazer crescer |
| empoderar | dar os meios para / permitir |
| desbravar | abrir / entrar em |
| forjar / instaurar | criar / montar / estabelecer |
| encarnar | representa / é |
| catalisar | desencadeia / acelera |
| abraçar (a mudança) | aceitar / adotar |
| pedra angular / pilar fundamental / espinha dorsal | name the function literally |
| ecossistema (metaphorical) | mercado / rede / comunidade |
| universo do X | setor X / o mundo do X / o X |
| de ponta / de última geração | novo / atual (with a date) |
| de classe mundial | cite a benchmark or number |
| além disso / ademais | e / também |
| por conseguinte / portanto | então / assim |
| navegar por | lidar com / atravessar |
| perfeito / sem emendas (seamless) | direto / sem problemas |

---

## AI constructions (PT)

Patterns the analyzer matches via regex. Severity drives scoring.

### High severity

#### "Não se trata (apenas / só) de X, mas de Y"

Calque of "It's not just X, it's Y". Never use. Replace with a concrete claim.

- Evitar: "Não se trata apenas de uma ferramenta de pricing, mas de um ativo estratégico."
- Preferir: "A ferramenta mostra as margens por SKU — os mesmos números que os compradores olham."

#### "Mergulhe no…" / "Embarque nessa jornada…" / "Vamos explorar…"

Never use as an introduction. State the subject directly.

- Evitar: "Mergulhe no fascinante mundo do pricing dinâmico."
- Preferir: "Pricing dinâmico — vamos começar pelos limites de margem."

#### "No mundo atual…" / "Na era digital…" / "Na era da IA…"

Never open with a temporal abstraction. Use a date, an event, or jump straight in.

- Evitar: "No mundo atual, em que os dados são o novo petróleo…"
- Preferir: "Desde a LGPD, exportar a sua base de clientes ficou mais caro."

#### "Imagine um mundo onde…" / "E se eu te dissesse que…?"

Conference-bro openers. Banned.

- Evitar: "Imagine um mundo onde os seus clientes pagam antes de comprar."
- Preferir: "O pré-pagamento já existe — grandes varejistas fazem isso há anos."

#### "Sem sombra de dúvida…"

Cf. suspect vocab. Pattern-matched separately because it acts as a topic-sentence opener.

- Evitar: "Sem sombra de dúvida, as margens estão caindo."
- Preferir: "As margens caem. Quatro pontos em dois anos."

#### "Vale ressaltar que…" / "Vale destacar que…"

The strongest single-phrase pt-BR topic-sentence tell of 2025-2026. Pattern-matched because it fronts a claim.

- Evitar: "Vale ressaltar que a migração melhorou o desempenho."
- Preferir: "A migração reduziu a latência em 40%."

### Medium severity

#### "Seja você X ou Y" / "Quer você seja X ou Y"

Avoid unless the branching is real. By default, pick one reader and write for them.

- Banido por padrão: "Seja você uma startup ou uma grande empresa…"
- Aceitável se real: "Seja você que fatura em BRL ou em USD, a exportação é idêntica."

#### "Prepare-se, porque…"

AI signal-flares to the reader. Cut them; the sentence after is the actual content.

#### "Vamos detalhar." / "Deixe-me explicar." / "Vamos direto ao ponto."

Meta-sentences that perform thinking instead of doing it. Skip to the decomposition.

#### "Em poucas palavras," / "Para resumir,"

Closers that announce a summary. Either summarize, or don't — don't announce.

#### "Você pode estar se perguntando…" / "Talvez você esteja se perguntando…"

AI's "you might be wondering" reflex. Bad. Just answer the implied question.

#### "O resultado? X." / "A conclusão? X." / "Por que isso importa? Porque…"

Question-then-answer pattern AI overuses. Native Portuguese does it occasionally; AI does it every paragraph. Cap at 1 per 800 words.

#### "O veredito é claro:" / "A conclusão é evidente:"

AI's "the verdict is clear" reflex. Drop.

### Low / conclusion severity

#### Conclusion openers: "Em suma," / "Em resumo," / "Em última análise," / "Por fim," / "Em conclusão," / "Para concluir," / "Em síntese,"

Conclusion templates. **"Em suma", "em última análise" and "por fim" are the strongest pt-BR closing tells** ("em última análise" is a direct calque of "ultimately"). Cap all at 0 as paragraph openers.

#### "Dito isso," / "Agora bem," (as paragraph openers)

Pseudo-hedges. Each acceptable rarely; AI overuses. Cap at 1 per 800 words.

### Hedging openers (drop entirely)

- "É importante destacar que"
- "É importante ressaltar que"
- "Convém lembrar que"
- "Cabe ressaltar que"
- "Vale lembrar que"

If the qualifier matters, state it inline. Example: "O preço depende do volume (importante: sem impostos)."

---

## Em-dash and travessão discipline

**Ban the em-dash "—" (U+2014) used as an Anglo-style parenthetical/rhetorical dash. Target 0; hard cap ≤ 1 per 1000 words.** As in French and Spanish, in Portuguese the wide "—" used like English (spaced, mid-sentence, for emphasis) reads as machine output on sight, because that usage is an AI signature, not native Portuguese typography. Convert every such "—" to a comma, colon, period, or parentheses.

Portuguese *does* have a legitimate native use of the travessão (`—`): **dialogue and incises within dialogue**, and a paired travessão for parenthetical insertion. The tell is not the character itself but the AI pattern: spaced Anglo dashes sprayed through expository/marketing prose. When cleaning or writing pt-BR, sweep for "—" explicitly and remove every occurrence that is not genuine dialogue or a deliberate, rare aside.

### Why pt (like FR/ES) is stricter than EN

- Native Brazilian expository prose prefers commas for short asides, colons for setups, parentheses for true asides, and periods for emphatic separation.
- The incise (a ferramenta, feita para X, roda todo dia) uses commas, not dashes, by default.
- The travessão belongs to **diálogo** (— Já vou — disse ele.) and to a rare paired parenthetical insertion. AI conflates this with the English emphasis-dash and over-applies it.

### When the travessão IS appropriate in pt

1. **Diálogo.** "— Já vou — disse ele." opens a speaker line and marks the dialogue tag.
2. **Paired parenthetical incise** where parentheses would feel too weak and commas ambiguous (because the clause already contains commas). Rare in expository prose: "O custo — nada desprezível — segue competitivo."

### Replacement table

| AI overuse | Human pt |
|---|---|
| "Rápido — eficaz — simples." | "Rápido, eficaz, simples." or "Rápido. Eficaz. Simples." |
| "A ferramenta — feita para vinícolas — roda todo dia." | "A ferramenta, feita para vinícolas, roda todo dia." |
| "Funciona — na maioria das vezes." | "Funciona (na maioria das vezes)." |
| "É simples — e funciona." | "É simples. E funciona." |
| "Três opções — A, B e C — todas válidas." | "Três opções: A, B e C. Todas válidas." |
| "O custo — não desprezível — segue competitivo." | "O custo, não desprezível, segue competitivo." |
| "Pricing flexível — pagamento por evento." | "Pricing flexível: pagamento por evento." |

---

## Calques anglo-saxões a evitar (anglicismos de IA)

These English-origin patterns leak into Brazilian Portuguese ChatGPT output. They're stronger tells in pt-BR than in English because they read as unnatural to a native ear.

### Lexical calques

- **"alavancar"** (leverage, when overused as the default "use") → "usar", "aproveitar", "tirar proveito de"
- **"perfeito"** / **"sem emendas"** / **"sem atritos"** (seamless) → "direto", "sem problemas", "sem cola no meio". "Sem emendas" and "perfeito" are the canonical pt-BR renderings of "seamless" and heavy tells.
- **"robusto"** (non-technical, robust) → "sólido", "confiável"
- **"transformador"** (transformative) → "decisivo", "importante"
- **"escalável"** (scalable, in marketing) → state the capacity number
- **"acionável"** (actionable) → "aplicável", "que dá para aplicar". "Informação acionável" is a direct calque of "actionable insight".
- **"impactar"** (to impact, transitively) → "afetar", "influenciar em". In careful Portuguese "impactar" takes "em" ("impactar em"); AI drops the preposition.
- **"customizar"** (customize) → "personalizar"
- **"resetar"** (reset) → "reiniciar", "zerar"
- **"endereçar (um problema)"** (to address an issue, calque) → "tratar", "resolver", "lidar com"
- **"assumir que"** (assume that) → "supor que", "partir do princípio de que". "Assumir" in pt = take on responsibility, not "suppose".
- **"realizar"** (overused for "do/make", calque of "realize a task") → "fazer", "executar"
- **"de ponta a ponta"** (end-to-end, when it's filler) → name the actual span
- **"baseado em"** (based on, before main verb where "segundo" fits) → "segundo", "a partir de"
- **"deletar"** (delete, software calque) → "apagar", "excluir", "remover"
- **"biblioteca"** is correct for a code library — do NOT "fix" it to "livraria" (which is a bookshop). The reverse calque ("livraria" for a software library) is the tell.
- **"eventualmente"** (eventually, calque — pt "eventualmente" = occasionally/possibly) → "com o tempo", "no fim"
- **"performar"** (to perform, calque) → "ter desempenho", "render"

### Calques de tradução (EN→pt)

When **translating** EN source into pt-BR (not writing fresh), a second class of calque appears: domain terms rendered word-for-word into pt strings that either don't exist or mean something else. They pass every "fluency" check yet read as machine output to a native professional.

| EN source | Calque (avoid) | Idiomatic pt-BR | Note |
|---|---|---|---|
| seamless integration | "integração sem emendas" | **"integração direta" / "se integra sem dor de cabeça"** | "sem emendas" / "perfeita" is the AI fingerprint for "seamless" |
| actionable insights | "informações acionáveis" | **"informações aplicáveis" / "dados que dá para usar"** | "acionável" = actuated by a mechanism, not "actionable" |
| default (value) | "o default" | **"o valor padrão"** | |
| to support a feature | "suportar um recurso" | **"oferecer / permitir / ser compatível com"** | "suportar" = to endure/bear; for software prefer "ter suporte a" |
| to address (an issue) | "endereçar o problema" | **"resolver / tratar / lidar com"** | "endereçar" = to put an address on |
| to leverage | "alavancar" | **"usar / aproveitar"** | the canonical "leverage" tell |
| robust | "robusto" | **"sólido / confiável"** | |
| cutting-edge | "de ponta" | **"novo / atual"** (with a date) | acceptable but AI-overused |
| ecosystem | "ecossistema" | **"rede / mercado / comunidade"** | |
| to navigate (complexity) | "navegar pela complexidade" | **"lidar com a complexidade"** | "navegar por" is the metaphor calque |
| scalable | "escalável" | **state the capacity number** | acceptable in tech; AI sprinkles it everywhere |

**Doctrine.** These are context-dependent (a few, like "de ponta", are tolerable), so they need a native judgment call, not a blind find-replace. In translated marketing/editorial copy aimed at a Brazilian professional audience, prefer the idiomatic column. The tell is strongest when the calque is the **central concept** of the piece.

### Syntactic calques

- **"o mais X de todos os tempos"** vs Anglo "the most X ever" → just "o mais X"
- **"X-amigável"** (X-friendly) → "fácil de X", "adaptado a X" (NEVER "X-amigável")
- **"impulsionado por X"** / **"movido a X"** (X-driven / powered by X) → "baseado em X", "com X" — fine sparingly, AI overuses
- **"pronto para X"** (X-ready) → "compatível com X", "preparado para X"
- **Gerund-as-title** ("Otimizando seu fluxo") — English progressive-title calque. pt prefers an infinitive or noun: "Como otimizar seu fluxo", "Otimização do fluxo".
- **Passive "é X-ado" overuse** — AI overuses the passive ("é recomendado que") where pt prefers the impersonal "recomenda-se" or active voice.
- **European "estar a + infinitivo"** ("estamos a construir") — wrong variety for pt-BR; use the gerund ("estamos construindo").

### Punctuation / typography calques

- **Title Case in pt titles** (capitalizing Every Word, e.g. "Como Escolher Seu Vinho") — wrong in pt. Portuguese capitalizes only the first word and proper nouns: "Como escolher seu vinho".
- **Stripped accents** — the single most diagnostic pt typography failure mode. See below.
- **Straight quotes `"X"`** instead of Portuguese angle quotes `«X»` (more European) or the common Brazilian curly `"X"` — typographic tell when the rest of the document is otherwise native. Brazilian editorial usually uses `"…"`.
- **Decimal point instead of comma** ("3.5 milhões" where pt uses "3,5 milhões") and thousands separator ("1,000" vs pt "1.000") — locale tell.

---

## Portuguese typography tells (the accent-stripping detector + more)

### Stripped accents — the signature pt failure mode (HARD CHECK, ported from FR)

Portuguese carries a dense accent system: the cedilla **ç**, the nasal tildes **ã õ**, and the acute/grave/circumflex/diaeresis vowels **á à â é ê í ó ô õ ú ü**. **Native Portuguese always carries them; AI plain-text output (and bad copy-paste, broken encodings, naive transliteration) sometimes strips them**, emitting "informacao" for "informação", "voce" for "você", "nao" for "não", "manha" for "manhã". A file with its accents stripped reads as broken Portuguese on sight — it is not a stylistic nuance, it is wrong.

The analyzer encodes this as `detect_accent_stripping`: it computes the **ratio of accented Portuguese characters to total letters**. Native pt-BR prose sits around **0.03–0.08**. A value far below the floor (`min_accent_ratio`, set at 0.012) means the accents were dropped, and the detector flags. It is a SMALL low-weight branch (+3/+5) — it never dominates the score — and it is **guarded against false positives on short input**: a text must be **≥ 40 words** before the detector can flag, because a short snippet (a CLI line, a one-sentence note) can legitimately carry zero accented characters.

- AI / mangled output: "A informacao precisa chegar rapido a equipe. Voce nao precisa de planilha."  → accents stripped
- Native pt-BR: "A informação precisa chegar rápido à equipe. Você não precisa de planilha."

**Cleanup rule.** When cleaning AI Portuguese for publication, if you see systematic accent loss, the file was mangled — re-accentuate (ç ã õ á é í ó ô õ ú â ê) before publishing. Do not ship de-accented prose.

### Angle quotes vs curly quotes

European Portuguese editorial style uses `«»`; Brazilian editorial usually uses curly `"…"`. AI defaults to straight `"X"`. Pick the convention your target locale expects and be consistent. For pt-BR, prefer `"…"`.

- AI: `"um projeto rentável"`
- pt-BR editorial: `"um projeto rentável"`

### The travessão vs the hífen vs the menos

- **Hífen `-`** — compound words ("guarda-chuva", "segunda-feira"), word-break, and (in pt) verb-clitic attachment ("faz-se", "diga-me").
- **Travessão `—`** — dialogue and paired incise (see em-dash section). Never the Anglo spaced emphasis dash.
- **Menos `−` / en-dash `–`** — number ranges ("páginas 12–14"). Rare elsewhere.

AI conflates these. Cleanup includes replacing inappropriate "—" with "," or "(".

---

## Pedantic / escolar turns

Schoolbook Portuguese. The training corpus is heavy with academic and journalistic writing, so the model defaults to phrases a *professor de redação* would have written in red pen on your essay.

Banned by default:

- **"Em um primeiro momento, convém situar o contexto"** — meta-textual scene-setting.
- **"Vale ressaltar que"** — cf. supra.
- **"Não restam dúvidas de que"** / **"Sem sombra de dúvida"** — appeal to phantom consensus.
- **"Como sabemos"** / **"Como é sabido"** — same.
- **"Diante do exposto"** — fake academic transition.
- **"A título de conclusão"** / **"A título de encerramento"** — fake academic closer.
- **"À primeira vista"** / **"De saída"** — AI's "at first glance" reflex (acceptable rarely).
- **"Em suma,"** — heavy closer.
- **"O presente artigo"** / **"O presente documento"** — bureaucratic self-reference. Drop.
- **"Pretende-se"** / **"Neste artigo, abordaremos"** — academic intent statement. Drop.
- **"Outrossim"** — pure bureaucratese. Never.

Rewrite by **stating** instead of **announcing**.

- Evitar: "Diante do exposto, convém analisar as margens."
- Preferir: "Agora, as margens."

---

## Conclusion templates (PT)

Never start a closing paragraph with any of:

- "Em conclusão,"
- "Em suma,"
- "Em última análise,"
- "Por fim,"
- "Em resumo,"
- "Em síntese,"
- "Para concluir,"
- "Para finalizar,"
- "A título de conclusão,"
- "Como vimos,"
- "Como mencionado anteriormente,"
- "Em suma, o futuro é promissor,"
- "Isso é apenas o começo."

End on a concrete action, a number, or a sharp opinion. Examples:

- "A escolha depende do volume. Menos de 100 SKUs: use A. Acima disso: B."
- "Três passos: teste, meça, decida. O resto vem sozinho."
- "Não te convenceu? Rode um dry-run em 100 linhas. Vai ver."

---

## Voice and POV tells (PT)

### Ausência de "eu" em 800+ palavras

AI defaults to detached third-person or the impersonal "se". A native author of an opinion piece **uses first person at least once per 500 words**. Cleanup rule: insert one first-person sentence per 500 words to break the impersonal register.

- Evitar (texto todo): "Pode-se observar que as margens caem. É provável que…"
- Preferir: "Vejo as margens caírem em três de cada dez clientes. Provavelmente…"

### Sobreuso do "nós" pedagógico

The "we" of a textbook ("vamos ver que…"). AI defaults to this when asked to explain. Replace with "você" (direct address) or first-person singular.

- Evitar: "Vamos ver como migrar."
- Preferir: "É assim que se migra." / "Você migra em três passos."

### "Você" sobreusado como tom de marketing

The other extreme. "Você", repeated every sentence, becomes salesy.

- Evitar: "Você ganha tempo. Você ganha dinheiro. Você ganha tranquilidade."
- Preferir: "Três horas por dia economizadas. R$ 2.000 por mês salvos. E o cliente liga menos."

### Futuro de prescrição

"Você descobrirá", "você entenderá", "você será capaz de" — AI's prescriptive future. Replace with present or imperative.

- Evitar: "Você descobrirá nossos três pilares."
- Preferir: "Três pilares. Vamos a eles."

### Condicional de cortesia em excesso

"Poderia ser interessante", "seria conveniente" — AI's politeness-conditional. Replace with direct present/imperative.

- Evitar: "Poderia ser interessante testar."
- Preferir: "Teste."

### Address-form consistency (você, not tu)

A Brazilian piece mixing "tu" with "você", or "estar a + infinitivo" with the gerund, betrays stitched output. Use "você" + gerund throughout pt-BR.

---

## Tricolon rationing (PT)

Same rule as EN/FR/ES: **cap at 1 tricolon per 200 words.** Portuguese has strong rhetorical pull toward triadic structures, so a high count reads as borrowed rhythm rather than authored prose. The analyzer's `detect_tricolons` matches the "X, Y e Z" pattern (Portuguese always uses **"e"** as the connector — there is no `y/e` allomorphy as in Spanish).

Vary list sizes (2, 4, 5 items). Use asyndeton ("rápido, confiável, limpo" without "e"). Don't close every list with ", e Z".

- Evitar: "A ferramenta é rápida, confiável e precisa. Gerencia pacotes, variantes e locais. Roda diariamente, semanalmente e sob demanda."
- Preferir: "A ferramenta gerencia pacotes e variantes em 12 locais. Rodada diária — ou sob demanda para uma auditoria pontual."

### Sub-rule: tricolons in titles and bullets

AI title format: "Rápido, confiável e eficiente". AI bullet last item: "e escalável". Both are tricolon tells.

- Title rewrite: "Rápido. E confiável." / "Rápido e confiável" (two items) / "Rápido" (one item).
- Bullet rewrite: drop the "e", or replace the last bullet with a different rhythm.

---

## Quick triage (for the human reviewer)

When auditing a 500-word pt-BR piece, scan in this order:

1. Accents — is the file properly accented (ç ã õ á é í ó ô õ ú â ê)? A de-accented file reads as broken Portuguese; re-accentuate (the detector flags long de-accented text).
2. Em-dashes / travessões — count spaced Anglo "—" in expository prose. If >1, replace.
3. Opening sentence — if it starts with a temporal abstraction ("no mundo atual", "na era digital") or a meta-frame ("vale ressaltar"), rewrite.
4. Closing sentence — if it starts with any conclusion template ("em suma", "em última análise", "por fim"), rewrite.
5. Tier-1 vocab — scan; cap at 1 per paragraph.
6. AI constructions — pattern-match by eye ("não se trata apenas de…, mas de…", "mergulhe no…").
7. Tricolons — count "X, Y e Z"; cap at 1 per 200 words.
8. Calques — find and replace the lexical ones ("sem emendas", "acionável", "suportar um recurso", "alavancar", "deletar", "eventualmente", "assumir que"); for translated copy scan the EN→pt table.
9. POV — at least one first-person mark if it's opinion; "você" (not "tu"); gerund (not "estar a").
10. Typography — sentence-case title, curly quotes for pt-BR, decimal comma.

A passing pt-BR piece, by this skill's bar:

- Properly accented throughout.
- 0–1 spaced em-dash per 500 words.
- 0 tier-1 vocab items, ≤ 2 tier-2.
- 0 AI constructions.
- ≤ 1 tricolon per 200 words.
- At least one first-person mark if opinion.
- "você" + gerund, consistent.
- Title in sentence case.

That piece will score LOW_RISK (≤ 24) on the deterministic analyzer and survive Copyleaks / GPTZero at sub-25 % AI probability in most domains.

---

## See also

- `tells-statistical.md` — burstiness, TTR, comma density doctrine (language-agnostic, shared across the family)
- `tells-structural.md` — bullets, headers, tricolons, emoji
- `humanization-techniques.md` — how to write with intentional asymmetry, with Portuguese worked examples
- `scripts/analyze.py` — `detect_suspect_vocab`, `detect_ai_constructions`, `detect_tricolons`, `detect_accent_stripping`
- `scripts/rules.yaml` — pt thresholds, suspect vocabulary, content-type weights
- the `human-writer` per-language family — sibling skills (`human-writer-en`, `human-writer-fr`, `human-writer-es`, `human-writer-de`, `human-writer-ar`, `human-writer-hi`) sharing this architecture
