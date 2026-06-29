# Humanization Techniques

> Doctrine for the `human-writer-pt` skill. The ten moves that turn AI-shaped prose into human-shaped prose. Apply in WRITE mode while drafting; apply in CLEAN mode as a targeted checklist. The doctrine is shared across the `human-writer` per-language family; the worked examples here are written in Brazilian Portuguese (EN examples kept for cross-reference).

The techniques are ordered by impact-per-edit. If you can only apply one, apply #1. If you can apply two, add #5. If you have time for everything, the full ten will cut analyzer score by 30–50 points on a typical AI draft.

Each technique below answers the same four questions:

1. **Definition.** What is it?
2. **Why it works.** Which statistical / stylistic signal does it disrupt?
3. **Worked examples.** Before and after, in EN plus pt-BR where applicable.
4. **How to apply.** Proactive in WRITE mode, targeted in CLEAN mode.

---

## 1. Vary sentence length deliberately

**Definition.** Alternate short (≤ 6 words) and long (≥ 25 words) sentences. Aim for a standard deviation of sentence lengths ≥ 8.

**Why it works.** AI prose averages 18–22 words per sentence with a low standard deviation (typically 3–5). The analyzer measures this via `sentence_length_stdev` and flags anything under ~8. Variance is the cheapest, highest-signal humanization edit available.

### Rhythm patterns to build in

| Pattern | Shape | Use case |
|---|---|---|
| **Short-short-long** | 5w + 4w + 28w | Set up a claim, then expand |
| **Long-short** | 30w + 4w | Build then punch (very human) |
| **Fragment-long** | 2w + 25w | Topic + dump |
| **Short-medium-fragment** | 6w + 15w + 3w | Cadence variation |
| **Run-on with semicolon** | 35w with `;` | One thought, two beats |

Use semicolons to extend without resetting rhythm. Use periods to reset hard. Use commas to slow without breaking. Explicit fragments ("É isso.", "E pronto.", "Ponto.") are the strongest rhythm breakers.

### Worked example (EN)

Bad (uniform; lengths 13, 13, 11, 12; stdev ~1):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> The pricing tool exports a CSV file with margin tiers per SKU. It updates daily based on competitor data scraped from major marketplaces. Users can filter by category, region, or supplier. The dashboard shows historical price evolution over the past 90 days.
<!-- human-writer:ignore-end -->

Good (varied; lengths 2, 8, 25, 18, 5, 8; stdev ~9):

> CSV out. One row per SKU, one column per marker. The pricing tool updates the file every night, pulling competitor data from Amazon, eBay, and three regional marketplaces I won't name in public. Filter it in Excel — category, region, supplier — and you get the same view our procurement team uses. Ninety days of history. That's usually enough to spot a competitor stockout.

### Worked example (pt-BR)

Bad (uniforme; comprimentos 14, 13, 15, 12; desvio ~1,2):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> Nossa ferramenta de análise exporta um arquivo CSV para cada item do catálogo. Ela se atualiza toda noite com os dados da concorrência. Os usuários podem filtrar por categoria, região ou fornecedor. O painel mostra a evolução dos preços ao longo de 90 dias.
<!-- human-writer:ignore-end -->

Good (comprimentos 3, 12, 28, 5, 18; desvio ~10):

> Exportação CSV. Uma linha por SKU, uma coluna por marcador de preço. A ferramenta roda toda noite e puxa os preços da Amazon, do Mercado Livre e de três marketplaces regionais que prefiro não citar aqui. Você filtra no Excel e pronto. Noventa dias de histórico, que cobre quase todas as rupturas de estoque da concorrência que vimos em 2025.

### Worked example (pt-BR) (second pattern)

Bad:

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> O scraper recupera os dados do site de origem. Ele os limpa segundo as regras configuradas. Em seguida os salva num banco PostgreSQL. Por fim, os disponibiliza por meio de uma API REST.
<!-- human-writer:ignore-end -->

Good:

> O scraper engole a página, limpa com as nossas regras caseiras (que nunca sobrevivem a um redesign do alvo) e empurra pro Postgres. Três colunas. Pronto. A API REST cospe o resto — e a gente deixa a saída em JSON porque é o que o front quer, e ponto.

### How to apply

