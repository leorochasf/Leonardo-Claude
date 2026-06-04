# Roteiro de vídeo — NotebookLM Rodadas (~4 min)

Vídeo curto de demonstração do pack. Formato de gravação: blocos com **[CENA]**, **[TELA]** (o que
aparece) e **[FALA]** (o que você diz). Tom: direto, de quem resolve um problema real — sem
"venda". Captura sugerida: tela cheia do terminal/Claude Code, com zoom nos momentos-chave.

---

## [CENA 1] Gancho — o problema (0:00–0:30)

**[TELA]** Você num caderno do NotebookLM com um processo grande aberto. Digita um prompt do tipo
"analise todo esse processo a fundo" e mostra a resposta voltando **rasa / resumida**.

**[FALA]**
> "Se você joga um caderno inteiro do NotebookLM num prompt só e pede pra analisar tudo, ele omite.
> Resume, pula trecho, entrega por cima. Eu cansei disso — então montei um pack de skills pro Claude
> Code que resolve de um jeito diferente."

---

## [CENA 2] A ideia — rodadas (0:30–1:10)

**[TELA]** Um diagrama simples na tela (pode ser o do README): Rodada 0 → rodada dirigida → rodada
dirigida → arquivo `.md`.

**[FALA]**
> "Em vez de um prompt gigante, a gente fatia em rodadas. A Rodada 0 faz um mapa amplo do caderno e
> lista as lacunas. Aí cada rodada seguinte pega UMA dessas lacunas e aprofunda — e o melhor: o
> prompt de cada rodada nasce do que a anterior já extraiu. Eu não escrevo prompt nenhum no meio do
> caminho."

---

## [CENA 3] Instalação (1:10–1:40)

**[TELA]** Rodar `/plugin marketplace add ...` e `/plugin install notebooklm-rodadas` (ou mostrar a
pasta sendo copiada para `~/.claude/skills/`). Mostrar rápido o pré-requisito da skill `notebooklm`.

**[FALA]**
> "Instalar é simples — dá pra fazer como plugin pelo Git, ou só copiando a pasta de skills. O único
> pré-requisito é ter a skill do NotebookLM instalada e logada, porque é ela que conversa com o
> caderno. Esse pack só orquestra."

---

## [CENA 4] Rodando ao vivo (1:40–3:10)

**[TELA]** Digitar `/contexto-perfeito`. Mostrar ele perguntando o caderno, você apontando um caderno
de teste. Então:
- aparece o `contexto-<slug>.md` sendo criado com `## Rodada 0`;
- depois `## Rodada 1`, `## Rodada 2` sendo **anexadas** (faça zoom no arquivo crescendo);
- destaque a mensagem de **saturação** ("não trouxe material novo — encerrando").

**[FALA]**
> "Eu rodo `/contexto-perfeito`, aponto o caderno, e ele conduz tudo. Olha o arquivo crescendo:
> Rodada 0 com o mapa, depois ele vai fundo numa frente, anexa, vai pra próxima... e quando percebe
> que não está mais aprendendo nada novo, ele **para sozinho**. Não roda rodada à toa."

---

## [CENA 5] O resultado (3:10–3:40)

**[TELA]** Abrir o `contexto-<slug>.md` final e rolar de cima a baixo, mostrando a densidade —
contraste com a resposta rasa da Cena 1.

**[FALA]**
> "Esse é o resultado: um único arquivo com o contexto que um prompt só jamais entregaria. É isso que
> eu colo de volta no Claude quando preciso que ele entenda o processo inteiro."

---

## [CENA 6] Fechamento / CTA (3:40–4:00)

**[TELA]** Tela do repositório no GitHub (link visível).

**[FALA]**
> "Tá tudo aberto, link na descrição. Tem um preset jurídico embutido pra quem trabalha com autos,
> mas funciona pra qualquer caderno. Se te ajudou, deixa o teu feedback."

---

### Notas de gravação

- Tenha um **caderno de teste já pronto** (poucas fontes) pra rodada não demorar no vídeo.
- Corte os tempos de espera do NotebookLM na edição — mantenha o ritmo.
- Zoom nos dois momentos que vendem a ideia: o `.md` **crescendo por rodada** e a **parada por saturação**.
- Se a sessão do NotebookLM tiver expirado, rode `notebooklm login` **antes** de gravar.
