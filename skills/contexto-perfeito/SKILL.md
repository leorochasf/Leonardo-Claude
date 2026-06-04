---
name: contexto-perfeito
description: Orquestra a extração de contexto completo de um caderno NotebookLM em rodadas adaptativas, de ponta a ponta. Use quando o usuário quer "o contexto perfeito", "análise profunda do caderno", "extrair tudo do NotebookLM", ou rodar o fluxo completo de rodadas sem chamar cada skill na mão. Encadeia /rodada-zero (mapa amplo) e depois /rodada-dirigida em loop até o contexto saturar, entregando um único .md consolidado. Requer a skill notebooklm instalada e logada.
---

# /contexto-perfeito — fluxo completo em rodadas

Você é o **orquestrador**. Sua função é extrair o **contexto completo** de um caderno NotebookLM
rodando o fluxo inteiro de rodadas, sem o usuário ter que conduzir cada passo nem escrever os
prompts de cada análise.

> **A ideia central:** um único prompt grande faz o NotebookLM **omitir partes** do material. A
> solução é **fatiar a análise em rodadas** — uma passada ampla (Rodada 0) seguida de rodadas
> dirigidas, cada uma guiada pelo que a anterior extraiu. No fim, um `.md` com o contexto que um
> prompt só nunca daria.

## Pré-requisito

A skill **`notebooklm`** instalada e com sessão logada. Se houver erro de autenticação rápido em
qualquer ponto, oriente o usuário a rodar `notebooklm login` no terminal e retome de onde parou.

## Fluxo

1. **Coletar entradas** (pergunte só o necessário):
   - O **caderno** (id/nome existente, ou fontes para criar um novo).
   - Se há um **preset** de gabinete aplicável (MP patrimônio/habitação, MP criminal, TJ criminal,
     TJ cível, execução penal, ou um preset próprio) — se sim, as rodadas dirigidas usarão os blocos
     desse preset. Lista e formato em `../rodada-dirigida/references/presets/README.md`.
   - Caminho de saída (opcional; padrão `contexto-<slug>.md` no diretório atual).

2. **Rodada 0 — mapa amplo.** Execute a skill **`rodada-zero`**: cria o `contexto-<slug>.md` com o
   mapa inicial e a lista de frentes a aprofundar.

3. **Rodadas dirigidas em loop (adaptativo).** Repita a skill **`rodada-dirigida`**:
   - Cada execução escolhe a próxima frente, monta o prompt dirigido a partir do que já há no `.md`,
     pergunta ao NotebookLM e anexa `## Rodada N`.
   - Após cada rodada, respeite a **checagem de saturação** dela: continue enquanto houver material
     novo relevante e frentes em aberto; **pare** quando saturar, acabarem as frentes, ou ao
     atingir a **Rodada 3** (teto padrão).
   - Normalmente são **2 a 3 rodadas** no total, conforme a complexidade — não force rodadas vazias.

4. **Consolidar e entregar.** Atualize o cabeçalho do `.md` para `> Status: concluído (N rodadas)`
   e apresente ao usuário:
   - o caminho do arquivo final,
   - um resumo do que foi coberto por rodada,
   - frentes que ficaram conscientemente de fora (se houver), para ele decidir.

## Princípios

- **Não despeje tudo num prompt.** Fatie. Profundidade vem de rodadas, não de um prompt gigante.
- **Cada rodada é guiada pela anterior** — o contexto acumulado no `.md` é a fonte dos próximos prompts.
- **Adaptativo, não mecânico.** Pare quando saturar; não rode a 3ª rodada só para "fechar o número".
- **Um arquivo só.** Tudo é anexado em `contexto-<slug>.md` — nunca sobrescreva rodadas anteriores.
