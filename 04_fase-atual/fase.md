# 00-Tasks_Gerais — Fase 1 (Módulo 1: Extração e Conciliação) — EDGE AUTO (Plano 44dd8eda)

> Tabela operacional. Fonte canônica dos cards: `00.tasks_per_fase/fase_1.md` (fase-format:2). UUIDs devolvidos pelo sincronizador do portal (30/09) e preservados. Champion: **@Bruno**. Prazo-base: 05/10→12/10/2026.

## Tasks

| ID | Task | Dono | Prazo | SPEC | Critério | Checklist-aceite | Recorte da prova | Status | Evidência |
|---|---|---|---|---|---|---|---|---|---|
| 1f8bc7fb-f85a-4ed1-9abc-a9d6dc8afbd5 | Cadastrar clientes, contratos e plantas com regras e tetos configuráveis | @Bruno | 05/10/2026 | SPEC-1-001 | CA-1-001, CA-1-002, CA-1-003 | Contrato sem entidade recusado; teto sem default; fail-closed | Fixture 2 clientes/3 plantas | Aguardando teste humano | QA v0.0.3 passou; migration 0005 aplicada; ver resumo em 06_notas/debug/debug-2026-10-06-task1-fixtures.md |
| f924d4f2-d6e4-4685-802f-f44f199dbb30 | Abrir a competência do mês com lista de colaboradores e bloqueio de liberação | @Bruno | 06/10/2026 | SPEC-1-001 | CA-1-004, CA-1-005 | Bloqueio de liberação testado; transições auditadas | Competência fixture (10 colaboradores) | Pendente (T1) | — |
| 85b69fe3-d278-41e3-b8cb-24177bc4d3e1 | Importar os dados de ponto com registro de origem e sem duplicidade | @Bruno | 07/10/2026 | SPEC-1-002 | CA-1-006, CA-1-008, CA-1-009, CA-1-011 | 2 cargas idênticas sem duplicidade; rótulo fiel | Arquivo de ponto fixture + duplicado | Pendente (T1) | — |
| cb389d03-1401-491f-82f6-e4ecd4dc9edf | Receber a planilha do cliente validada pelo contrato de semântica | @Bruno | 08/10/2026 | SPEC-1-002 | CA-1-007, CA-1-010 | Layout divergente rejeitado (0 linhas) | Planilha modelo + variante divergente | Pendente (T1) | — |
| 195a6547-bd37-442a-b22a-0dd541b44bfd | Conciliar ponto, reporte e planilha do cliente com status por colaborador | @Bruno | 09/10/2026 | SPEC-1-003 | CA-1-012, CA-1-016 | Status nas 2 comparações; isolamento de semânticas | 10 colaboradores, 4 cenários | Pendente (T3, T4) | — |
| f367ac8b-08f6-4e3e-a58e-22287bebb06a | Conduzir ajustes de ponto e divergências com decisão humana e histórico | @Bruno | 10/10/2026 | SPEC-1-003 | CA-1-013, CA-1-014, CA-1-015, CA-1-017 | Não-decisão provada; origem obrigatória; append-only | Ajuste pendente 24h + correção versionada | Pendente (T5) | — |
| 630704b0-7141-45e2-9462-84d0737946dd | Calcular horas faturáveis com regra por cliente e fail-closed de teto | @Bruno | 11/10/2026 | SPEC-1-004 | CA-1-018, CA-1-019, CA-1-022, CA-1-023, CA-1-024 | Sem teto = “em conferência”; dado real recusado | 2 regras distintas + teto vazio/preenchido | Pendente (T5) | — |
| 01e77682-eb47-41a0-ad2a-0a589c5abec0 | Emitir o relatório comparativo e registrar o baseline da medição | @Bruno | 12/10/2026 | SPEC-1-004 | CA-1-020, CA-1-021 | Relatório exportável; protocolo de medição registrado | 1ª competência do piloto (fixture) | Pendente (T7) | — |

**Cobertura**: CA-1-001..024 = 24/24. **Levas**: 1: T1 · 2: T2 · 3: T3 ∥ T4 · 4: T5 · 5: T6 ∥ T7 · 6: T8. **Task ativa**: task 1, aguardando teste humano.