**WRITE mode (proactive).** As you draft, force yourself to drop a one- or two-word sentence after every long one. If you've written three sentences of similar length, the next one *must* be a fragment or a 30+ word run-on.

**CLEAN mode (targeted edit).** Run `analyze.py` and look at `sentence_length_stdev`. If under 8, identify the three longest paragraphs and rewrite them by:
1. Splitting one mid-length sentence into a fragment + a sentence.
2. Joining two short sentences into one long, comma-spliced or semicolon-linked sentence.
3. Adding one explicit fragment ("Pronto.", "É isso.", "E ponto.").

---

## 2. Inject one opinion or specific anecdote per ~300 words

**Definition.** Every 300 words or so, insert one of: a first-person take, a named entity, a specific number, or a small concrete story.

**Why it works.** AI prose is information-dense but opinion-empty and entity-light. LLMs default to generic claims because generic claims minimize the chance of being wrong. Specific entities ("Rioja 2018", "47 req/s", "a Maria do compras") are statistically rare in AI output; they're high-signal markers of authored prose because they couldn't be generated without first-hand context.

### What counts as an "opinion"

A take that someone could disagree with. Not "X é bom para Y"; that's a fact-claim. But "eu pularia o X pra qualquer coisa abaixo de 100 SKUs porque o ROI não fecha" is an opinion: opinionated, specific, defensible.

| Not an opinion | Opinion |
|---|---|
| "O desempenho importa" | "O desempenho é a única coisa que importa abaixo de 1k QPS; o resto é perda de tempo." |
| "Escolha a ferramenta certa" | "Não use Playwright pra página estática. Cheerio é mais rápido e dá menos manutenção." |
| "Pricing é importante" | "A maioria das estratégias de pricing falha porque quem define o preço nunca fala com quem faz a cotação." |

### What counts as "specific"

A named entity (person, place, product, version), a date, a number with units, or a concrete event. Not "um marketplace grande"; diga Amazon. Not "recentemente"; diga "março de 2024". Not "os usuários"; diga "o time de compras de um dos nossos clientes de vinho".

### How to inject without breaking flow

Three placements work:

1. **Mid-paragraph aside.** "O actor (medimos a 47 req/s numa instância de 2 GB) gerencia os pacotes…"
2. **End-of-paragraph kicker.** "…e é isso. Sinceramente, é aí que a maioria para — e é onde a gente começa."
3. **New sentence between two claims.** "Ferramentas de pricing precisam de rate limit. A API pública corta em 60/min, aliás. Então você projeta em volta disso."

### Bad vs good (pt-BR)

Bad (obviedade vaga):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> O scraping em escala exige ferramentas cuidadosamente escolhidas. Escolher o framework certo pode fazer uma diferença significativa no desempenho.
<!-- human-writer:ignore-end -->

Good (posição específica):

> Coleta de dados em escala se resume a uma decisão: você paga pela rota cara e resiliente ou pela barata e frágil? A rota resiliente custa ~US$ 0,30/1k páginas e quase não quebra. A rota barata custa ~US$ 0,05/1k, mas começa a falhar no segundo mês. A gente escolhe a cara pra dado de alto valor; a barata pra coleta interna que dá pra refazer.

### How to apply

**WRITE mode.** Before writing, list 3 specific facts/anecdotes/opinions you can drop into the piece. Place one every ~300 words.

**CLEAN mode.** Search the draft for paragraphs that contain zero proper nouns, zero numbers, and zero first-person markers. Each such paragraph needs one injection. If the draft has *none* across the whole text, that's an emergency — the piece reads as generic and no amount of sentence-length variance will save it.

---

## 3. Use asymmetric bullets

**Definition.** In any bulleted list, deliberately vary the length, structure, opening word, and grammatical shape of each item.

**Why it works.** AI bullets are parallel by default: same verb (`Construir / Construir / Construir`), same length (8–12 words each), same shape (verb + object). The analyzer flags this when > 80% of bullets share the same first or last word. Asymmetry breaks the fingerprint.

### Three asymmetry axes

| Axis | Bad (symmetric) | Good (asymmetric) |
|---|---|---|
| **Length** | All 6–8 words | Mix of 2-word fragments and 25-word callouts |
| **Opener** | All start with a verb | Mix verbs, nouns, questions, fragments |
| **Shape** | All `verb + object` | Mix commands, observations, questions, mini-paragraphs |

