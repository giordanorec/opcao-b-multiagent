# opcao-b-multiagent

Plugin Claude Code que implementa o fluxo **Opção B — sessões persistentes
multi-agente** com dashboard tmux ao vivo.

Autor: Giordano Rec · MIT.

## O que é

Um agente **Arquiteto** coordena um time de **especialistas** (cada um é
uma sessão Claude Code persistente) comunicando via arquivos
(`specs/`, `reports/`, `memory/`). Você acompanha o trabalho deles em
tempo real numa grade tmux com um painel por agente, texto colorido
semanticamente (tool calls, diffs, erros, resultado final).

Convém pra projetos de médio/grande porte onde 4-10 papéis trabalham em
paralelo sem se atropelar.

## Instalação

Adiciona o marketplace e instala o plugin:

```bash
claude plugin marketplace add giordanorec/claude-plugins
claude plugin install opcao-b-multiagent@giordanorec
```

## Comandos

- **`/opcao-b-init`** — inicia um projeto novo: Discovery (perguntas),
  Fase 1 (docs numerados), Fase 2 (time de agentes), Fase 3 (setup +
  git + repo GitHub), spawn dos especialistas, abre dashboard.
- **`/opcao-b-spawn <agente>`** — spawna um especialista novo num
  projeto já iniciado.
- **`/opcao-b-dashboard`** — abre (ou reabre) o dashboard tmux no
  Tilix.

## O que o plugin traz

- **9 templates de agentes** (`agents/`): `arquiteto`, `pipeline-dev`,
  `devops-installer`, `qa-tester`, `docs-writer`, `llm-prompt`,
  `frontend-dev`, `dba`, `asset-designer`, `mobile-dev`.
- **7 scripts** (`scripts/`): `spawn.sh`, `drive.sh`, `take_over.sh`,
  `open_dashboard.sh`, `_tail_color.sh`, `_status_summary.sh`,
  `_stream_pretty.py`.
- **Templates de docs** (`templates/docs/`): `00_OBJETIVO.md` até
  `10_PRIMEIROS_PASSOS.md` + `DECISOES.md`.
- **Skill de bootstrap** (`skills/opcao-b-workflow`): Claude lê e
  assume o papel de Arquiteto quando o comando é invocado.

## Dependências do sistema

- `tmux` (motor do dashboard)
- `jq` (manipulação de JSON)
- `uuidgen` (parte do util-linux, geração de session_id)
- `sed` unbuffered (`sed -u` — GNU sed)
- `python3` (parser de stream-json)
- `gh` CLI autenticado (criação de repo GitHub)
- `tilix` ou outro terminal emulator (pro dashboard — default Tilix)

## Fluxo esperado

1. `cd` num diretório vazio.
2. `/opcao-b-init` — o Arquiteto faz Discovery (stack, objetivo,
   público, orçamento), decide time, monta estrutura, commita,
   publica no GitHub, abre dashboard.
3. A partir daí, o Arquiteto é seu ponto de contato único. Ele
   escreve `specs/` e despacha os especialistas via `drive.sh`. Você
   vê tudo acontecendo nos painéis.

Ver `~/.claude/CLAUDE.md` (global do autor) pra filosofia completa do
modo, ou o README do marketplace `giordanorec/claude-plugins`.

## Licença

MIT.
