---
name: rodada-zero
description: Primeira passada (Rodada 0) de análise de um caderno NotebookLM — um mapa amplo e estrutural do material, salvo como rascunho .md que as rodadas seguintes vão aprofundar. Use quando o usuário quer "começar a análise", "rodada 0", "análise inicial", "mapear o caderno/processo" no NotebookLM, ou como primeiro passo do fluxo /contexto-perfeito. NÃO tenta extrair tudo de uma vez — propositalmente amplo, para revelar as frentes que as rodadas dirigidas vão explorar.
---

# Rodada 0 — Mapa inicial do caderno

Você está na **Rodada 0**: a primeira passada de uma análise em rodadas. O objetivo **não** é
extrair tudo — é fazer um **mapa amplo e estrutural** do caderno e, a partir dele, identificar as
**frentes/lacunas** que as próximas rodadas vão aprofundar.

> **Princípio do pack:** um único prompt grande faz o NotebookLM **omitir partes**. Por isso a
> Rodada 0 é deliberadamente de *cobertura*, não de *profundidade*. Profundidade é trabalho das
> rodadas dirigidas (`/rodada-dirigida`).

## Pré-requisito

A skill **`notebooklm`** precisa estar instalada e com sessão logada. Se qualquer chamada ao
NotebookLM falhar rápido com erro de autenticação, peça ao usuário para rodar `notebooklm login`
no terminal (fora do Claude Code, para abrir o navegador) e tente de novo.

## Entradas que você precisa

1. **Caderno** — um destes:
   - um caderno NotebookLM **já existente** (id ou nome), ou
   - **fontes** (URLs, PDFs, etc.) para criar um caderno novo — nesse caso, crie-o via skill `notebooklm`.
2. **Caminho de saída** (opcional) — onde salvar o `.md`. Se não informado, use o diretório de
   trabalho atual e gere o nome a partir de um *slug* do caderno: `contexto-<slug>.md`.

Se faltar o caderno, pergunte. Não invente fontes.

## Passos

1. **Resolver o caderno.** Se for novo, crie-o via skill `notebooklm` e adicione as fontes. Se já
   existe, apenas referencie-o.

2. **Perguntar ao NotebookLM um mapa amplo.** Invoque a skill **`notebooklm`** com um prompt de
   *cobertura* (curto, estrutural — não peça detalhes exaustivos). Cubra:
   - O que é este material (tipo, objeto, finalidade) em 2–3 linhas.
   - Partes / atores / entidades envolvidos.
   - Cronologia ou estrutura macro (capítulos, fases, marcos, seções).
   - Temas centrais e subtemas.
   - **Lacunas aparentes** — o que parece existir mas não está detalhado, pontos que pedem
     aprofundamento.

   > Quirk do binário: se chamar o CLI do NotebookLM direto com prompt multi-linha, **colapse `\n`
   > em espaço** antes de passar o argumento (`prompt.replace(/\n+/g, ' ')`) — o CLI falha em
   > silêncio com quebras de linha literais.

3. **Salvar o rascunho** em `contexto-<slug>.md` com este cabeçalho padronizado (as rodadas
   seguintes leem e anexam exatamente nesta estrutura):

   ```markdown
   # Contexto — <nome do caderno>

   > Caderno NotebookLM: <id ou nome>
   > Início: <data de hoje>
   > Status: Rodada 0 concluída

   ## Rodada 0 — Mapa inicial

   <resposta do NotebookLM>

   ### Frentes para aprofundar (semente das próximas rodadas)
   - [ ] <frente/lacuna 1>
   - [ ] <frente/lacuna 2>
   - [ ] <frente/lacuna 3>
   ```

   Se o arquivo **já existir**, não sobrescreva: avise o usuário e pergunte se é para recomeçar ou
   se ele queria a `/rodada-dirigida`.

4. **Devolver** ao usuário: o caminho do `.md` criado e a lista de **3–5 frentes** que merecem
   aprofundamento — elas são a semente da próxima rodada.

## Saída

Um arquivo `contexto-<slug>.md` com a Rodada 0 e as frentes marcadas, pronto para a
`/rodada-dirigida` (ou para o orquestrador `/contexto-perfeito` continuar o fluxo).
