# STATUS — Projeto EDGE AUTO (Medição, Faturamento e Cobrança)

**Etapa atual:** Fase 1 — task 1 implementada em Skip v0.0.3; aguardando teste humano no preview
**Champion:** Bruno (CEO) · **Construção:** Skip (GoSkip + SkipCloud)

| Etapa | Estado |
|---|---|
| Kickoff e corte do escopo | Concluídos (17/09–30/09) |
| Escopo do ciclo 1 (conciliação + cobrança) | Aprovado |
| SPECs da Fase 1 | 4 SPECs · 24 critérios de aceite · com TDD e provas negativas |
| Tasks da Fase 1 | 8 tasks em 6 levas · prazo-base 05/10→12/10/2026 · responsável: Bruno |
| Task 1 — cadastro clientes/contratos/plantas/tetos | Código no preview v0.0.3; QA pipeline passou; migration 0005 aplicada; aguardando teste humano |
| Execução confirmada | 0 tasks fechadas; teste funcional da task 1 pendente |

## Próxima ação

1. Bruno entra no preview autenticado e valida as provas de CA-1-001/002/003 descritas no gate. O agente não tem credencial de teste confirmada; não fez login nem gravou cadastros via UI.
2. Só depois da aprovação explícita do teste humano, concluir a task 1 e atualizar o avanço da fase.

## Limites

- App não publicado em produção.
- `npm test` do projeto é um placeholder sem casos automatizados reais.
- Dados de trabalho devem continuar sintéticos até aprovação da política de dados.
