# Preset — MP · Patrimônio público e habitação (autos extrajudiciais)

> **Quando usar:** caderno é um **auto extrajudicial** do MP (Inquérito Civil Público, Procedimento
> Administrativo ou Procedimento Preparatório), em **patrimônio público, habitação social,
> regularização fundiária (REURB), loteamentos irregulares e infraestrutura urbana**.

> Uso: na `/rodada-dirigida`, escolha **um bloco por rodada** (ou um subconjunto coeso). Não jogue
> todos os blocos num prompt só — isso é exatamente o que faz o NotebookLM omitir. Adapte as
> perguntas ao que a Rodada 0 já revelou; pule blocos que não se aplicam.

## Bloco 1 — Identificação do procedimento

- Qual o tipo (ICP / PA / PP), número e data de instauração?
- Qual o **objeto** e a finalidade declarada do procedimento?
- Quem é o **interessado / noticiante** e quem é o **investigado / requerido**?
- Qual a **promotoria / órgão** responsável e o promotor signatário?

## Bloco 2 — Linha do tempo de movimentos

- Liste, em ordem cronológica, **todos os movimentos** (despachos, ofícios, juntadas, manifestações).
- Para cada movimento: data, autor, tipo e síntese do conteúdo.
- Há **lacunas temporais** relevantes (períodos sem movimentação)?

## Bloco 3 — Prazos, prescrição e prorrogações

- Quantas **prorrogações** já houve e em que datas?
- Qual o **prazo corrente** e quando vence?
- Há risco de **prescrição** ou de extrapolar o prazo máximo do procedimento?
- Há determinação de prazo pendente de cumprimento?

## Bloco 4 — Mérito e providências

- Quais **diligências** já foram realizadas e quais resultados produziram?
- Quais **providências pendentes** ou requeridas e ainda não atendidas?
- Há **prova de dano** ao patrimônio público / irregularidade configurada? Qual?
- Há indícios de **improbidade**, desvio de finalidade ou parcelamento irregular do solo?

## Bloco 5 — Programa / política pública envolvida

- Qual **programa habitacional** ou política está em discussão (PMCMV, AGEHAB, PTTS, PAC, REURB-S/E)?
- Há **convênio / repasse** envolvido? Valores, partes, vigência e prestação de contas?
- Qual o estágio da **regularização fundiária** ou da obra (se houver)?

## Bloco 6 — Desfecho e fundamentação

- Os elementos apontam para qual **desfecho** (arquivamento, prorrogação, instauração de PA, TAC)?
- Qual a **fundamentação jurídica** pertinente (Resolução n. 09/2018 do CPJ/MPGO e legislação aplicável)?
- O que ainda **falta** para fundamentar com segurança a minuta?

---

> Estes blocos são um roteiro, não um script rígido. A skill `patrimonio-publico-habitacao` do
> usuário cobre a redação da minuta em si; aqui o objetivo é apenas **extrair do caderno o contexto**
> necessário para alimentá-la.
