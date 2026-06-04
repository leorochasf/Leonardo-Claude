---
name: rodada-dirigida
description: Aprofunda a análise de um caderno NotebookLM numa rodada dirigida — lê o arquivo contexto-*.md já existente (com a Rodada 0 e rodadas anteriores), identifica as lacunas, monta UM prompt focado nelas, pergunta ao NotebookLM e anexa a resposta no mesmo arquivo. Use para "próxima rodada", "aprofundar a análise", "rodada dirigida", ou como passo de loop dentro de /contexto-perfeito. Trata uma frente por vez para o NotebookLM não omitir, e decide (adaptativo) se ainda vale outra rodada.
---

# Rodada dirigida — aprofundamento guiado

Você está numa **rodada dirigida**: o coração do pack. Diferente da Rodada 0 (cobertura ampla),
aqui você **aprofunda** o que já foi mapeado. O prompt desta rodada **nasce do que já foi extraído**
— o usuário não escreve o prompt, você o deriva das lacunas registradas no arquivo.

> **Princípio do pack:** um prompt grande omite. Por isso cada rodada ataca **uma frente de cada
> vez**, com contexto do que já se sabe — assim o NotebookLM responde fundo, sem pular partes.

## Pré-requisito

- A skill **`notebooklm`** instalada e logada (se der erro de auth rápido, peça `notebooklm login`).
- Um arquivo **`contexto-<slug>.md`** já existente (criado pela `/rodada-zero`). Se não houver,
  oriente o usuário a rodar `/rodada-zero` primeiro.

## Passos

1. **Ler o arquivo** `contexto-<slug>.md` inteiro — todas as rodadas já feitas e a lista de
   **frentes para aprofundar**. Entenda o que já está coberto para **não repetir**.

2. **Escolher a frente desta rodada.** Pegue a próxima lacuna mais relevante ainda em aberto
   (`- [ ]`). Trate **uma frente** (ou um grupo coeso pequeno) — não tudo de uma vez.
   - Se o caderno casar com um **preset** conhecido, carregue o arquivo correspondente em
     `references/presets/` e use os blocos de lá como roteiro dirigido (um bloco por rodada). Veja
     `references/presets/README.md` para a lista de presets e como o usuário cria o próprio. Se
     nenhum preset casar, siga sem preset — guiado só pelas frentes do `.md`. Presets atuais:
     `mp-patrimonio-habitacao`, `mp-criminal`, `tj-criminal`, `tj-civel`, `execucao-penal`.

3. **Montar UM prompt dirigido.** Construído a partir do contexto já extraído: relembre ao
   NotebookLM o que já se sabe sobre a frente e peça **o detalhe que falta** — específico,
   delimitado, com a profundidade que a Rodada 0 não alcançou.

   > Quirk do binário: se chamar o CLI direto, **colapse `\n` em espaço** no argumento do prompt.

4. **Perguntar ao NotebookLM.** Invoque a skill **`notebooklm`** com esse prompt.

5. **Anexar** a resposta no MESMO arquivo (nunca sobrescrever), com a numeração correta:

   ```markdown
   ## Rodada N — <tema da frente>

   <resposta do NotebookLM>
   ```

   Em seguida, atualize a lista de frentes: marque a que foi coberta (`- [x]`) e **adicione novas
   frentes** que esta rodada eventualmente revelou. Atualize a linha `> Status:` do cabeçalho.

6. **Checagem de saturação (decisão adaptativa).** Decida se vale outra rodada:
   - **Continuar** se: a rodada trouxe material **novo e relevante** E ainda há frentes em aberto
     E você está abaixo da Rodada 3.
   - **Parar** se: a rodada não trouxe nada substancialmente novo (saturou), OU não há mais frentes
     em aberto, OU você já chegou à Rodada 3 (teto padrão).

   Informe ao usuário a decisão e o porquê em uma linha.

## Saída

O arquivo `contexto-<slug>.md` atualizado com a nova `## Rodada N`, frentes remarcadas, e uma
recomendação clara: **rodar de novo** (`/rodada-dirigida`) ou **encerrar** (contexto saturado).
