# Presets de rodadas

Um **preset** é um roteiro de perguntas dirigidas, organizado em **blocos**, que a
`/rodada-dirigida` usa para conduzir o aprofundamento quando o caderno é de um domínio conhecido.
Sem preset, a skill deriva as frentes só do que a Rodada 0 revelou; **com** preset, ela usa esses
blocos como espinha dorsal — um bloco por rodada.

## Presets incluídos

| Arquivo | Gabinete / contexto |
|---------|---------------------|
| `mp-patrimonio-habitacao.md` | MP — patrimônio público, habitação, REURB (autos extrajudiciais) |
| `mp-criminal.md` | MP — criminal 1ª instância (denúncia / arquivamento / ANPP) |
| `tj-criminal.md` | TJ — gabinete criminal (apelação, RESE, HC, revisão) |
| `tj-civel.md` | TJ — gabinete cível (apelação, agravo) |
| `execucao-penal.md` | Execução penal (progressão, livramento, remição, faltas) |

## Como a skill escolhe o preset

Na `/rodada-dirigida` (e no `/contexto-perfeito`), o agente identifica o tipo de caderno — pelo que
a Rodada 0 mostrou ou perguntando a você — e carrega o arquivo correspondente desta pasta. Se nenhum
preset casar, a skill segue **sem preset**, guiada apenas pelas frentes do `.md`.

## Como configurar o SEU próprio preset

1. **Copie** um arquivo existente como modelo (ex.: `tj-civel.md`) e renomeie com um slug claro:
   `meu-gabinete.md`. Coloque-o **nesta pasta** (`skills/rodada-dirigida/references/presets/`).

2. **Edite o cabeçalho** — mantenha o formato, é assim que a skill sabe quando usar o preset:

   ```markdown
   # Preset — <Nome do seu gabinete>

   > **Quando usar:** <descreva o tipo de caderno/processo que dispara este preset>

   > Uso: na `/rodada-dirigida`, escolha um bloco por rodada...
   ```

3. **Escreva os blocos.** Cada `## Bloco N — <tema>` é uma frente de aprofundamento (vira ~uma
   rodada). Dentro, liste as perguntas dirigidas em bullets. Regras de ouro:
   - **Um bloco = uma frente coesa.** Não misture assuntos — é o que evita a omissão do NotebookLM.
   - Ordene do mais estrutural (identificação) ao mais conclusivo (desfecho).
   - 4 a 8 blocos costuma ser o ideal.

4. **Adicione uma linha** na tabela "Presets incluídos" acima (opcional, só organização).

5. **Pronto.** Na próxima vez que você rodar `/rodada-dirigida` num caderno desse tipo, é só apontar
   o preset (ou deixar o agente reconhecer pelo "Quando usar").

> Dica: presets não precisam ser jurídicos. O mesmo formato serve para qualquer processo recorrente
> — due diligence, análise de contrato, revisão de artigo, onboarding técnico. Troque os blocos.