### Worked example (pt-BR)

Bad (simétrico em comprimento e verbo):

```
- Raspar as páginas de produto
- Extrair os dados de preço
- Salvar os resultados no dataset
- Exportar para CSV
```

Good (assimétrico):

```
- Raspar as páginas de produto (parser leve pro estático, navegador headless pro que resiste — ver `selectors.ts`)
- Preços: capturamos lista, oferta e o "você economiza" separados, porque a Amazon arredonda do jeito que quer
- Dataset → CSV: `apify run --output-csv`, e pronto
- E depois? A maioria para aqui. A gente pluga no Metabase pra ver a tendência.
```

What changed: bullet 1 has a parenthetical with a code path; bullet 2 opens with a noun and uses a colon callout; bullet 3 is one short clause with an arrow; bullet 4 is a rhetorical question + two sentences.

### Sub-bullets for asymmetry

Adding a single sub-bullet under one item (and only one) breaks the visual rhythm hard:

```
- Raspar as páginas de produto
  - Navegador headless só pros alvos com muito JS — adiciona ~200 ms/página
- Extração de preços
- Exportação CSV
```

The lone sub-bullet kills the AI shape. It signals "a human chose to elaborate exactly here."

### When symmetric bullets ARE appropriate

Parallel lists where the reader compares like-with-like deserve symmetric formatting: step-by-step procedures, API reference tables, comparison matrices, pricing tiers. There, parallelism is *informational*. The rule: **prose-embedded lists should be asymmetric; reference/comparison structures can stay symmetric**.

### How to apply

**WRITE mode.** When you reach for a bullet list, draft it normally, then deliberately rewrite at least 2 of the 4 bullets to use a different shape.

**CLEAN mode.** Check `bullet_parallelism_ratio` from `analyze.py`. If ≥ 0.80, rewrite half the bullets to NOT start with the dominant verb.

---

## 4. Break tricolons: vary list sizes

**Definition.** Resist the "rule of three" reflex. Use lists of 2, 4, or 5 items. Cap the explicit three-item `e`-joined tricolon at 1 per 200 words. (Portuguese always uses **"e"** as the connector: "rápido, confiável e íntegro".)

**Why it works.** AI prose is saturated with tricolons. Typical specimens:

<!-- human-writer:ignore-start (citation: tricolon tells quoted, not used) -->
"rápido, confiável e escalável", "construir, testar e implantar", "pequeno, médio e grande".
<!-- human-writer:ignore-end -->

The cadence is comforting and tidy, which is exactly why LLMs default to it. The analyzer flags density above 1 per 200 words.

### Specific alternatives

| Reflex | Alternative | Example |
|---|---|---|
| Tricolon (3 items, "e") | **List of 2** | "Rápido e barato." |
| Tricolon (3 items, "e") | **List of 4** | "Rápido, barato, cacheado e auditado." |
| Tricolon | **List of 5 with asyndeton** | "Rápido, barato, cacheado, auditado, implantável num comando." |
| Tricolon | **List of 3 with asyndeton (no "e")** | "Rápido, confiável, escalável." |
| Tricolon | **Pair + parenthetical** | "Rápido e confiável (barato também, mas isso é de brinde)." |

Asyndeton — dropping the final "e" — is the cheapest variation. It keeps the three-beat rhythm but loses the AI-signature `, e` connector.

### Worked example (pt-BR)

Bad (três tricolons em duas frases):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> A ferramenta é rápida, confiável e precisa. Gerencia pacotes, variantes e locais. Roda diariamente, semanalmente e sob demanda.
<!-- human-writer:ignore-end -->

Good (um orçamento de tricolon gasto; tamanhos de lista variados):

> A ferramenta gerencia pacotes e variantes em 12 locais. Rodada diária, ou sob demanda pra auditoria pontual. Rápida, confiável, precisa: essa é a ordem em que a gente otimiza.

### How to apply

**WRITE mode.** Keep a mental "tricolon budget" of 1 per 200 words. If you've already used one, force the next list into 2 or 4 items, or use asyndeton.

