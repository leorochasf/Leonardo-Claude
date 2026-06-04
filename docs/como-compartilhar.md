# Como compartilhar o pack

Duas formas de distribuir o **NotebookLM Rodadas**. A primeira é a profissional (instalável por
qualquer pessoa com um comando); a segunda é a rápida (mandar uma pasta).

---

## Forma 1 — GitHub (plugin / marketplace) — recomendada

A pessoa instala com dois comandos e recebe atualizações via `git pull`.

### Publicar

1. Dentro de `notebooklm-rodadas/`, inicie o repositório e suba para o GitHub:

   ```bash
   git init
   git add .
   git commit -m "NotebookLM Rodadas v1.0.0"
   git branch -M main
   git remote add origin https://github.com/leorochasf/Leonardo-Claude.git
   git push -u origin main
   ```

2. Confira que `.claude-plugin/marketplace.json` e `.claude-plugin/plugin.json` estão no repositório
   (são eles que tornam o pack instalável). Ajuste `owner.url` / `author.url` para o seu GitHub real.

### Como o destinatário instala

```
/plugin marketplace add https://github.com/leorochasf/Leonardo-Claude
/plugin install notebooklm-rodadas
```

### Versionar atualizações

Ao publicar uma nova versão, **suba o número em DOIS lugares** (devem ficar iguais):
`marketplace.json` (`version` no topo e dentro de `plugins[]`) e `plugin.json` (`version`). Commit +
push. Quem instalou atualiza com `/plugin update notebooklm-rodadas`.

---

## Forma 2 — Pasta / ZIP (sem Git)

Para mandar direto a alguém (WhatsApp, Drive, e-mail).

1. Zipe a pasta `skills/` e o `README.md`:

   ```bash
   zip -r notebooklm-rodadas-skills.zip skills README.md
   ```

2. O destinatário descompacta e copia as subpastas de `skills/` para a pasta de skills dele:

   - macOS/Linux: `~/.claude/skills/`
   - Windows: `C:\Users\<ele>\.claude\skills\`

   Ficando: `…/.claude/skills/contexto-perfeito/`, `…/rodada-zero/`, `…/rodada-dirigida/`.

3. Reiniciar a sessão do Claude Code. As skills aparecem como `/contexto-perfeito` etc.

---

## Pré-requisito que o destinatário precisa ter

Avise sempre: este pack **não conversa com o NotebookLM sozinho** — ele orquestra a skill
**`notebooklm`**. Quem instalar precisa:

1. Ter a skill **`notebooklm`** instalada.
2. Estar **logado** (`notebooklm login` no terminal, uma vez, para abrir o navegador).

Sem isso, as rodadas falham com erro de autenticação.

---

## Checklist antes de compartilhar

- [ ] Testei numa **sessão limpa** do Claude Code e as 3 skills aparecem (`/contexto-perfeito`,
      `/rodada-zero`, `/rodada-dirigida`).
- [ ] Rodei o fluxo num caderno de teste e o `contexto-*.md` foi criado e aprofundado por rodada.
- [ ] **Nenhum caminho ou segredo pessoal hardcoded** nas skills (paths do meu PC, ids de caderno
      meus, tokens). As skills devem ser genéricas.
- [ ] `owner.url` e `author.url` nos manifestos apontam para o **meu** GitHub.
- [ ] `version` igual em `marketplace.json` e `plugin.json`.
- [ ] README explica o pré-requisito da skill `notebooklm`.
