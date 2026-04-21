---
description: "Spawna um novo especialista num projeto Opção B já iniciado"
argument-hint: "<nome-do-agente> (ex frontend-dev, dba, llm-prompt)"
---

Spawna um agente especialista adicional no projeto corrente.

## Pré-requisitos

- Projeto já inicializado com `/opcao-b-init` (tem `scripts/spawn.sh`,
  `.claude/agents/`, `sessions.json`).
- Argumento obrigatório: `$ARGUMENTS` = nome do agente.

## Processo

1. **Validar argumento**: se `$ARGUMENTS` vazio, peça o nome do agente.
2. **Verificar se o agente-file existe**:
   - Se `./.claude/agents/$ARGUMENTS.md` existir, ok, prossiga.
   - Se não existir, procure em `${CLAUDE_PLUGIN_ROOT}/agents/$ARGUMENTS.md`.
     - Se encontrar: copie para `./.claude/agents/` e avise o usuário.
     - Se não encontrar nem no plugin: liste os templates disponíveis
       em `${CLAUDE_PLUGIN_ROOT}/agents/` e peça pro usuário escolher,
       ou oferecer criar do zero com frontmatter mínimo.
3. **Verificar se não está duplicado**: se o agente já está em
   `sessions.json`, avise que já existe e ofereça `/opcao-b-dashboard`
   pra ver os panos.
4. **Spawnar**: `scripts/spawn.sh $ARGUMENTS`.
5. **Atualizar dashboard**: `scripts/open_dashboard.sh --rebuild`.
6. **Reportar**: session_id, cor no dashboard, próxima sugestão de
   spec pra ele.