**CLEAN mode.** Search the draft for `, e ` followed by a noun ending the sentence. Count instances. If > 1 per 200 words, rewrite the lowest-impact occurrences first.

---

## 5. Cut all hedging openers

**Definition.** Delete the AI-templated qualifier phrases that front-load sentences. State the claim directly.

**Why it works.** Hedging openers are the most distinctive AI signature in long-form prose. They're space-filler with zero information value. Removing them is the highest words-saved-per-edit move available.

### Full forbidden list (pt-BR)

<!-- human-writer:ignore-start (citation table: tells quoted, not used) -->
| Forbidden opener | Why it's a tell |
|---|---|
| "Vale ressaltar que" | The #1 pt-BR topic-sentence tell |
| "Vale destacar que" | Same family |
| "É importante destacar que" | Calque + AI template |
| "É importante notar que" | Calque of "keep in mind" |
| "Convém lembrar que" | Formal AI register |
| "Cabe ressaltar que" | Templated |
| "Sem sombra de dúvida," | Empty certainty assertion |
| "Em conclusão," | Conclusion template |
| "Em suma," (as opener) | Conclusion template |
| "Em última análise," | Calque of "ultimately" |
<!-- human-writer:ignore-end -->

### Worked example (pt-BR)

Bad:

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> Vale ressaltar que o actor precisa de pelo menos 1 GB de memória. É importante notar que o desempenho cai com os pacotes. Cabe ressaltar que o esquema pode mudar.
<!-- human-writer:ignore-end -->

Good (opção 1, direto):

> O actor precisa de 1 GB no mínimo. O desempenho cai com os pacotes (vamos resolver na v2). O esquema pode mudar.

Good (opção 2, qualificador embutido):

> O actor precisa de 1 GB no mínimo, inegociável no plano grátis da Apify. Em SKUs de pacote roda 40% mais devagar; é um problema conhecido pra v2. O esquema vai mudar nos próximos dois trimestres.

Same content. Half the words. Sounds like someone actually wrote it.

### How to apply

**WRITE mode.** Never start a sentence with a hedging opener. If you catch yourself typing "Vale ressaltar", delete and rewrite.

**CLEAN mode.** Grep the draft for every entry in the forbidden list. Delete each occurrence and rewrite the remaining sentence. This is the single highest-ROI CLEAN-mode operation.

---

## 6. Use idiosyncratic markers

**Definition.** Deliberately build 1–2 recurring tics per piece (a favored conjunction, a pet phrase, a quirky structural pattern) that the analyzer cannot fingerprint but that human readers attribute to authorial personality.

**Why it works.** Human writers have tics. AI prose is *too clean*. It avoids signature moves because LLMs are trained to produce average-of-corpus output. A deliberate tic registers as personality.

One tic per ~500 words is invisible to the analyzer (which thresholds on density) but registers to readers. Two tics per 200 words is noise.

### pt-BR-specific tics

| Tic | Cadence | Use case |
|---|---|---|
| "Olha," as sentence pivot | 1 per ~1000 words | Pivot to a strong claim |
| "No fim das contas," as paragraph closer | 1 per ~800 words | Casual register |
| "Ou seja," as connector | 1 per ~400 words | Spoken register |
| "Sinceramente," as opener | 1 per ~600 words | First-person take |
| "E pronto." / "E ponto." as fragment | 1 per ~600 words | Hard stop after a claim |
| Sentences ending with ", sei lá." | 1 per ~1000 words | Very casual register; informal only |

### Worked example (pt-BR)

Sem tic (limpo, sabor de IA):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> A ferramenta de pricing roda a cada 15 minutos. Vigia 50 SKUs por padrão. Os resultados caem numa view do Postgres que o time consulta pelo Metabase.
<!-- human-writer:ignore-end -->

Com "Olha," e "ou seja":

> A ferramenta roda a cada 15 minutos. Olha, a gente testou com 5 e os rate limits mataram a gente — 15 é o piso. Vigia 50 SKUs por padrão. Ou seja, os resultados acabam numa view do Postgres que o time consulta pelo Metabase de qualquer jeito.

The two tics are invisible to bot detection but read as a person with a voice.

### How to apply

**WRITE mode.** Before drafting, pick one or two tics. Use them at the cadence listed. Resist adding more.

