# Configuracao Claude Code — LINUX/B3_CUSTOM_ISO

Stack: **Shell / build de ISO**.

## Arquivos
- `settings.json` — configuracao ATIVA do projeto (permissoes e effort; nao escolhe modelo).
- `settings.local.json` — override local (gitignored), precede o settings.json.

## Modelo
- **O modelo e escolha do usuario**, por sessao, com `/model`. O repositorio nao escolhe
  modelo (repodocs ADR-027).
- `settings.json` nao tem `model`, `fallbackModel` nem `availableModels`, e nao exporta
  `ANTHROPIC_MODEL`, `ANTHROPIC_DEFAULT_*_MODEL` nem `CLAUDE_CODE_SUBAGENT_MODEL`.
- **Subagente herda o modelo da sessao.** Nao ha perfis stand-by para copiar por cima do
  `settings.json`: quem troca de modelo e o `/model`.
- Effort `max` via env `CLAUDE_CODE_EFFORT_LEVEL` (o campo `effortLevel` so aceita low/medium/high/xhigh).

## Permissoes
- `defaultMode: plan`; denies de seguranca (rm -rf, force push, reset --hard, clean -fd, curl|sh).
- **git push liberado** (em `allow`).
