# SPEC-1-001 — Cadastro operacional e competência mensal

- **Fase**: F1 (Módulo 1 — Extração e Conciliação) · **Capacidades**: C1, C2 · **Prioridade**: ≤3 calls
- **Ambiente**: Skip (GoSkip + SkipCloud) — regra geral do consultor (22/09/2026)
- **Degrau da solução**: primeiro degrau — sem cadastro único de clientes/contratos/plantas/regras e sem a competência mensal como container do ciclo, nenhuma conciliação é possível. Troca a navegação por pastas/planilhas por um cadastro consultável.

## Contexto

- **Estado atual**: controles dispersos em planilhas (SharePoint/Excel), regras contratuais em memória das responsáveis, teto de horas em conflito (187:30 × 183:30), entidade empregadora/faturamento não confirmada (EEP DATA MANAGEMENT × EDGE AUTO).
- **Estado desejado**: cadastro de cliente (com entidade), projeto/planta, regra de medição e **teto configurável** por cliente/projeto/planta/vigência (nenhum valor padrão); competência mensal com status único e lista de colaboradores/documentos esperados.

## Atores e permissões
- RH/Medição (Meire): cadastra operacional, abre competência, mantém lista de colaboradores.
- Financeiro (Renata): consulta; valida dados contratuais (teto, entidade).
- CEO/Liderança (Bruno Perrotta): consulta.
- Nenhuma alteração de cadastro sem registro de autoria (quem/quando/por quê).

## Dados
Cliente, entidade empregadora/faturamento, projeto/comprador, planta (Anchieta, Curitiba, Taubaté…), vigência da regra, teto de horas (nullable), colaborador (nome, PT, área), competência (período, status), documentos esperados.

## Regras
1. Contrato só é cadastrado com entidade confirmada (I-09) — sem confirmação, recusa explícita com motivo.
2. Teto é campo configurável; **nunca** fixado em 187:30 ou 183:30 por padrão (DH-04).
3. Sem teto, o cálculo de faturáveis retorna "em conferência — teto não provado" (fail-closed).
4. Competência tem status único entre: em preparação · aguardando documentos · em conciliação · com divergência · liberada internamente · enviada ao cliente · aguardando aprovação · aprovada · faturada · aguardando pagamento · paga · cancelada/refaturamento em análise.
5. Nenhuma competência avança para liberação com colaborador sem situação definida.

## Fluxo e passos
1. Cadastrar cliente/entidade (com I-09 embutido: "qual entidade emprega e qual fatura cada contrato?").
2. Cadastrar projeto/planta/regra/vigência/teto (I-04 embutido: "trazer a cláusula/planilha contratual com o teto por planta").
3. Abrir competência → lista de colaboradores + documentos esperados + marcos.
4. Manter status por transição auditada.

## Exceções e rollback
- Entidade não confirmada → cadastro de contrato bloqueado com motivo (não é gate do projeto: a task pergunta e segue em fixture).
- Teto divergente entre fontes → cadastra como "em disputa", cálculo fail-closed.
- Exclusão nunca física: cadastro inativado com histórico.

## Critérios de aceite (binários)
- **CA-1-001**: contrato só cadastra com entidade empregadora/faturamento confirmada; sem isso, recusa com motivo registrado.
- **CA-1-002**: teto de horas é configurável por cliente/projeto/planta/vigência, sem valor padrão; a tela de regra exibe a vigência.
- **CA-1-003**: com teto vazio, qualquer tentativa de calcular faturável retorna "em conferência — teto não provado" (nunca número).
- **CA-1-004**: abrir competência cria ciclo com status único, lista de colaboradores, documentos esperados e marcos; cada transição de status é auditada (quem/quando/por quê).
- **CA-1-005**: sistema recusa liberar competência com colaborador sem situação definida (conciliado / divergente justificado / excluído / pendente assumido), com bloqueio explícito em tela.

## TDD da SPEC
- **RED**: cenário "criar contrato sem entidade confirmada" → sistema aceita hoje (não existe sistema; controle é planilha). Prova: registro da tentativa em fixture mostra aceitação sem validação.
- **GREEN**: CA-1-001..005 verificados em fixture sintética (2 clientes, 3 plantas, 1 competência); prova: recusa com motivo (001), campo teto vazio salvo sem default (002), resposta "em conferência" (003), transição auditada (004), bloqueio de liberação (005).
- **REGRESSÃO**: reabrir/fechar competência e reeditar teto preservam histórico; nenhuma alteração destrutiva.

## Instruções para o Ethos
- Superfícies: cadastro de cliente/contrato/regra; tela de competência; lista de colaboradores; trilha de auditoria.
- Dados de demonstração: fixtures sintéticos (nada real até I-06); nomes fictícios; teto vazio ou fictício.
- Insumos embutidos na task (perguntas junto com a execução): I-01 (aceite do núcleo — Bruno/Ricardo), I-04 (teto — Renata/contrato), I-09 (entidade — Bruno/Financeiro), I-10 (champion/RACI — liderança).
- **Ponto de parada**: se I-09 não vier, mantém cadastro de contrato bloqueado com motivo e segue com fixture; se I-04 não vier, teto vazio + fail-closed. Nunca inventar valor, entidade ou regra.

## Checklist de aceite
- [ ] CA-1-001..005 provados em fixture
- [ ] Auditoria de transições visível
- [ ] Nenhum dado real presente
- [ ] Teste humano do RH/Medição registrado

## Tasks vinculadas
| Task (fase.md) | Critérios | Leva |
|---|---|---|
| Cadastrar clientes, contratos e plantas com regras e tetos configuráveis | CA-1-001/002/003 | 1 |
| Abrir a competência do mês com lista de colaboradores e bloqueio de liberação | CA-1-004/005 | 2 |

## Emendas
(nenhuma)