**CLEAN mode.** If the piece is otherwise good but reads as bot-clean, inject *one* tic at *one* natural insertion point. Re-run the analyzer.

---

## 7. Inject digressions and parentheticals

**Definition.** Humans wander. AI stays on-track relentlessly. Insert one short digression per ~500 words. Use parentheses for genuine asides.

**Why it works.** LLMs are trained to follow the prompt without drift. The result is unnaturally focused prose: every paragraph stays inside its topical lane. Human writers tangent constantly. The drift is the signal of authentic thought. The key constraint: the digression must *return* to the main thread.

### Worked example (pt-BR)

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
Sem digressão:

> O pricing do vinho é volátil. Os produtores se adaptam acompanhando os sinais de mercado.
<!-- human-writer:ignore-end -->

Com digressão:

> O pricing do vinho é volátil (o Borgonha 2020 caiu 11% em três semanas). Os produtores se adaptam — pelo menos os que olham os sinais de mercado toda semana.

### Worked example (pt-BR) (longer)

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
Sem digressão:

> O scraping precisa de uma boa infraestrutura. Os proxies, o fingerprint e os rate limits — tudo tem que estar afinado ou o alvo te corta em menos de uma hora.
<!-- human-writer:ignore-end -->

Com digressão:

> O scraping precisa de uma boa infraestrutura. Proxies, fingerprint, rate limits — um errado e o alvo te corta em menos de uma hora. (A gente aprendeu na marra num trabalho em março de 2024: proxies impecáveis, fingerprint impecável, mas esquecemos de randomizar o sleep. Banidos em 47 minutos.) No fim das contas, cinto e suspensório em cada camada.

### How to apply

**WRITE mode.** Plan one digression per major section (every ~500 words). Mark insertion points in your outline.

**CLEAN mode.** Read each paragraph and ask: "Did the writer think of anything specific while writing this?" If every paragraph is locked to its topic, inject one parenthetical with a real specific fact.

---

## 8. Choose concrete over abstract

**Definition.** When given the choice between a generic noun and a specific one, always pick the specific. AI defaults to abstractions ("soluções", "empresas", "fluxos de trabalho"); humans default to concrete examples ("a planilha de 14 abas", "o time de compras do nosso cliente de vinho", "a prep da manhã de segunda").

**Why it works.** AI prose lives in the abstraction layer because abstractions are safer. Concrete nouns ("Postgres", "47 req/s", "12 minutos") commit to facts that must be true. Their presence is a strong signal of first-hand writing.

### Abstract → concrete substitution table (pt-BR)

<!-- human-writer:ignore-start (citation table: abstract AI nouns quoted, not used) -->
| Abstract (AI default) | Concrete (human alternative) |
|---|---|
| "as empresas" | "o nosso cliente de vinho" / "um time de compras de 12 pessoas" |
| "soluções" | a ferramenta concreta: "o painel", "o cron", "a exportação CSV" |
| "fluxos de trabalho" | o passo concreto: "a prep de segunda", "o script de importação" |
| "os usuários" | "o comprador do Carrefour" / "o analista da mesa de trading" |
| "os dados" | "47 colunas de SKU + preço + concorrente + timestamp" |
| "o desempenho" | "47 req/s numa instância de 2 GB" |
| "a escalabilidade" | "rodamos contra 2,3 mi de URLs em 9 horas" |
| "informação valiosa" | "o número concreto que você não tinha antes" |
| "as partes interessadas" | nomeie: "o diretor financeiro", "o time de compras" |
| "o ecossistema" | nomeie: "a Apify Store", "o conjunto de extensões do Postgres" |
<!-- human-writer:ignore-end -->

### Worked example (pt-BR)

Bad (abstrato):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> A nossa solução ajuda as empresas a otimizar os seus processos.
<!-- human-writer:ignore-end -->

Good (concreto):

> Trocamos a planilha de Excel de 14 abas que o nosso cliente usava pro pricing por um único painel. A prep da manhã de segunda caiu de 2 horas pra 12 minutos.

### Worked example (pt-BR) (longer)

Bad:

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> A plataforma permite que as organizações alavanquem os dados em tempo real para tomar decisões melhores.
<!-- human-writer:ignore-end -->

Good:

