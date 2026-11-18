# AGENTS.md — Steering central do projeto Gestão Oba Doceria

## Início de sessão (obrigatório)

Antes de qualquer ação:
1. Ler `docs/HANDOFF.md`
2. Ler `docs/CURRENT_STATE.md`

Não redescobrir informações disponíveis nesses documentos. Não reabrir tarefas concluídas sem solicitação explícita ou evidência nova que justifique revisão.

## Fontes de referência

Cada fonte tem finalidade distinta — não substituem umas às outras:

| Fonte | Finalidade |
|---|---|
| Código executado | Demonstra o que está efetivamente implementado |
| Git | Demonstra histórico, alterações e estado versionado |
| `docs/DECISOES_ARQUITETURA_ESTOQUE_LOTES.md` | Autoridade sobre decisões arquiteturais aprovadas |
| `docs/PLANO_EXECUTIVO_IMPLEMENTACAO.md` | Autoridade sobre etapas, prioridades e progresso planejado |
| `docs/HANDOFF.md` | Estado de trabalho para continuidade entre sessões |
| `docs/CURRENT_STATE.md` | Estado atual do sistema |
| Demais docs em `docs/` | Referência técnica e operacional |
| Testes e auditorias | Evidências de comportamento e validação |

Uma implementação existente não altera automaticamente uma decisão aprovada. Divergência entre código e decisão aprovada deve ser identificada e tratada pelo processo de decisão — não ignorada nem resolvida unilateralmente.

## Escopo e autonomia

**Dentro do escopo autorizado**, o Kiro pode diagnosticar, planejar, implementar e testar. O nível de processo deve ser proporcional ao risco:

- **Correções simples e bem delimitadas:** executar diretamente, com testes pertinentes.
- **Alterações com dependências identificadas:** verificar dependências, implementar, validar.
- **Alterações estruturais, fora do escopo autorizado ou de maior risco:** apresentar proposta consolidada — arquivos afetados, dependências, riscos, impacto, critérios de conclusão — e aguardar aprovação antes de qualquer alteração.

Não transformar tarefa simples em processo burocrático. Não exigir proposta formal para correções autocontidas.

## Preservação

Manter decisões e melhorias anteriormente aprovadas. Não substituir soluções validadas sem justificativa técnica explícita e aprovação. Não alterar testes para fazer uma implementação passar — testes podem ser atualizados quando requisitos ou contratos aprovados mudam, preservando sua capacidade de detectar regressões.

## Implementação

Antes de qualquer alteração significativa: compreender o fluxo afetado, dependências, serviços, APIs, dados, efeitos colaterais e testes relacionados. Automatizar implementação e testes sempre que possível.

## Bloqueios

Se uma abordagem falhar, diagnosticar a causa e realizar no máximo uma recuperação tecnicamente justificada. Se o bloqueio persistir, informar a causa com clareza e interromper — não tentar indefinidamente.

## Evidências e conclusão

Encerrar quando os critérios acordados forem satisfeitos. Não acrescentar melhorias especulativas nem verificações sem propósito identificado.

O nível de validação deve ser proporcional à natureza da tarefa:
- Testes locais são suficientes quando comprovam o resultado sem dependência de ambiente externo.
- Validação em staging é necessária quando a tarefa envolve Worker, D1, concorrência, autenticação ou comportamento específico de ambiente.

## Ambientes e publicação — proteções obrigatórias

- Nunca alterar D1 de produção em testes.
- Nunca fazer commit, push, deploy ou rollback sem autorização explícita. Preparar e revisar alterações não autoriza executá-las.
- Staging antes de produção.
- Não habilitar `centralWrite` global sem gate explícito.
- Não salvar secrets no repositório.
- Aguardar Pages Functions estabilizarem após deploy antes de executar testes.
- Tratar SPA fallback 200 como possível falso positivo.

## Encerramento de sessão significativa

Atualizar somente quando houver informação relevante a registrar:
- `docs/HANDOFF.md` — quando o estado de trabalho mudar de forma que afete a próxima sessão.
- `docs/CURRENT_STATE.md` — quando o estado do sistema mudar.
- `docs/CHANGELOG.md` — quando houver entrega concluída.
- `docs/PLANO_EXECUTIVO_IMPLEMENTACAO.md` — quando houver mudança efetiva em etapas ou planejamento.
- `docs/DECISOES_ARQUITETURA_ESTOQUE_LOTES.md` — quando houver nova decisão aprovada.

Não criar atualizações artificiais apenas para cumprir rotina.

## Evolução das instruções

Aprendizados operacionais vão para a Skill correspondente. Mudanças nas regras do Steering ou nas Skills devem ser propostas e aprovadas antes de implementadas. Skills não contêm cópias de decisões — apenas referências.

## Handoff

Ao receber `/handoff` ou "faça o handoff":
- Inspecionar Git
- Identificar mudanças e testes
- Atualizar CURRENT_STATE
- Atualizar CHANGELOG
- Atualizar PLANO_EXECUTIVO_IMPLEMENTACAO e DECISOES se necessário
- Sobrescrever HANDOFF com estado acionável
- Validar consistência
- Nunca incluir secrets
- Não fazer commit/push sem autorização
