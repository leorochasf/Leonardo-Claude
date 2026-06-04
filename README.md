# NotebookLM Rodadas

Pack de skills para Claude Code que extrai o **contexto completo** de um caderno do Google NotebookLM
através de **análise em rodadas**.

## O problema

Um único prompt grande faz o NotebookLM **omitir partes** do material — ele resume, pula trechos,
nivela por cima. Pedir "analise tudo isso a fundo" devolve uma resposta rasa.

## A solução

Fatiar a análise em **rodadas**, onde cada rodada é guiada pelo que a anterior extraiu:

```
Rodada 0 (mapa amplo)  →  Rodada dirigida  →  Rodada dirigida  →  ...  →  contexto-<slug>.md
        │                       │                    │
   cobre o caderno      aprofunda 1 frente    aprofunda outra frente
   e lista lacunas      por vez, com contexto    até o contexto saturar
```

No fim você tem um `contexto-<slug>.md` com o contexto que um prompt só nunca daria — e você não
precisou escrever o prompt de cada análise: as skills os derivam do que já foi extraído.

## Skills incluídas

| Skill | O que faz |
|-------|-----------|
| `/contexto-perfeito` | **Orquestrador.** Roda o fluxo completo: Rodada 0 + rodadas dirigidas em loop até saturar. |
| `/rodada-zero` | Mapa amplo e estrutural do caderno → cria o `.md` e lista as frentes a aprofundar. |
| `/rodada-dirigida` | Lê o `.md`, escolhe uma frente, monta o prompt dirigido, pergunta ao NotebookLM e anexa. |

### Presets de gabinete

Quando o caderno é de um domínio conhecido, a `/rodada-dirigida` usa um **preset** — um roteiro de
perguntas em blocos — como espinha dorsal do aprofundamento. Presets incluídos
(`skills/rodada-dirigida/references/presets/`):

| Preset | Gabinete / contexto |
|--------|---------------------|
| `mp-patrimonio-habitacao` | MP — patrimônio público, habitação, REURB (autos extrajudiciais) |
| `mp-criminal` | MP — criminal 1ª instância (denúncia / arquivamento / ANPP) |
| `tj-criminal` | TJ — gabinete criminal (apelação, RESE, HC, revisão) |
| `tj-civel` | TJ — gabinete cível (apelação, agravo) |
| `execucao-penal` | Execução penal (progressão, livramento, remição, faltas) |

Sem preset, a skill funciona normalmente — guiada só pelas frentes que a Rodada 0 revelou.

## Pré-requisito

A skill **`notebooklm`** precisa estar instalada e com sessão **logada** (`notebooklm login` no
terminal na primeira vez). Este pack não fala com o NotebookLM direto — ele orquestra essa skill.

## Instalação

### Opção A — como plugin (Git / marketplace)

```
/plugin marketplace add <url-do-repositorio-git>
/plugin install notebooklm-rodadas
```

### Opção B — como pasta de skills (sem Git)

Copie cada subpasta de `skills/` para `~/.claude/skills/`:

```
~/.claude/skills/contexto-perfeito/
~/.claude/skills/rodada-zero/
~/.claude/skills/rodada-dirigida/
```

(No Windows: `C:\Users\<você>\.claude\skills\`.) Reinicie a sessão do Claude Code.

## Uso

Fluxo completo (recomendado):

```
/contexto-perfeito
```

Ele pergunta o caderno (id/nome existente ou fontes para criar), qual preset de gabinete usar (se
houver), e conduz todas as rodadas, entregando o `.md` consolidado.

Skills soltas, se quiser controlar manualmente:

```
/rodada-zero        # cria o mapa inicial
/rodada-dirigida    # roda uma rodada dirigida (repita conforme a recomendação dela)
```

## Configurar seu próprio preset

Quer um roteiro sob medida para o seu gabinete (ou para qualquer processo recorrente — due
diligence, análise de contrato, revisão de artigo)? Em 3 passos:

1. **Copie** um preset existente como modelo, na pasta `skills/rodada-dirigida/references/presets/`,
   e renomeie (ex.: `meu-gabinete.md`).
2. **Ajuste o cabeçalho** (`# Preset — <nome>` e a linha `> **Quando usar:** …`) — é por ele que a
   skill reconhece quando aplicar o preset.
3. **Escreva os blocos** (`## Bloco N — <tema>`): um bloco = uma frente coesa de perguntas, do mais
   estrutural ao mais conclusivo. 4 a 8 blocos é o ideal.

O passo a passo completo, com exemplo de formato, está em
[`skills/rodada-dirigida/references/presets/README.md`](skills/rodada-dirigida/references/presets/README.md).

## Documentação

- `docs/guia-instalacao-uso.pdf` — guia visual curto de instalação e uso.
- `docs/roteiro-video.md` — roteiro para gravar um vídeo de demonstração.
- `docs/como-compartilhar.md` — como publicar e distribuir este pack.