> A plataforma empurra as variações de preço de 8 marketplaces pro Slack, canal por canal e região por região. Quando o Rioja 2018 cai mais de 5%, a mesa de trading sabe em 90 segundos. Fecharam três ordens de compra no último trimestre com sinais que a ferramenta tirou antes dos e-mails do corretor.

### How to apply

**WRITE mode.** Each time you reach for an abstract noun ("solução", "usuários", "dados"), pause: "What's the concrete version?" Write that.

**CLEAN mode.** Grep the draft for the abstract nouns in the table above. Replace each with a concrete equivalent or rewrite the sentence around it.

---

## 9. Vary transitions, drop the formal connectors

**Definition.** AI-generated transitions are predictable and connector-heavy. Humans transition with simple conjunctions, restructure sentences, or skip transitions entirely.

**Why it works.** The connector-class AI tells are the formal-register conjunctions below. They appear when an LLM tries to make logical structure visible at the surface, which humans rarely do.

### Forbidden transitions (pt-BR)

<!-- human-writer:ignore-start (citation list: tells quoted, not used) -->
- Além disso (as paragraph opener)
- Ademais
- Outrossim
- Por conseguinte
- Portanto (as paragraph opener)
- Contudo (when overused)
- Por sua vez (as paragraph opener)
- Da mesma forma
- Nesse sentido (as paragraph opener)
<!-- human-writer:ignore-end -->

### pt-BR alternatives

- **"E"**: yes, start a sentence with "e". Portuguese allows it.
- **"Mas"**: sharp pivot.
- **"Só que"**: informal contrast.
- **"A questão é que"**: register varies but this is human.
- **"Bom,"** / **"Olha,"**: pt rhythm markers.
- **"Se não,"**: branching alternative.
- **Restructure**: often the cleanest transition is no transition — rewrite the next sentence to flow without a connector.

### Worked example (pt-BR)

Bad (cheio de conectores):

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
> O actor recupera os preços da Amazon. Além disso, vigia os níveis de estoque. Outrossim, se integra com o Slack. Por sua vez, suporta exportações diárias.
<!-- human-writer:ignore-end -->

Good (variado):

> O actor recupera os preços da Amazon. Também vigia o estoque. A integração com o Slack chega na v2. Exportações diárias — ou de hora em hora se você pedir.

### How to apply

**WRITE mode.** Never use the forbidden list. At a transition point, pick from the human alternatives or restructure.

**CLEAN mode.** Grep for every forbidden transition. Delete and rewrite. One of the fastest, highest-impact CLEAN-mode operations.

---

## 10. Build in productive imperfection

**Definition.** Humans pause, repeat for emphasis, change midstream, use casual contractions and oral elisions. AI hyper-corrects. A light imperfection ratio (1–2 instances per 500 words) registers as human without seeming sloppy.

**Why it works.** LLMs are trained out of the small imperfections real writing carries. Self-corrections, repetitions for emphasis, and casual interjections are statistically scarce in AI output and common in human prose. A small dose flips the signal.

### Imperfection categories (pt-BR)

