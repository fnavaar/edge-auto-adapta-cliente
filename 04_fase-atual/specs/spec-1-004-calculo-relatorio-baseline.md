# SPEC-1-004 — Cálculo faturável fail-closed, relatório comparativo e baseline

- **Fase**: F1 · **Capacidades**: C7 (parcial), C11 (v1), C13 (mínima) · **Risco**: obrigatório (dado pessoal, valor financeiro)
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: entrega palpável da F1 — o **relatório comparativo ponto × planilha do cliente** (valor visível na 1ª consultoria e argumento do rito/SLA) — e fecha a base de medição do ciclo (baseline + métrica), com o cálculo de faturáveis protegido por fail-closed.

## Contexto
- **Estado atual**: horas faturáveis calculadas à mão em planilha (H.T., H.E.1 75%, H.E.2 100%, noturno, sáb/dom/fer), com teto contratual em conflito e sem baseline medido.
- **Estado desejado**: motor de cálculo parametrizado por regra contratual, fail-closed sem teto provado; relatório comparativo por competência/planta/colaborador com divergências por origem; baseline coletado com protocolo de medição; governança mínima (dado real bloqueado, auditoria).

## Atores e permissões
- Financeiro: confere itens faturáveis, valida relatório, registra baseline.
- RH/Medição: contribui com dados de tempo de processo.
- Consultoria: registra protocolo de medição (janela/método).

## Dados
Regra contratual por cliente/planta/vigência (H.E.1 %, H.E.2 %, adicional noturno, sáb/dom/fer), teto (I-04), horas conciliadas (SPEC-1-003), itens faturáveis/não faturáveis/em conferência, tempos do baseline (I-02: conciliação, envio→aprovação, aprovação→pagamento), métrica por competência.

## Regras
1. **Fail-closed de teto**: sem teto provado, nenhum item sai como "faturável" — apenas "em conferência — teto não provado" (DH-04).
2. Faturáveis só com regra contratual aplicada e conferência registrada; rubricas (H.E.1/H.E.2/noturno/sáb/dom/fer) calculadas por parametrização, nunca por valor fixo universal (a regra VW não é universal).
3. **Meta numérica só após baseline** (DH-02) — nada de promessa antes de medido.
4. Política mínima: dado real (próprio/de terceiros) bloqueado até I-06; até lá, fixtures (CA-1-022 com prova negativa de recusa).
5. Toda alteração de valor/horas/previsão auditada (quem/quando/por quê).
6. Nenhuma superfície promete automação não provada (I-03): rótulos de "manual/integração" fiéis à realidade.

## Fluxo e passos
1. Aplicar regra contratual às horas conciliadas → itens faturáveis / não faturáveis / em conferência.
2. Gerar relatório comparativo ponto × planilha do cliente (por competência/planta/colaborador, divergências por origem).
3. Registrar tempos de processo → baseline + métrica por competência (protocolo de medição documentado).

## Exceções e rollback
- Regra contratual ausente → item "sem regra", não faturável.
- Baseline incompleto → registra parcial com ressalva; nunca estima.
- Relatório regenerável a qualquer momento a partir dos dados versionados (idempotente).

## Critérios de aceite (binários)
- **CA-1-018**: motor calcula H.E.1 (75%), H.E.2 (100%), noturno, sáb/dom/fer conforme regra parametrizada por cliente/planta/vigência; teste com 2 regras distintas mostra resultados distintos para as mesmas horas.
- **CA-1-019**: sem teto provado, todos os itens saem "em conferência — teto não provado"; com teto cadastrado (I-04), H.T. acima do teto é sinalizado e faturáveis exigem conferência registrada.
- **CA-1-020**: relatório comparativo ponto × planilha do cliente é gerado por competência/planta/colaborador, com divergências agrupadas por origem e exportável para apresentação ao cliente.
- **CA-1-021**: baseline é coletado com protocolo de medição (janela/método) registrado; métrica (tempo de conciliação, dias envio→aprovação, dias aprovação→pagamento) é registrada desde a primeira competência.
- **CA-1-022**: tentativa de usar dado real antes de I-06 é recusada com motivo (prova negativa); demonstrações e testes rodam em fixture sintético.
- **CA-1-023**: toda alteração de valor, horas ou previsão gera registro de auditoria (quem, quando, por quê) — verificado por consulta após edição.
- **CA-1-024**: nenhuma superfície exibe "integração ativa" sem I-03 provado; o fallback manual é visível e operável (rótulo fiel).

## TDD da SPEC
- **RED**: cenário "calcular faturáveis sem teto cadastrado" → hoje a planilha calcula mesmo sem teto confiável (187:30 × 183:30 em disputa). Prova: folha de cálculo produz número sem validade contratual.
- **GREEN**: CA-1-018..024 em fixtures (2 regras distintas, teto vazio/preenchido, relatório com divergências, baseline parcial); prova: fail-closed (019), regras distintas (018), relatório exportável (020), protocolo registrado (021), recusa de dado real (022), auditoria (023), rótulo fiel (024).
- **REGRESSÃO**: regenerar relatório é idempotente; editar valor mantém auditoria; mudar regra contratual não altera competências já encerradas.

## Instruções para o Ethos
- Superfícies: motor de cálculo; regras contratuais parametrizadas; gerador/exportador do relatório comparativo; registro de baseline/métrica; trilha de auditoria.
- Fixtures: 2 regras contratuais sintéticas, teto vazio e teto fictício, tempos de baseline fictícios.
- Insumos embutidos na task: I-02 (baseline 3 meses — Renata/Meire: "quanto tempo leva a conciliação e quantos dias entre envio, aprovação e pagamento?"), I-04 (cláusula do teto — Renata/contrato VW).
- **Ponto de parada**: sem I-04, teto vazio + fail-closed (não é bloqueio de task — a pergunta vai junto). Sem I-02, baseline nasce coletando a partir da primeira competência executada, com ressalva explícita. Nunca inventar teto, fórmula contratual ou número de baseline.

## Checklist de aceite
- [ ] CA-1-018..024 provados em fixture
- [ ] Prova negativa de fail-closed (019) e de dado real (022) registradas
- [ ] Relatório comparativo exportável demostrado (entrega palpável da F1)
- [ ] Teste humano do Financeiro registrado

## Tasks vinculadas
| Task (fase.md) | Critérios | Leva |
|---|---|---|
| Calcular horas faturáveis com regra por cliente e fail-closed de teto | CA-1-018/019/022/023/024 | 5 |
| Emitir o relatório comparativo e registrar o baseline da medição | CA-1-020/021 | 6 |

## Emendas
(nenhuma)