| Category | Example | Cadence |
|---|---|---|
| **Oral elisions / contractions** | "pra" for "para", "tá" for "está", "né" tag | Informal marketing only, never technical |
| **Repetition for emphasis** | "Tá bom. Muito bom." | 1 per ~500 words |
| **Self-correction** | "O preço mexeu 11% — bom, mais pra 12% se você contar as comissões." | 1 per ~700 words |
| **Casual interjections** | "Sinceramente,", "Olha,", "Ó,", "Bom," | 1 per ~400 words (overlaps with #6) |
| **Mid-sentence pivot** | "A gente testou o proxy mais barato, mas — enfim, você já imagina." | 1 per ~800 words |
| **Trailing "e tal"** | "…ou o que for no seu stack, e tal." | 1 per ~1000 words (informal only) |

### Worked example (pt-BR)

<!-- human-writer:ignore-start (before-example, deliberately AI) -->
Sem imperfeição (IA hipercorreta):

> O preço mexeu 11% em três semanas. Isso é significativo. Convém investigar a causa subjacente.
<!-- human-writer:ignore-end -->

Com imperfeição (autocorreção + interjeição):

> O preço mexeu 11% em três semanas — bom, mais pra 12% se você contar as comissões. Isso é muito. Sinceramente, vale dar uma olhada.

### Calibration warning

Imperfection is dosed. Too much and you cross from "human writer" to "sloppy draft". The cadences above are upper bounds. In a technical doc, lean low. In casual marketing copy, the upper end works.

### How to apply

**WRITE mode.** Use natural elisions where the register allows. Add one self-correction or casual interjection per ~500 words.

**CLEAN mode.** Identify one paragraph that reads as too-polished and inject a single self-correction.

---

## Bonus: how to combine techniques

The techniques compound. Applying #1 alone drops `sentence_length_stdev` flags. Applying #1 + #5 + #9 drops the three most common AI signatures simultaneously. Below is a worked example showing the cumulative effect on a Brazilian-Portuguese paragraph.

### Starting paragraph (vanilla AI output, ~90 words)

<!-- human-writer:ignore-start (citation: deliberately AI) -->
> No mundo atual do e-commerce, monitorar os preços da concorrência é fundamental. A nossa ferramenta de inteligência de preços oferece uma solução perfeita, robusta e intuitiva. Não se trata apenas de acompanhar preços, mas de empoderar o seu time com informações acionáveis. Seja você uma startup ou uma grande empresa, a nossa plataforma ajuda você a navegar pela complexidade do pricing dinâmico. Além disso, se integra sem emendas aos seus fluxos de trabalho. Em suma, você poderá tomar decisões baseadas em dados e sair na frente da concorrência.
<!-- human-writer:ignore-end -->

**Analyzer baseline:** suspect vocab ~7 (`no mundo atual`, `fundamental`, `perfeita`, `robusta`, `empoderar`, `acionáveis`, `sem emendas`), tricolon 1 ("perfeita, robusta e intuitiva"), construction "não se trata apenas de … mas de", "seja você … ou", conclusion "em suma", connector "além disso". Estimated AI-probability: HIGH/CRITICAL.

### Final humanized version (same content, ~90 words)

> Os preços mudam de hora em hora na Amazon em plena Black Friday. Olha — a nossa ferramenta roda a cada 15 minutos contra os seus 50 SKUs mais caros e marca qualquer mexida acima de 3%. E pronto. O painel é uma view do Postgres (sem UI bonita) porque o time que precisa dele vive no Metabase de qualquer jeito. A gente montou pra um importador de vinho em 2024, depois que baixaram o preço dele seis semanas seguidas antes de ele perceber. Quer o mesmo setup? O monitor de preços roda como um Actor agendado.

What changed: temporal abstraction → concrete season + marketplace; tricolon and suspect vocab gone; "não se trata apenas de…" and "seja você…" gone; "em suma" gone; "além disso" gone; added an "Olha —" tic, an "E pronto." fragment, a real 2024 anecdote, concrete numbers (15 min, 50 SKUs, 3%), and a closing pointer.

### Order of operations summary

| Order | Technique | Reason |
|---|---|---|
| 1 | #5 Cut hedging openers | Highest words-saved, fastest fix |
| 2 | #9 Vary transitions | Cuts the connector class in one pass |
| 3 | #1 Vary sentence length | Statistical signal most analyzers test |
| 4 | #4 Break tricolons | Density signal — easy to target |
| 5 | #3 Asymmetric bullets | Only if the piece has lists |
| 6 | #8 Concrete over abstract | Compounds with #2 |
| 7 | #2 Inject opinion/anecdote | Highest authorial-signal move |
| 8 | #7 Digressions | Adds drift |
| 9 | #6 Idiosyncratic markers | Final personality layer |
| 10 | #10 Imperfection | Final humanity layer |

The first five fix the statistical signature. The last five inject the authorial signal.

---

## See also

- `tells-stylistic-pt.md` — Portuguese vocabulary and construction lists that techniques #5, #8, #9 reference directly.
- `tells-statistical.md` — the metrics (sentence-length stdev, bullet parallelism, tricolon density, em-dash density) these techniques target.
- `tells-structural.md` — bullet, header, conclusion anti-patterns that techniques #3 and #4 disrupt.
- `adapter-marketing.md` / `adapter-short-comms.md` / `adapter-technical.md` / `adapter-editorial-seo.md` — content-type-specific calibration.
